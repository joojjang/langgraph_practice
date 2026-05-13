# [iMBank DiGital Banker] LangGraph 멀티 에이전트 프로젝트

## 프로젝트 개요

사용자의 운동 관련 고민을 입력받아  
LangGraph 기반 Multi-Agent 시스템을 통해 다음 과제를 수행하는 AI 운동 추천 프로그램

- 증상 추출
- 운동 추천
- 최종 건강 가이드 생성

> ### LangGraph
>
> LLM을 기반으로 상태를 유지하고(Stateful), 여러 단계에 걸쳐 작동하는(multi-step) 에이전트를 구축하기 위한 라이브러리  
> <img width="108" height="432" alt="chain" src="https://github.com/user-attachments/assets/a8f39514-788c-4b1a-a2de-909589954dfe" />

## 구현 포인트

- LangGraph 기반 상태 머신 구현
- Multi-Agent 구조 설계
- Prompt Chaining
- Ollama 기반 로컬 LLM (exaone3.5) 활용
- Agent별 역할 분리
- 상태(State) 기반 데이터 전달

## 기술 스택

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-121212?style=for-the-badge)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge)

## 시스템 아키텍처

사용자 질의는 LangGraph State를 기반으로  
**3개의 Agent를 순차적으로 통과함.**

User Query  
↓  
Extractor Agent  
↓  
Exercise Agent  
↓  
Answer Agent  
↓  
Result

> ### 각 Agent의 역할
>
> 각 Agent는 역할별 PromptTemplate을 사용하며,  
> 역할별 Prompt를 분리함으로써 단일 프롬프트 대비 응답 품질과 구조화를 개선할 수 있음.
>
> 1. Extractor Agent
>
> - 사용자 질문에서 현재 상태 및 증상을 추출
> - PromptTemplate 기반 증상 추론 수행
>
> 2. Exercise Agent
>
> - 추출된 증상을 기반으로 운동 추천
> - 체력 저하 및 체중 증가에 적합한 운동 후보 생성
>
> 3. Answer Agent
>
> - 증상 + 운동 리스트를 종합
> - 개조식 형태의 최종 건강 가이드 생성

## 코드 실행 방법

1. 터미널에서 다음 패키지 설치

   ```shell
   pip install ollama
   pip install langchain langgraph langchain-community chromadb sqlite-utils
   pip install grandalf
   ```

2. Ollama 모델 다운로드
   ```shell
   ollama pull exaone3.5:7.8b
   ```
3. Run All 혹은 Shift + Control + Return

## 개선 방안

- 운동 강도 및 사용자 연령 반영
- RAG 기반 건강 문서 검색 추가
- FastAPI 기반 웹 챗봇 연동
- 운동 추천 개인화
- 운동 영상 추천 기능 추가
- Streaming 응답 적용
