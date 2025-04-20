# 비동기 코드 흐름
send 함수가 내 요약 LLM과 어떻게 통신하는지 확인할 것.


- bug
	- texts, summary_text의 개수가 안맞음.
		- texts는 partition_pdf에서 나온 text들의 리스트,
		  text_summary는 text_spliter를 통해 새로 생성된 리스트에 대한 요약이니 당연히 안맞음.


# Crawltool 어떻게 작동시키는지?
- 
