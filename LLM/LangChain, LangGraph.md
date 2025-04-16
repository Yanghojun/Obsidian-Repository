# steram, astream
- output token을 yield하는 `generator`를 반환한다.


# Streaming
`stream_mode = values`
`chunk.items()`로 각 노드 단계마다, 모든 state key, state value에 접근 가능

`stream_mode = updates`
`chunk.items()`로 각 노드 단계마다, 업데이트된 **node 이름**, **어떤 state가 수정됐는지**에 대해 접근 가능
```python
for chunk in graph.stream(inputs, configs, stream_mode="updates"):
    for node_name, states in chunk.items():
        print(node_name)
        print(states)            # 여기 states객체에서 state_key, state_value에 접근 가능.
```

두개 차이가 뭐지..?

# conditional_edges
```python
# `tools_condition` 함수는 챗봇이 도구 사용을 요청하면 "tools"를 반환하고, 직접 응답이 가능한 경우 "END"를 반환 
graph_builder.add_conditional_edges( source="chatbot", path=route_tools, # route_tools 의 반환값이 "tools" 인 경우 "tools" 노드로, 그렇지 않으면 END 노드로 라우팅 
path_map={"tools": "tools", END: END}, )
```
chatbot에서 state에 값을 담고, route_tools 함수에서, state값을 보면서 어디로 보낼지 string으로 반환.
# create_react_agent
`responseformat`: qwen2.5는 되는데, gemma3는 안됨.
현재는 gemma3로 dict 반환하게 해서 사용 중.

# 발생하는 에러 정리
```
return {"messages": [result]}   # 에러 발생

# 직접 state["messages"].append(result)를 하면 에러 안남..
```
langgraph에서 with_structured_output으로 출력한 결과를 result로 넣으면 에러남.