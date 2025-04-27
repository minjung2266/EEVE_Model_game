## 🌱 다마일기 : 다마고치 성장일기

### 🔎 프로젝트 개요
이 프로젝트는 **EEVE-Korean-10.8B LLM**을 활용한 감성 기반 상호작용 게임입니다.
사용자는 다양한 행동을 선택해 다마고치와 교감하며, 캐릭터의 감정과 상태에 실시간으로 반응하는 AI와 상호작용할 수 있습니다.

### 📖프로젝트 목적
* 다양한 프롬프팅 시도
  - 감정형 인터랙션은 일방적인 질의응답이 아니라 유저와 지속적으로 상호작용하며 감정과 상태를 반영한 대화가 가능
  - 프로젝트에서는 다마고치의 상태에 따라 상황별로 다른 프롬프트를 설계하여 LLM이 자연스럽고 감정이 반영된 응답을 생성하도록 유도
  - 프롬프트를 세분화하고 상황에 맞게 조정하는 방식은으로 모델의 감성 표현 능력과 맥락 이해도를 실험하는 데 효과적이라 판단

### 📆 개발 기간
2025.04.20 ~ 2025.04.25

### 🛠️ 기술 스택
<p align="left"> 
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/> <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white"/>
 <img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge"/> <img src="https://img.shields.io/badge/EEVE_Korean_10.8B-FFD400?style=for-the-badge&logoColor=black"/> </p>


### 🧷WBS
| 작업명 | 작업 내용 | 산출물 | 날짜 |
|--------|------------|---------|------|
| 상태 변수 설계 | 다마고치의 상태 변수 정의 (친밀도, 기분, 건강, 배부름 등) | 상태 변수 딕셔너리 구조 | 2025-04-20 |
| 행동 정의 및 구현 | 사용자 행동에 따라 상태가 변화하는 로직 구현 | 행동-상태 변화 함수 | 2025-04-20 |
| LLM 프롬프트 설계 | 상황별 챗봇 프롬프트 작성 및 응답 처리 | 프롬프트 스크립트, 챗봇 응답 로직 | 2025-04-21 ~ 2025-04-22 |
| 콘솔 버전 완성 | Jupyter 기반의 다마고치 CLI 인터페이스 구현 | damagochi.ipynb | 2025-04-21 ~ 2025-04-22 |
| 웹 UI 전환 | Streamlit을 이용한 웹 인터페이스 구현 | Streamlit 앱 (tama_app.py) | 2025-04-23 |
| 다마고치 이미지 추가 | 행동별 이미지 출력 기능 연동 | 다마고치 표정 지정 | 2025-04-23 |
| 엔딩기능 추가 | 성장 조건 도달 시 엔딩 처리 및 상태 초기화 | 엔딩 조건 지정 | 2025-04-24 |
| 시연준비 | 리드미 작성 및 발표 준비 | readme 자료 | 2025-04-23 ~ 2025-04-24 |

---- 

### 🎮 게임 규칙
1. 이름 설정 : 다마고치의 이름을 설정합니다. (미입력 시 행동버튼 비활성화)
2. 다마고치 돌보기 : 현재 다마고치의 상태에 따라 행동버튼을 클릭하여 교감합니다.
3. 성장완료 : 성장 조건에 만족하면 다마고치는 어른이 되어 엔딩화면이 나옵니다.

### 엔딩 분기
```
    if st.session_state.turn < 20:
        return None, None
    if s["친밀도"] >= 100 and s["기분"] >= 70 and s["건강"] >= 70:
        return "🎉 최고의 친구 엔딩", "주인의 사랑덕분에 아가 다마는 사랑둥이 다마고치가 되었어요!"
    elif s["외로움"] >= 80:
        return "🌧️ 조용한 이별 엔딩", "외로웠던 다마고치는 다른 주인을 찾아 떠나버렸어요"
    elif s["분노"] >= 70:
        return "😡 분노 엔딩", "사랑 없이 혼나기만 한 다마고치는 떠나버렸어요"
    elif s["건강"] <= 30:
        return "🤒 병약한 다마고치 엔딩", "다마고치는 병에 걸려 병원으로 떠났어요"
    elif s["친밀도"] < 20:
        return "💔 어사 엔딩", "당신과의 어색한 사이를 견디지 못한 다마는 당신을 떠났어요"
    elif s["기분"] <= 20:
        return "😢 다마의 심경을 거슬리게 해서 떠나버린 엔딩", "당신은 다마 달래기에 실패했습니다"
```


