<div align="center">

# 🏭 비계 및 시설물 안전 관리를 위한 실시간 모니터링 시스템: GSS

### [infogssiot.com](https://infogssiot.com) 운영 및 기술 지원

<img width="800" alt="GSS 메인 화면" src="https://github.com/user-attachments/assets/0797b5ef-b189-4157-b580-673022f08002" />

</div>

---

## 📝 프로젝트 소개
건설 현장 내 **비계(가설 구조물)의 기울어짐 및 붕괴 징후를 실시간으로 포착**하여 인명 사고를 예방하는 IoT 관제 시스템입니다. 센서 설치 시 발생하는 물리적 오차를 백엔드 로직으로 보정하여 데이터 신뢰성을 확보하고, 대규모 시계열 데이터를 안정적으로 처리하는 데 집중했습니다.

## 🛠 기술 스택

### Back-end & Database
<img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/NodeJS.png?raw=true" width="80"> <img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/MongoDB.png?raw=true" width="80">

### Infra & Tools
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/AWSEC2.png?raw=true" width="80"> <img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Github.png?raw=true" width="80"> <img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Notion.png?raw=true" width="80">

---

## ⚙️ 프로젝트 아키텍처
<div align="center">
<img width="700" alt="시스템 아키텍처" src="https://github.com/user-attachments/assets/ff3202dc-a056-41a6-8514-fbaadbe0cdff" />
</div>

---

## 🗂️ APIs
설계 및 구현된 상세 API 명세는 아래 링크에서 확인할 수 있습니다.
👉🏻 [API 명세서 바로보기](https://github.com/AHNRYUHYUN/GSS/blob/main/APIs.md)

---

## 📌 주요 역할 및 성과

### 1. 실시간 데이터 파이프라인 엔진 구축
- **MQTT & Socket.io**: MQTT 프로토콜로 수신되는 센서 데이터를 `EventEmitter`를 통해 처리 로직과 분리하여 결합도를 낮췄습니다.
- **동적 브로드캐스팅**: 건물/구역별 ID를 기준으로 소켓 토픽을 분류하여 실시간 데이터를 효율적으로 전송하도록 설계했습니다.

### 2. 서버 측 중앙 집중형 보정(Calibration) 로직
- **문제 해결**: 센서 설치 환경에 따른 물리적 기울기 오차를 해결하기 위해 초기 샘플링 기반의 자동 보정 알고리즘을 구현했습니다.
- **성과**: 하드웨어마다 개별 코드를 주입할 필요 없이 서버에서 0점을 조절함으로써 **단말기 자원 최적화 및 운영 효율성 100% 향상**을 달성했습니다.

### 3. 대용량 시계열 데이터 처리 최적화
- **스트리밍 추출**: 수만 건의 데이터를 CSV로 추출 시 발생하는 메모리 부하를 방지하기 위해 **MongoDB Cursor 기반 스트리밍** 방식을 도입했습니다.
- **데이터 무결성**: 수집 시점의 위치 정보(Zone, Position)를 함께 기록하는 스냅샷 아키텍처를 적용하여 데이터 정합성을 확보했습니다.

---

## 🎯 주요 성과 지표
| 지표 (Metric) | 결과 (Result) | 비고 |
| :--- | :--- | :--- |
| **데이터 정밀도** | **100% 확보** | 자동 보정 알고리즘 적용 결과 |
| **메모리 안정성** | **OOM 발생 0건** | Cursor 기반 스트리밍 처리 도입 |
| **조회 응답 속도** | **약 40% 개선** | 인메모리 Map 캐싱 및 DB 인덱싱 최적화 |

---

## 💡 Lessons Learned
백엔드 개발자가 단순히 데이터만 저장하는 것이 아니라, 하드웨어의 자원 한계를 이해하고 시스템 전체의 지연(Latency)을 조율하는 **컨트롤 타워** 역할을 해야 함을 체득했습니다. 특히 SW 로직으로 HW 공정 효율을 높였던 경험은 기술적 선택이 비즈니스 가치로 직결됨을 깨닫는 계기가 되었습니다.
