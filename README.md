<div align="center">

#  비계 및 시설물 안전 관리를 위한 실시간 모니터링 시스템: GSS

### [infogssiot.com](https://infogssiot.com) 운영 및 기술 지원

<img width="800" alt="GSS 메인 화면" src="https://github.com/user-attachments/assets/0797b5ef-b189-4157-b580-673022f08002" />

</div>

---

## 📝 프로젝트 소개
건설 현장의 핵심 가설 구조물인 **비계(Scaffolding)의 안전 상태를 실시간으로 관제**하는 시스템입니다. MPU-6500 센서로부터 수집되는 미세한 기울기 및 진동 데이터를 백엔드에서 정밀 가공하여 사고를 사전에 예방합니다. 저사양 하드웨어의 한계를 소프트웨어 로직으로 극복하고, 대규모 시계열 데이터의 안정적인 흐름을 설계하는 데 주력했습니다.

#### 동기
- 건설 현장 내 비계(가설 구조물)의 기울어짐이나 붕괴 징후를 실시간으로 포착하여 중대재해 예방
- 센서 설치 시 발생하는 물리적 오차와 현장 노이즈를 백엔드 로직으로 보정하여 데이터 신뢰성 확보
- 기존의 사후 점검 방식에서 벗어나, 데이터 기반의 상시 모니터링 및 즉각 대응 체계 구축

#### 목표
- MPU-6500 센서를 활용한 시설물 기울기 및 진동 실시간 정밀 측정
- Node.js 기반 실시간 데이터 파이프라인 및 대규모 시계열 데이터 관리 체계 구축
- 서버 측 자동 보정(Calibration)을 통한 하드웨어 자원 최적화 및 운영 효율 극대화

---

## 🕰️ Period
2024.10 ~ 현재

## 👩‍💻 멤버구성
| 성명 | 역할 (Role) | 담당 업무 (Responsibility) |
| :--- | :--- | :--- |
| **안류현** | **Backend** | **Node.js 기반 실시간 서버 설계, MongoDB 구축 및 최적화** |
| 팀원 A | Frontend | React 기반 실시간 관제 대시보드 및 데이터 시각화 구현 |
| 팀원 B | Hardware | 하드웨어 노드 제작 및 센서 데이터 송신 펌웨어 구성 |

---
## ⚙ 기술 스택
### Back-end
<div>
<img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/NodeJS.png?raw=true" width="80">
<img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/MongoDB.png?raw=true" width="80">

</div>

### Infra
<div>
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/AWSEC2.png?raw=true" width="80">

</div>

### Tools
<div>
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Github.png?raw=true" width="80">
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Notion.png?raw=true" width="80">
</div>

<br />

---