### ⭐ 주요 기능
| 기능 | 설명 |
|------|------|
| 사용자 입력값 확인 | user_name 입력 여부 유효성 검증 |
| 다마고치 상태 관리 | 행동방식에 따른 상태 수치 실시간 관리 |
| 행동 선택 시스템 | 버튼 클릭을 통한 상태 수치 변화 |
| LLM 대화 응답 | 행동 결과 기반 감정형 자연어 응답 생성 |
| 상황별 이미지 출력 | 행동에 따른 표정·배경 이미지 출력 |
| 턴 기반 진행 & 상태 갱신 | 행동 후 응답 출력 → 상태 자동 갱신 |
| 엔딩 조건 판별 | 친밀도 기준 도달 시 성장 엔딩 출력 |
| 초기화 및 재시작 기능 | 엔딩 후 상태 초기화 및 새 게임 시작 |
| Streamlit 기반 UI | 세션 상태 반영형 웹 인터페이스 구성 |

---- 

### 🧠 프롬프트 예시 
```
{
  "role": "system",
  "content": """
  너는 아주 귀엽고 어린 5살 다마고치야. 
  말투는 짧고 귀엽고 솔직해야 해. 
  문장은 최대 두 문장 이하로 말하고, "~처럼", "마치" 같은 비유는 쓰지 않아. 
  어려운 말은 피하고, 어린아이처럼 감정을 표현해줘.
  사용자가 행동을 해주면, 그 행동이 좋았는지 싫었는지를 지금 느끼는 기분으로 반응해줘.
  """
}
```

### 🤖 AI 응답 방식
```
{ "role": "assistant", "content": "우와! 배불러서 기분 좋아! 민정이 최고~" }
```

### 📺시연 예시
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/461ee3f2-6f1c-485d-af49-7537d84bd8d7" width="400"/><br/>
      <sub>초기화면</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ef082cc4-b40b-440d-b225-9d6b66c48bad" width="400"/><br/>
      <sub>초기화면 (행동 비활성화)</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/c8657d34-ec79-4ae4-8857-b56c8599ea03" width="400"/><br/>
      <sub>유저 입력 후 메세지</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/85d496d9-b6c3-4926-9f13-f5e9bb754479" width="400"/><br/>
      <sub>다마 상태 업데이트</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/9caa17e8-122c-45f8-b7bf-d12b4fc6fab4" width="400"/><br/>
      <sub>엔딩 옵션</sub>
    </td>
    <td align="center" valign="bottom">
      <img src="https://github.com/user-attachments/assets/06641f8c-7adc-4da7-a643-568a5051b5ad" width="400"/><br/>
      <sub>엔딩 화면</sub>
    </td>
</td>

  </tr>
</table>

----

### ☺️ 회고
#### 잘한점
  * 유저이름 입력 유효성 검사 
    - 이름이 입력되면 다마고치가 사용자 이름을 불러주는 인터랙션으로 사용자에게 몰입도를 줄 수 있다
  * 세션 관리 
    -  상태 정보를 유지 + 조건 분기로 UI 관리

#### 아쉬운 점
 * 프롬프트 설계 디테일에 대한 아쉬움
     * 상세한 상황 설정이 없어 실제 모델 응답이 일관된다는 점이 아쉬웠다
  
#### 추후 보완할 것
- 상태 기반 프롬프트 추가 : 행동-상태에 대한 조합을 늘려 다양한 답변 생성하기 ex) 밥주기 -> 기분 (좋음 보통 나쁨) / 배부름 (높음 보통 낮음) 에 따라 다른 답변 생성

- temperature 설정 : 특정 상황에는 창의적인 대사, 반복 상황에는 통제된 반응을 보이도록 설정

