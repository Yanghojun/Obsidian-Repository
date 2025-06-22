# 비동기 코드 흐름
send 함수가 내 요약 LLM과 어떻게 통신하는지 확인할 것.


- bug
	- texts, summary_text의 개수가 안맞음.
		- texts는 partition_pdf에서 나온 text들의 리스트,
		  text_summary는 text_spliter를 통해 새로 생성된 리스트에 대한 요약이니 당연히 안맞음.


# MCP 적용
참고: https://modelcontextprotocol.io/quickstart/server#why-claude-for-desktop-and-not-claude-ai

- MCP의 3가지 main concept
	1. File, API 등의 Resource를 제공한다
	2. Tool을 제공한다
	3. Prompt를 제공한다.

- 본 튜토리얼은 Tool 제공에 집중한 MCP 튜토리얼이다.

uv로 기본적인 환경 구성을 한다.
windows claude desktop app에서 내가 만든 Tool을 claude 3.7 sonnet 이 사용 후 답변을 생성하는걸 볼 수 있다.

- C:\Users\hojun_window\AppData\Roaming\Claude\claude_desktop_config.json
	```json
	{
	    "mcpServers": {
	        "weather": {
	            "command": "uv",
	            "args": [
	                "--directory",
	                "C:\\Users\\hojun_window\\Desktop\\workspace\\play_ground\\uv_study\\weather",
	                "run",
	                "weather.py"
	            ]
	        }
	    }
	}
	```
- C:\Users\hojun_window\Desktop\workspace\play_ground\uv_study\weather\weather.py
	```python
	from typing import Any
	import httpx
	from mcp.server.fastmcp import FastMCP
	
	# Initialize FastMCP server
	mcp = FastMCP("weather")
	
	# Constants
	NWS_API_BASE = "https://api.weather.gov"
	USER_AGENT = "weather-app/1.0"
	
	async def make_nws_request(url: str) -> dict[str, Any] | None:
	    """Make a request to the NWS API with proper error handling."""
	    headers = {
	        "User-Agent": USER_AGENT,
	        "Accept": "application/geo+json"
	    }
	    async with httpx.AsyncClient() as client:
	        try:
	            response = await client.get(url, headers=headers, timeout=30.0)
	            response.raise_for_status()
	            return response.json()
	        except Exception:
	            return None
	
	def format_alert(feature: dict) -> str:
	    """Format an alert feature into a readable string."""
	    props = feature["properties"]
	    return f"""
	Event: {props.get('event', 'Unknown')}
	Area: {props.get('areaDesc', 'Unknown')}
	Severity: {props.get('severity', 'Unknown')}
	Description: {props.get('description', 'No description available')}
	Instructions: {props.get('instruction', 'No specific instructions provided')}
	"""
	
	@mcp.tool()
	async def get_alerts(state: str) -> str:
	    """Get weather alerts for a US state.
	
	    Args:
	        state: Two-letter US state code (e.g. CA, NY)
	    """
	    url = f"{NWS_API_BASE}/alerts/active/area/{state}"
	    data = await make_nws_request(url)
	
	    if not data or "features" not in data:
	        return "Unable to fetch alerts or no alerts found."
	
	    if not data["features"]:
	        return "No active alerts for this state."
	
	    alerts = [format_alert(feature) for feature in data["features"]]
	    return "\n---\n".join(alerts)
	
	@mcp.tool()
	async def get_forecast(latitude: float, longitude: float) -> str:
	    """Get weather forecast for a location.
	
	    Args:
	        latitude: Latitude of the location
	        longitude: Longitude of the location
	    """
	    # First get the forecast grid endpoint
	    points_url = f"{NWS_API_BASE}/points/{latitude},{longitude}"
	    points_data = await make_nws_request(points_url)
	
	    if not points_data:
	        return "Unable to fetch forecast data for this location."
	
	    # Get the forecast URL from the points response
	    forecast_url = points_data["properties"]["forecast"]
	    forecast_data = await make_nws_request(forecast_url)
	
	    if not forecast_data:
	        return "Unable to fetch detailed forecast."
	
	    # Format the periods into a readable forecast
	    periods = forecast_data["properties"]["periods"]
	    forecasts = []
	    for period in periods[:5]:  # Only show next 5 periods
	        forecast = f"""
	{period['name']}:
	Temperature: {period['temperature']}°{period['temperatureUnit']}
	Wind: {period['windSpeed']} {period['windDirection']}
	Forecast: {period['detailedForecast']}
	"""
	        forecasts.append(forecast)
	
	    return "\n---\n".join(forecasts)
	
	if __name__ == "__main__":
	    # Initialize and run the server
	    mcp.run(transport='stdio')
	```

# Multi-Turn
- 우리 Discord bot에서 multiturn 구현이 가능한 이유
- `Memory Saver`를 통해 대화를 자동 저장하고, 이를 `thread_id`를 통해 새로운 langgraph에서 invoke 할 때 사용할 수 있다.