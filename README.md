# Nextloop Data Pipeline

---
## 프로젝트 정보 

- **프로젝트 명**: 2024 이어드림스쿨 4기 두왓 기업연계 프로젝트  
- **개발기간**: 2024.10.15. ~ 2024.11.22.
---
  
## NextLoop팀 소개 

![image](https://github.com/user-attachments/assets/734f6e3c-0487-4727-9635-38d13c266c37)


### 팀 이름의 의미
- **끊임없는 발전**  
   - "Next"는 항상 다음 단계로 나아가는 것을 뜻함, 개발 팀이 계속해서 더 나은 솔루션과 기술을 탐구하고 도전한다는 의미를 담고 있음
     
- **순환적 개선**  
   - "Loop"는 프로그래밍에서 반복을 뜻함, 이는 코드나 제품을 지속적으로 개선하고 최적화하는 개발 과정을 상징함.
     
- **미래 지향성**  
   - 변화와 발전을 멈추지 않고, 항상 다음 단계를 생각하고 준비하는 미래 지향적인 팀이라는 이미지를 전달.

---

## 📊 Repository 방문 횟수 

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fimella0707%2Ftest_20240411&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)


---
## Stacks

- **Environment**: ![VS Code](https://img.shields.io/badge/Visual%20Studio%20Code-blue?logo=visual-studio-code&logoColor=white) ![Git](https://img.shields.io/badge/Git-orange?logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-black?logo=github&logoColor=white)
- **Development**: ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) ![Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?logo=apache-airflow&logoColor=white) ![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?logo=apache-spark&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white) ![MLflow](https://img.shields.io/badge/MLflow-0194E2?logo=mlflow&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white) ![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)



- **Communication**: ![Slack](https://img.shields.io/badge/Slack-4A154B?logo=slack&logoColor=white) ![Notion](https://img.shields.io/badge/Notion-000000?logo=notion&logoColor=white)
 

---

## 주요 기능 

- **데이터 파이프라인 구축**
   - 제공받은 Dowhat 데이터를 GCS에 적재
   - 주 단위로 Airflow 배치 태스크를 통해 데이터를 인입하는 데이터 파이프라인 구현

- **MLOps 파이프라인 구축**
   - 제공받은 Dowhat 데이터를 전처리하여 간단한 추천 모델 학습
   - FastAPI를 활용해 모델 서빙 구현
 
- **모니터링 시스템 구축**
   - Prometheus, Grafana를 통해 시스템 성능 모니터링 및 slack 알람
   - cAdvisor, prometheus Fastapi instrumentator 사용해 메트릭 정보 수집
     

---



## 아키텍처


![dowhat-pileline drawio](https://github.com/user-attachments/assets/51e2365e-6fff-4f42-91b8-5bd35ccd61a1)

- 두왓의 데이터 양이 현재는 적기 때문에 로컬에서 스파크로 처리하고, 추후 데이터 규모가 많아질 경우를 대비해서 스파크 클러스터를 구축해 놓았음.




![image](https://github.com/user-attachments/assets/8da81757-4720-4548-bd5f-f1b66901de49)

![image](https://github.com/user-attachments/assets/15ea07f8-c0c0-4b92-95b2-355b674bc189)

---

