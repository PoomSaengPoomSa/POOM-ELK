# 📊 POOM-ELK

> **POOM** — PB(Private Banker) 업무 지원 AI Assistant 플랫폼의 로그 수집 및 모니터링 스택

---

## 📌 개요

POOM 플랫폼의 ELK Stack 기반 로그 수집 및 모니터링 레포지토리입니다.
Elasticsearch, Logstash, Kibana를 Docker Compose로 구성하여
백엔드·AI 서버의 로그를 수집하고 시각화합니다.
AWS S3 스냅샷 연동을 통해 Elasticsearch 데이터를 백업합니다.

---

## 🗂 프로젝트 구조
POOM-ELK/

├── config/

│   └── logstash/

│       └── pipeline/       # Logstash 파이프라인 설정

├── .github/workflows/      # GitHub Actions CI/CD

├── docker-compose-elk.yml  # ELK 서비스 구성

└── README.md

---

## ⚙️ 기술 스택

| 분류 | 기술 | 버전 |
|---|---|---|
| **검색/저장** | Elasticsearch | 9.3.0 |
| **시각화** | Kibana | 9.3.0 |
| **수집/파싱** | Logstash | 9.3.0 |
| **스토리지 백업** | AWS S3 (repository-s3 플러그인) | - |
| **인프라** | Docker Compose, `poom-network` | - |

---

## 🧩 서비스 구성

`docker-compose-elk.yml` 기준으로 아래 서비스가 실행됩니다.

| 서비스 | 역할 | 포트 |
|---|---|---|
| `elasticsearch` | 로그 데이터 저장 및 검색 | 9200 |
| `kibana` | 로그 시각화 대시보드 | 5601 |
| `logstash` | 로그 수집 및 파싱 파이프라인 | 5044 |

> Elasticsearch는 `repository-s3` 플러그인을 자동 설치하여 AWS S3 스냅샷 백업을 지원합니다.

---

## 🚀 실행 방법

```bash
# 1. 환경변수 설정
cp .env.example .env

# 2. 서비스 실행
docker compose -f docker-compose-elk.yml up -d

# 3. Kibana UI 접속
# http://localhost:5601

# 4. Elasticsearch 상태 확인
curl http://localhost:9200
```

---

## 🔗 연관 레포지토리

| 레포 | 역할 |
|---|---|
| [POOM-BACK](https://github.com/PoomSaengPoomSa/POOM-BACK) | FastAPI 백엔드 서버 (로그 전송) |
| [POOM-AI](https://github.com/PoomSaengPoomSa/POOM-AI) | AI 서버 (로그 전송) |
| [POOM-AIRFLOW](https://github.com/PoomSaengPoomSa/POOM-AIRFLOW) | MLOps 파이프라인 |
| [POOM-MLFLOW](https://github.com/PoomSaengPoomSa/POOM-MLFLOW) | 모델 실험 관리 |

---

> 우리FISA AI 엔지니어링 1팀 | POOM 프로젝트
