# Potatalk

Django 기반의 OpenAI GPT 모델을 활용한 챗봇 서비스 앱입니다.

## 개요

레시피 특화 LLM 모델 파인튜닝을 통해 기존 복잡한 응답 대신 간단하게 필요한 재료, 조리법만 응답해
한눈에 보기 좋게 해주는 서비스입니다.

## 주요 기능

- **실시간 챗봇 대화**: 사용자 질문에 대한 AI 답변 생성
- **대화 내역 저장**: 질문과 답변을 데이터베이스에 저장
- **대화 내역 조회**: 저장된 대화 내역 조회 기능
- **상태 관리**: 대화 내역의 활성/비활성 상태 관리

## 기술 스택

- **Framework**: Django
- **LLM**: OpenAI GPT-3.5 Turbo (Fine-tuned)
- **Library**: LangChain OpenAI
- **API**: Django REST Framework

## 프로젝트 구조

```
kyuilLLM/
├── __init__.py
├── admin.py          # Django 관리자 설정
├── apps.py           # 앱 설정
├── models.py         # 데이터베이스 모델
├── urls.py           # URL 라우팅
├── views.py          # 뷰 및 API 엔드포인트
├── tests.py          # 테스트 코드
└── migrations/       # 데이터베이스 마이그레이션
```

## 모델

### kyuilLLM

대화 내역을 저장하는 모델입니다.

- `question` (TextField): 사용자의 질문
- `answer` (TextField): AI의 답변
- `status` (BooleanField): 대화 내역 상태 (1: 활성, 0: 삭제)
- `createed_date` (DateTimeField): 생성 일시 (Period 모델 상속)
- `updated_date` (DateTimeField): 수정 일시 (Period 모델 상속)


## API 엔드포인트

### 1. 메시지 페이지 렌더링

**URL**: `/kyuil/`  
**Method**: `GET`  
**View**: `KyuilLLMView`  
**설명**: 챗봇 대화 인터페이스를 제공하는 페이지를 렌더링합니다.

### 2. 질문 입력 및 답변 생성

**URL**: `/kyuil/input/`  
**Method**: `POST`  
**View**: `InputAPI`  
**설명**: 사용자의 질문을 받아 GPT 모델로 답변을 생성하고 데이터베이스에 저장합니다.


**기능**:
- 사용자 질문을 받아 OpenAI Fine-tuned 모델(`ft:gpt-3.5-turbo-0125:personal::AFdUlGjP`)로 답변 생성
- 생성된 질문과 답변을 데이터베이스에 저장
- 트랜잭션 처리로 데이터 일관성 보장

