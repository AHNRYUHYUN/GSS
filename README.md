<div align="center">



## 📝 소개


 <img width="1893" height="921" alt="image" src="https://github.com/user-attachments/assets/0797b5ef-b189-4157-b580-673022f08002" />
infogssiot.com 사이트에 대한 내용을 제공하는 파일입니다.

## 🛠 기술 스택
<img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/NodeJS.png" width="100"><img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/MongoDB.png" width="100">




<br />



### 화면 구성
 <img width="1893" height="921" alt="image" src="https://github.com/user-attachments/assets/0797b5ef-b189-4157-b580-673022f08002" />



<br />

## 🗂️ APIs
작성한 API는 아래에서 확인할 수 있습니다.

👉🏻 [API 바로보기](/backend/APIs.md)


<br />

## ⚙ 기술 스택
> skills 폴더에 있는 아이콘을 이용할 수 있습니다.
### Back-end
<div>
<img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/NodeJS.png?raw=true" width="80">
<img src="https://github.com/AHNRYUHYUN/AHNRYUHYUN/blob/main/skills/MongoDB.png?raw=true" width="80">

</div>

### Infra
<div>
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/AWSEC2.png?raw=true" width="80">
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/AWSEC2.png?raw=true" width="80">
</div>

### Tools
<div>
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Github.png?raw=true" width="80">
<img src="https://github.com/yewon-Noh/readme-template/blob/main/skills/Notion.png?raw=true" width="80">
</div>

<br />

## 🛠️ 프로젝트 아키텍쳐

<div align="center">

<pre>
┌─────────────── 현장(빌딩) ───────────────┐
│  [각도 노드/도어 노드] ──► [게이트웨이]  │
└───────────────┬─────────────────────────┘
                │ MQTT (ingest)
                ▼
         ┌──────────────────┐
         │  MQTT Broker(*)  │
         └────────┬─────────┘
                  │ subscribe
                  ▼
          ┌──────────────────────┐
          │  Node.js (Express)   │
          │  - Routes/Controllers│
          │  - Services          │
          │  - Socket.IO         │
          └───────┬───────┬──────┘
              save/agg    │ push
                          │
                          ▼
                  ┌──────────────┐
                  │  Web Clients │
                  └──────────────┘
                          │
                          ▼
        ┌─────────────────────────────┐
        │         MongoDB             │
        │     (Models/Schemas)        │
        └─────────────────────────────┘
</pre>

</div>


<br />

## 🤔 기술적 이슈와 해결 과정



<br />


