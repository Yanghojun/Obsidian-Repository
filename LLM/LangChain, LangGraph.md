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


# create_react_agent
`responseformat`: qwen2.5는 되는데, gemma3는 안됨.
현재는 gemma3로 dict 반환하게 해서 사용 중.