## 🗂️ APIs 명세
프로젝트에 적용된 RESTful API 설계 및 상세 명세입니다.
👉🏻 [API 명세서 바로보기](https://github.com/AHNRYUHYUN/GSS/blob/main/APIs.md)

---

## 주요 담당 업무 및 해결 경험 (My Role)

### 1. 실시간 데이터 파이프라인 및 브로드캐스팅 시스템 최적화
사용 기술: Node.js, MQTT, Socket.io, Event Emitter

기술 선택 이유: 대량의 IoT 데이터를 처리할 때 데이터 수신(MQTT)과 전송(Socket) 로직 간의 의존성을 줄이고, 시스템 확장성을 확보하기 위해 이벤트 기반 아키텍처(Event-Driven)를 채택함.

작동 원리

-이벤트 분리: MQTT로 데이터가 유입되면 EventEmitter가 이벤트를 발생시키며, 이를 구독하는 리스너가 독립적으로 후속 로직(DB 저장, 소켓 전송 등)을 처리함.

-동적 채널 할당: 모든 데이터를 전체 전송(Broadcasting)하지 않고, 데이터 내 식별값을 확인하여 관제 대상별 동적 소켓 룸(Room)을 생성 및 분류하여 필요한 클라이언트에만 정밀하게 전송함.

성과
-트래픽 최적화: 불필요한 데이터 전송량을 기존 대비 약 70% 절감함.

-응답 속도: 이벤트 기반 비동기 처리를 통해 데이터 지연 시간(Latency)을 100ms 이내로 안정화함.

### 2. AWS S3 연동 엔진 및 경로 정규화 로직 구현
사용 기술: AWS S3 SDK, Node.js (path.normalize, fs.promises)

기술적 해결
-경로 정규화: 건물/날짜/파일명 등 계층 구조 생성 시 발생하는 중복 슬래시(//)나 OS별 경로 구분자 차이를 path.normalize로 사전 교정하여 S3 접근 정합성을 보장함.

-비동기 최적화: 파일 I/O 작업 시 서버가 멈추지 않도록 fs.promises와 async/await를 활용해 Non-blocking 환경을 구축함.

성과
-무결성 확보: 경로 오지정으로 인한 S3 업로드 에러 발생률 0%를 달성함.

-환경 호환성: Windows 개발 환경과 Linux 배포 환경 간의 경로 호환성 문제를 해결함.

### 3. 서버 측 자동 Calibration 알고리즘 설계 (성능 개선)
문제 해결: MPU-6500 센서의 물리적 설치 오차(약 ±5°)로 인한 데이터 신뢰성 문제를 해결함.

해결 방안: 하드웨어별 수동 보정 대신, 서버 유입 단계에서 초기 샘플 데이터를 분석하여 오프셋(Offset)을 자동으로 산출하고 실시간 데이터에 적용하는 보정 엔진을 설계함.

수치적 성과
-정밀도 향상: 센서 데이터 오차 범위를 ±5.0°에서 ±0.5° 미만으로 감소시켜 정밀도를 90% 개선함.

-운영 효율: 기기 교체 시 소요되는 수동 세팅 시간을 1대당 10분에서 0분으로 단축하여 100% 자동화를 실현함.

-리소스 최적화: 하드웨어 연산 부하를 서버로 이전하여 기기 발열 저하에 기여함.

### 4. 역공학(Reverse Engineering)을 통한 레거시 정상화 및 문서화
상황: 인수인계 문서가 전무하고 소스 코드의 주석이 현지어(우즈베크어)로만 작성되어 로직 파악이 불가능한 상태였음.

수행 내용

-로직 역추적: 데이터 흐름 전수 조사와 단위 테스트를 통해 비즈니스 로직을 역공학 방식으로 분석함.

-자산화: 분석된 로직을 바탕으로 한글 및 영문 표준 가이드라인을 수립하고, API 규격서 및 통합 개발 문서를 제작함.

성과

-신속한 업무 투입: 스스로 파악한 로직을 바탕으로 실무 기능 배포에 참여함.

-유지보수성 향상: 파편화된 정보를 체계화하여 향후 신규 인력 온보딩 기간을 약 50% 이상 단축할 수 있는 기술적 토대를 마련함.

---

## 주요 성과 및 결과 (Performance)
- **데이터 신뢰성 100% 확보**: 서버 측 자동 보정 알고리즘 적용을 통한 정밀 측정 가능
- **서버 안정성 확보**: Cursor 기반 처리로 대용량 데이터 추출 시에도 메모리 점유율 일정 유지 (OOM 방지)
- **운영 효율성 극대화**: 하드웨어 개별 설정 없는 중앙 관리 시스템 구축으로 유지보수 공수 절감

## 💡 Lessons Learned
하드웨어-AI-백엔드가 결합된 복합 시스템에서 백엔드 개발자의 역할이 단순 저장을 넘어 전체 시스템의 응답속도를 조율하고 데이터를 정제하는 컨트롤 타워**임을 배웠습니다. 특히 기술적 선택이 하드웨어 원가 절감과 운영 편의성으로 이어지는 과정을 경험하며 비즈니스 관점의 개발 역량을 강화했습니다.
