# Flask Docker CI/CD 프로젝트

이 프로젝트는 Flask 애플리케이션을 Docker로 컨테이너화하고 GitHub Actions를 통해 CI/CD 파이프라인을 구축한 예제입니다.

## 프로젝트 구조

```
DevOps/
├── app.py              # Flask 애플리케이션
├── requirements.txt    # Python 의존성
├── Dockerfile         # Docker 이미지 빌드 설정
├── test_app.py        # 테스트 파일
├── .github/workflows/ # CI/CD 워크플로우
│   └── docker-ci.yml  # Docker CI/CD 파이프라인
└── .dockerignore      # Docker 빌드 시 제외할 파일들
```

## 로컬 실행

### Python으로 직접 실행
```bash
pip install -r requirements.txt
python app.py
```

### Docker로 실행
```bash
# 이미지 빌드
docker build -t flask-app .

# 컨테이너 실행
docker run -p 5000:5000 flask-app
```

## CI/CD 파이프라인

### 워크플로우 설명

1. **test**: Python 테스트 실행
2. **docker-build**: Docker 이미지 빌드 및 컨테이너 테스트
3. **docker-push**: Docker Hub에 이미지 푸시 (main 브랜치에서만)

### 트리거 조건
- `main` 또는 `develop` 브랜치에 push
- `main` 브랜치로 pull request

### Docker Hub 푸시 설정

Docker Hub에 이미지를 푸시하려면 GitHub Secrets에 다음을 설정해야 합니다:

1. `DOCKER_USERNAME`: Docker Hub 사용자명
2. `DOCKER_PASSWORD`: Docker Hub 액세스 토큰

### Secrets 설정 방법

1. GitHub 저장소 → Settings → Secrets and variables → Actions
2. "New repository secret" 클릭
3. 위의 두 개의 secret 추가

## 테스트

```bash
pytest
```

애플리케이션은 `http://localhost:5000`에서 "Hello, Flask!" 메시지를 확인할 수 있습니다.