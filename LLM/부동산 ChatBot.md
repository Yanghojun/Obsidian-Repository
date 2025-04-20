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



