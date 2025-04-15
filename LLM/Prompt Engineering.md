[[구글개발자_프롬프트엔지니어링팁.pdf]]

# 퍼플렉시티의 위 pdf에 대한 요약
구글이 최근 발표한 69페이지 분량의 프롬프트 엔지니어링에 관한 백서(저자: Lee Boonstra)는 대규모 언어 모델(LLM)과의 상호작용을 최적화하기 위한 포괄적인 가이드를 제공합니다. 기술 매체들에 의해 널리 보도된 이 문서는 LLM을 생산 환경에서 다루는 개발자, 연구자, AI 전문가들에게 필수적인 자료로 빠르게 자리 잡았습니다. 소셜 미디어 플랫폼에서의 논의와 공유가 더해지며 온라인에서 그 인기가 급상승하고 있습니다.

[

![aibase.com favicon](https://www.google.com/s2/favicons?sz=128&domain=aibase.com)

AIbase

Optimizing AI Models Through Prompt Engineering - AIbase









](https://www.aibase.com/news/www.aibase.com/news/17051)

[

![learnprompting.org favicon](https://www.google.com/s2/favicons?sz=128&domain=learnprompting.org)

learnprompting.org

Shot-Based Prompting: Zero-Shot, One-Shot, and Few-Shot Prompting









](https://learnprompting.org/docs/basics/few_shot)

[

![gptaiflow.tech favicon](https://www.google.com/s2/favicons?sz=128&domain=gptaiflow.tech)

gptaiflow

[PDF] Author: Lee Boonstra - GPT AI Flow









](https://www.gptaiflow.tech/assets/files/2025-01-18-pdf-1-TechAI-Goolge-whitepaper_Prompt%20Engineering_v4-af36dcc7a49bb7269a58b1c9b89a8ae1.pdf)

![laurencemoroney.com favicon](https://www.google.com/s2/favicons?sz=128&domain=laurencemoroney.com)

![pluralsight.com favicon](https://www.google.com/s2/favicons?sz=128&domain=pluralsight.com)

![arxiv.org favicon](https://www.google.com/s2/favicons?sz=128&domain=arxiv.org)

+4

소스

## 핵심 프롬프트 기법

백서에는 효과적인 LLM 상호작용의 근간을 이루는 몇 가지 기본적인 프롬프트 기법이 설명되어 있습니다. 제로샷 프롬프트는 예시 없이 지시를 제공하며, 모델의 사전 학습된 지식에 의존합니다[1](https://www.aibase.com/news/www.aibase.com/news/17051). 원샷 및 퓨샷 프롬프트는 작업 전에 하나 이상의 예시를 포함하여 성능을 향상시키며, 기대치를 명확히 하는 데 도움을 줍니다[2](https://learnprompting.org/docs/basics/few_shot). 이러한 기법은 맥락에서 학습하는 모델의 능력을 활용하여 출력의 정확성과 일관성을 개선합니다.

시스템 프롬프트는 전체 대화에 대한 포괄적인 규칙이나 맥락을 설정하며, 역할 프롬프트는 LLM에 특정 페르소나를 부여하여 창의성을 높이고 응답을 맞춤화합니다[3](https://www.gptaiflow.tech/assets/files/2025-01-18-pdf-1-TechAI-Goolge-whitepaper_Prompt%20Engineering_v4-af36dcc7a49bb7269a58b1c9b89a8ae1.pdf). 맥락 프롬프트는 모델 출력의 관련성과 정확성을 향상시키기 위해 필요한 배경 정보를 제공합니다[4](https://laurencemoroney.com/2023/12/19/prompts.html). 이러한 핵심 기법들은 프롬프트 엔지니어가 LLM의 동작을 미세 조정하고 다양한 응용 분야에서 보다 목표 지향적이고 효과적인 결과를 달성할 수 있도록 하는 다재다능한 도구 세트를 제공합니다.

![aibase.com favicon](https://www.google.com/s2/favicons?sz=128&domain=aibase.com)

![learnprompting.org favicon](https://www.google.com/s2/favicons?sz=128&domain=learnprompting.org)

![gptaiflow.tech favicon](https://www.google.com/s2/favicons?sz=128&domain=gptaiflow.tech)

4 소스들

## 고급 프롬프트 전략

이 백서에서는 LLM을 사용하여 복잡한 작업을 처리하기 위한 혁신적인 기술을 소개합니다. 체인 오브 쏘트(Chain-of-Thought, CoT) 프롬프팅은 모델이 단계별 추론을 통해 논리적 출력을 개선하도록 안내합니다[1](https://www.aibase.com/news/www.aibase.com/news/17051). ReAct(Reason + Act)는 내부 추론과 외부 도구 사용을 결합하여 실제 문제 해결 능력을 향상시킵니다[2](https://learnprompting.org/docs/basics/few_shot). 기타 고급 전략에는 다음이 포함됩니다:

- 트리 오브 쏘트(Tree-of-Thoughts, ToT): 해결책에 도달하기 전에 여러 추론 경로를 탐색
    
- 셀프 컨시스턴시 보팅(Self-Consistency Voting): 높은 온도에서 모델을 반복적으로 프롬프팅하고 가장 일관된 답변을 선택
    
- 시스템, 역할 및 맥락 프롬프팅(System, Role, and Contextual Prompting): 포괄적인 규칙 정의, 특정 페르소나 할당 또는 배경 정보 제공을 통해 LLM의 동작을 조정[3](https://www.gptaiflow.tech/assets/files/2025-01-18-pdf-1-TechAI-Goolge-whitepaper_Prompt%20Engineering_v4-af36dcc7a49bb7269a58b1c9b89a8ae1.pdf)
    

이러한 방법은 LLM의 잠재적 응용 범위를 크게 확장하여 복잡한 작업에 대해 더 정교하고 신뢰할 수 있는 출력을 가능하게 합니다.

![aibase.com favicon](https://www.google.com/s2/favicons?sz=128&domain=aibase.com)

![learnprompting.org favicon](https://www.google.com/s2/favicons?sz=128&domain=learnprompting.org)

![gptaiflow.tech favicon](https://www.google.com/s2/favicons?sz=128&domain=gptaiflow.tech)

3 소스들

## 코드 생성 기법

코드 프롬프트 애플리케이션은 개발자들에게 워크플로우와 생산성을 향상시킬 수 있는 강력한 도구를 제공하며, 크게 확장되었습니다. 대규모 언어 모델(LLM)은 이제 전체 함수 생성부터 복잡한 알고리즘 디버깅까지 다양한 코딩 작업을 지원할 수 있습니다. 주요 애플리케이션은 다음과 같습니다:

- 코드 생성: 개발자는 특정 함수, 클래스 또는 알고리즘을 선택한 프로그래밍 언어로 요청할 수 있습니다. 예를 들어, "퀵소트를 구현하는 Python 함수를 작성하세요"와 같은 프롬프트는 작동하는 구현을 생성할 수 있습니다[1](https://www.pluralsight.com/resources/blog/software-development/prompt-engineering-for-developers).
    
- 코드 설명: LLM은 복잡한 코드 스니펫을 줄 단위로 기능을 설명하며 분석할 수 있습니다. 이는 특히 레거시 코드를 이해하거나 새로운 프로그래밍 개념을 배우는 데 유용합니다[1](https://www.pluralsight.com/resources/blog/software-development/prompt-engineering-for-developers).
    
- 자동화된 테스트: 프롬프트를 설계하여 주어진 코드에 대한 단위 테스트를 생성할 수 있으며, 이는 코드 품질을 보장하고 수동 테스트 노력을 줄이는 데 도움을 줍니다[1](https://www.pluralsight.com/resources/blog/software-development/prompt-engineering-for-developers).
    
- 코드 최적화: 기존 코드를 분석하여 LLM은 성능 개선이나 더 효율적인 알고리즘을 제안할 수 있습니다[2](https://arxiv.org/html/2406.00515v1).
    
- 문서화 생성: 개발자는 LLM에게 함수 설명, 매개변수 설명 및 사용 예제를 포함한 명확하고 포괄적인 코드 문서를 생성하도록 요청할 수 있습니다[3](https://swabhs.com/fall23-csci499-lm4nlp/assets/reports/KeyuHe_MaxLi_JosephLiu.pdf).
    

이러한 애플리케이션은 초기 코딩부터 유지보수 및 최적화에 이르기까지 소프트웨어 개발 프로세스를 크게 향상시킬 수 있는 프롬프트 엔지니어링의 가능성을 보여줍니다. LLM이 계속 발전함에 따라 점점 더 복잡한 코딩 작업을 지원하는 능력이 성장할 가능성이 높으며, 이는 소프트웨어 개발의 지형을 더욱 변화시킬 것입니다.

![pluralsight.com favicon](https://www.google.com/s2/favicons?sz=128&domain=pluralsight.com)

![arxiv.org favicon](https://www.google.com/s2/favicons?sz=128&domain=arxiv.org)

3 소스들

## 모범 사례 및 동향

백서에서는 효과적인 프롬프트 설계를 위한 몇 가지 주요 모범 사례를 강조하고 있습니다. 여기에는 명확한 지침 사용, 관련 예제 제공, 원하는 출력 형식 지정 등이 포함됩니다. 또한 창의성과 신뢰성의 균형을 맞추기 위해 온도, top-K, top-P와 같은 샘플링 매개변수의 반복적인 설계와 신중한 조정을 권장합니다[1](https://www.aibase.com/news/www.aibase.com/news/17051)[2](https://learnprompting.org/docs/basics/few_shot). AI 자체를 사용한 자동 프롬프트 생성, 멀티모달 입력 통합, 다양한 모델 간 프롬프트 표준화 노력과 같은 프롬프트 엔지니어링의 새로운 트렌드도 논의됩니다[3](https://www.gptaiflow.tech/assets/files/2025-01-18-pdf-1-TechAI-Goolge-whitepaper_Prompt%20Engineering_v4-af36dcc7a49bb7269a58b1c9b89a8ae1.pdf). 이러한 발전은 LLM과 작업하는 과정을 간소화하고 다양한 유형의 데이터와 작업을 처리하는 능력을 확장하는 것을 목표로 합니다.

![aibase.com favicon](https://www.google.com/s2/favicons?sz=128&domain=aibase.com)

![learnprompting.org favicon](https://www.google.com/s2/favicons?sz=128&domain=learnprompting.org)

![gptaiflow.tech favicon](https://www.google.com/s2/favicons?sz=128&domain=gptaiflow.tech)

3 소스들