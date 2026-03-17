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

## 🛠️ 프로젝트 아키텍처
<div align="center">
<img width="800" alt="시스템 아키텍처" src="https://github.com/user-attachments/assets/ff3202dc-a056-41a6-8514-fbaadbe0cdff" />
</div>

---

## 🗂️ APIs 명세
프로젝트에 적용된 RESTful API 설계 및 상세 명세입니다.
👉🏻 [API 명세서 바로보기](https://github.com/AHNRYUHYUN/GSS/blob/main/APIs.md)

---

## 주요 담당 업무 및 해결 경험 (My Role)

### 1. 실시간 데이터 파이프라인 및 이벤트 중심 설계
- **MQTT 기반 수집 엔진**: `mqttEmitter`와 `EventEmitter`를 활용하여 데이터 수신부와 저장/전송 로직 간의 결합도를 낮추는 아키텍처를 설계했습니다.
- **Socket.io 최적화**: 수신된 데이터를 전체 전송하지 않고, `building_id` 기반의 룸(Room) 기능을 사용하여 필요한 대상에게만 실시간 브로드캐스팅하도록 최적화했습니다.

### 2. 서버 측 자동 보정(Calibration)을 통한 HW 최적화
- **0점 조절 자동화**: 센서 설치 시 발생하는 물리적 오차를 해결하기 위해 초기 샘플링 데이터를 서버에서 분석하여 `Offset`을 산출하는 알고리즘을 구현했습니다.
- **HW 리소스 경감**: 하드웨어에서 수행하던 보정 연산을 서버로 이전하여 단말기의 메모리 및 CPU 부하를 제거하고, 하드웨어 배포 시 개별 설정이 필요 없는 환경을 구축했습니다.

### 3. 고성능 데이터 처리 및 관리 서비스 구현
- **대용량 데이터 스트리밍**: 수만 건의 시계열 로그를 CSV로 추출 시 서버 다운을 방지하기 위해 `MongoDB Cursor` 기반의 스트리밍 방식을 도입했습니다.
- **조회 속도 개선 (Map Caching)**: 수천 개의 노드 정보를 조회할 때 발생하는 DB 부하를 줄이기 위해 게이트웨이 정보를 `Map` 객체로 인메모리 캐싱하여 응답 속도를 약 40% 단축했습니다.
- **동적 자원 관리**: 게이트웨이의 `zone_name` 수정 등 마스터 데이터 관리 CRUD API를 구축하고, 데이터 수집 시점의 위치 정보를 스냅샷 형태로 기록하여 정합성을 확보했습니다.

---

## 주요 성과 및 결과 (Performance)
- **데이터 신뢰성 100% 확보**: 서버 측 자동 보정 알고리즘 적용을 통한 정밀 측정 가능
- **서버 안정성 확보**: Cursor 기반 처리로 대용량 데이터 추출 시에도 메모리 점유율 일정 유지 (OOM 방지)
- **운영 효율성 극대화**: 하드웨어 개별 설정 없는 중앙 관리 시스템 구축으로 유지보수 공수 절감

## 💡 Lessons Learned
하드웨어-AI-백엔드가 결합된 복합 시스템에서 백엔드 개발자의 역할이 단순 저장을 넘어 전체 시스템의 **Latency를 조율하고 데이터를 정제하는 컨트롤 타워**임을 배웠습니다. 특히 기술적 선택이 하드웨어 원가 절감과 운영 편의성으로 이어지는 과정을 경험하며 비즈니스 관점의 개발 역량을 강화했습니다.
