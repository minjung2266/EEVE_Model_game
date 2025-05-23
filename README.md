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
    # 1. 최고의 친구 엔딩
    if s["친밀도"] >= 100 and s["기분"] >= 70 and s["건강"] >= 70:
        return f"🎉 최고의 친구 엔딩 : 주인의 사랑덕분에 아가 다마는 사랑둥이 다마고치가 되었어요!"

    # 2. 폭발 엔딩
    if s["외로움"] >= 80 and s["분노"] >= 80:
        return f"💥 폭발한 다마 엔딩 : 외롭고 화나서 다마고치는 폭발하고 말았어요!"

    # 3. 우울증 엔딩
    if s["외로움"] >= 80:
        return f"🌧️ 조용한 이별 엔딩 : 외로운 다마고치는 우울증에 걸려 다른 주인을 찾아 떠나버렸어요"

    # 4. 분노 엔딩 
    if s["분노"] >= 80:
        return f"😡 분노 엔딩 : 사랑 없이 혼나기만 한 다마고치는 화가 나서 떠나버렸어요"

    # 5. 병약한 엔딩 
    if s["건강"] <= 30:
        return f"🤒 병약한 다마고치 엔딩 : 다마고치는 병에 걸려 병원으로 떠났어요"

    # 6. 어사 엔딩 
    if s["친밀도"] < 20:
        return f"💔 어사 엔딩 : 당신과의 어색한 사이를 견디지 못한 다마는 당신을 떠났어요"

    # 7. 불쾌한 엔딩 
    if s["기분"] <= 20:
        return f"😢 기분이 불쾌해 떠나버린 엔딩 : 다마는 당신이 싫대요"

    # 8. 더러운 엔딩 
    if s["청결"] <= 20 or s["기저귀"] >= 80:
        return f"💩 청결 문제 엔딩 : 기저귀를 방치한 당신 때문에 다마고치가 떠나버렸어요..."

    # 9. 과식 엔딩
    if s["배부름"] >= 85:
        return f"🍰 과식 엔딩 : 살이 찐 다마는 당신을 원망하며 떠났어요..."

```

### 다마고치 랜덤 리액션
```
    if s["배부름"] < 30: talk_list.append("꼬르륵... 배고파... 🍚🥹")
    if s["배부름"] > 50: talk_list.append("꺼억.. 밥 그만 좀 줘")
    if s["기분"] < 30: talk_list.append("기분이 안좋아... 놀아줘... 😢")
    if s["청결"] < 30: talk_list.append("찝찝해... 씻겨줘... 🛁")
    if s["기저귀"] > 50: talk_list.append("나 떵 마려워... 🧻")
    if s["건강"] < 50: talk_list.append("몸이 아파... 🤒")
    if s["외로움"] > 70: talk_list.append("너무 외로워... 🥺")
    if s["분노"] > 60: talk_list.append("화났어 나... 😡")
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
      <img src="https://github.com/user-attachments/assets/21efcdf9-455e-4b4e-bf63-b6b0c6912acf" width="400"/><br/>
      <sub>초기화면(행동 비활성화)</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/878def53-8aed-4795-acb4-2855990ea9e9" width="400"/><br/>
      <sub>유저 입력 후 메세지</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/d8b7b6dc-ac33-4f3d-98ed-5cbacabfcadb" width="400"/><br/>
      <sub>행동에 따른 리액션 / 상태 메시지</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/91303bed-e567-49bf-a3a6-8fea5de5577f" width="400"/><br/>
      <sub>다마고치와 놀기 기능</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/952839e1-20e7-4b2c-95bc-059668d2f2d3" width="400"/><br/>
      <sub>놀아주기 이후 상태 (지면 부정 이기면 긍정)</sub>
    </td>
    <td align="center" valign="bottom">
      <img src="https://github.com/user-attachments/assets/fa3d1050-474c-4ee3-9fb7-189c08fe5711" width="400"/><br/>
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
- 프롬프트 설계의 디테일 부족
  - 다마고치의 상태(기분, 건강, 행동 등)에 대한 구체적인 설정 없이 단순한 지시만 전달되어, 모델의 응답이 일관성과 감정 표현 면에서 부족하게 느껴졌다.
  
- LLM 활용의 한계 
  1. 감정형 대화보다는 다소 직설적이고 기계적인 표현이 반복됨  
  2. 상황에 따른 다양한 감정 변화나 자연스러운 반응 생성이 제한적이었음


#### 추후 보완할 것
- 다마고치의 상태(기분, 건강 등)를 포함한 프롬프트 컨텍스트를 정교화하여 응답의 감정과 맥락 일관성 개선
- 단순 버튼 기반 반응 구조를 제거하고, 사용자 입력을 기반으로 LLM이 자율적으로 감정 표현을 생성하도록 개선
- 보다 자연스럽고 감정에 공감하는 반응 생성을 위해, OpenChat, Zephyr, LLaMA2-Chat 등 감성 대화에 최적화된 모델로 대체 계획

- 예시
```
# 키워드 기반 상태 변화 규칙
def update_state_from_input(user_input, state):
    if "밥" in user_input:
        state["배부름"] = min(100, state["배부름"] + 20)
        state["기분"] = min(100, state["기분"] + 10)

    if "씻" in user_input or "샤워" in user_input:
        state["청결"] = min(100, state["청결"] + 30)
        state["기분"] = min(100, state["기분"] + 5)

    if "혼냈" in user_input or "화냈" in user_input:
        state["분노"] = min(100, state["분노"] + 20)
        state["친밀도"] = max(0, state["친밀도"] - 10)
        state["기분"] = max(0, state["기분"] - 10)

    if "병원" in user_input:
        state["건강"] = min(100, state["건강"] + 30)
        state["기분"] = min(100, state["기분"] + 5)

    if "놀" in user_input or "산책" in user_input:
        state["기분"] = min(100, state["기분"] + 15)
        state["외로움"] = max(0, state["외로움"] - 20)
        state["친밀도"] = min(100, state["친밀도"] + 10)

    # 기타 상황 업데이트 생략 가능
    return state
```


