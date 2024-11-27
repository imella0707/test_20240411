# Dowhat 기업 연계 프로젝트 

---
## 🏨 프로젝트 정보 

- **프로젝트 명**: 호텔 운영 효율화 및 AI CRM 파이프라인 구축
- **소속 기관**: 2024 이어드림스쿨 4기  
- **개발 기간**: 2024.10.15. ~ 2024.11.22.
---
  
## 👫 NextLoop팀 소개 

![image](https://github.com/user-attachments/assets/734f6e3c-0487-4727-9635-38d13c266c37)

- **끊임없는 발전**  
   - 'Next'는 항상 다음 단계로 나아가는 것을 뜻함, 이는 계속해서 더 나은 솔루션과 기술을 탐구하고 도전한다는 의미를 담고 있음
     
- **순환적 개선**  
   - 'Loop'는 프로그래밍에서 반복을 뜻함, 이는 코드나 제품을 지속적으로 개선하고 최적화하는 개발 과정을 상징함.
     
- **미래 지향성**  
   - 변화와 발전을 멈추지 않고, 항상 다음 단계를 생각하고 준비하는 미래 지향적인 팀이라는 이미지를 전달.

---

## 🔔 NextLoop Repository 방문 횟수 

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fminhyeok0328%2Fnext-loop&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)



---
## 🛠 Stacks

- **Environment**: ![VS Code](https://img.shields.io/badge/Visual%20Studio%20Code-blue?logo=visual-studio-code&logoColor=white) ![Git](https://img.shields.io/badge/Git-orange?logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-black?logo=github&logoColor=white)
- **Development**: ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) ![Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?logo=apache-airflow&logoColor=white) ![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?logo=apache-spark&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white) ![MLflow](https://img.shields.io/badge/MLflow-0194E2?logo=mlflow&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white) ![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)



- **Communication**: ![Slack](https://img.shields.io/badge/Slack-4A154B?logo=slack&logoColor=white) ![Notion](https://img.shields.io/badge/Notion-000000?logo=notion&logoColor=white)
 

---

## 🔅 주요 기능 

- **데이터 파이프라인 구축**
   - 제공받은 Dowhat 데이터를 GCS에 적재
   - 주 단위로 Airflow 배치 태스크를 통해 데이터를 인입하는 데이터 파이프라인 구현
   - 현재는 로컬에서 Spark를 사용, 추후 데이터 규모가 많아질 경우를 대비해서 Spark cluster 구축해 둠

- **MLOps level 1 파이프라인 구축**
   - 제공받은 Dowhat 데이터를 전처리하여 간단한 추천 모델 학습
   - mlflow를 통해 모델 실험 관리(Tracking), 모델 레지스트리 기능 사용
   - FastAPI를 통해 모델 서빙 구현
   - Github action, Nginx를 활용한 Blue-Green 무중단 배포 방식을 통해 CI/CD 구현
 
- **모니터링 시스템 구축**
   - Prometheus, Grafana를 통해 시스템 성능 모니터링 및 slack 알람 연동
   - cAdvisor, prometheus Fastapi instrumentator를 통해 메트릭 정보 수집
     

---
## 🖥️ 개발 환경 설정

- **GCP 인스턴스 사용**
  - 리전: 서울 (asia-northeast3-a) 
  - Image : Ubuntu 24.04.1 LTS(x86/64) 단, MLFlow 등 모델 학습 인스턴스는 Deep Learning VM with CUDA 12.3 M125
  - Instance Type :  E2.standard-4 (vcpu 4, ram 16gb)
  - Storage : 최소 100GB (균형 있는 영구 디스크)

- **기타 주의사항**
  - 각 인스턴스 하나에 하나의 서비스 만을 띄워야 함. 
    다만 **Prometheus, Grafana**같이 부하가 별로 없는 서비스의 경우 같은 인스턴스에 배포하여도 상관없음.
  - 인스턴스 이름은 **dowhat-{platform}-{number}** 
    ex) dowhat-monitoring-1   



---


## 🖊 아키텍처
- **전체 아키텍처** 
![image](https://github.com/user-attachments/assets/3dbbe9fb-90c4-4033-ab9b-769772fb8c1a)



- **파이프라인 상세 구조**
데이터 파이프라인은 4개의 주요 계층으로 구성되어 있습니다:


![image](https://github.com/user-attachments/assets/8da81757-4720-4548-bd5f-f1b66901de49)






### 1. Storage Layer (입력 저장소 계층)
#### 데이터 소스:
- CSV 파일 업로드를 통해 데이터를 입력받음.
- GCS(Google Cloud Storage)에서 직접 데이터를 저장하거나 가져오는 것도 가능.

#### 역할:
- 원시 데이터를 **Cloud Storage Bucket**에 저장.



### 2. Processing Layer (데이터 처리 계층)
- **Apache Spark**를 사용하여 3단계 데이터 처리 수행.

#### 3단계 데이터 처리:
1) **데이터 검증 (Data Validation)**:
   - 데이터를 검증하고 품질을 확인.
2) **변환 (Transformation)**:
   - 호텔 도메인에 기반한 feature 생성 및 데이터 전처리.
3) **포맷 변환 (Format Convert)**:
   - 데이터를 효율적으로 저장 및 활용할 수 있도록 **Parquet 포맷**으로 변환.


## 3. Storage Layer (출력 저장소 계층)
- 최종 처리된 데이터를 feature store인 **Cloud Storage Bucket**에 저장.
- Feature Store인 feast를 사용하지 않은 이유는 인프라 구축 초기단계이기 때문에 최대한 간소화하기로 결정.  

## 4. Consumption Layer (소비 계층)
- 최종 데이터는 **데이터 사이언티스트**들이 Feature Store에서 데이터를 가져와 분석 및 모델 학습 등에 활용.


- **mlops 파이프라인 상세 구조** 
![image](https://github.com/user-attachments/assets/15ea07f8-c0c0-4b92-95b2-355b674bc189)

---

