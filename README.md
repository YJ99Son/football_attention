# 영화 리뷰 크로스 어텐션 시각화 대시보드

## 프로젝트 개요

이 프로젝트는 영화 리뷰와 영화 정보/설명 간의 크로스 어텐션(cross-attention)을 시각화하는 대시보드를 제공합니다. 사전훈련된 한국어 트랜스포머 모델(KLUE-RoBERTa)을 활용하여 리뷰 텍스트가 영화 정보 및 줄거리의 어떤 부분에 주의를 기울이는지 분석할 수 있습니다.

## 주요 기능

1. **리뷰-영화 정보 어텐션 히트맵**: 리뷰(y축)가 영화 정보(x축)의 어떤 부분에 주목하는지 시각화
2. **리뷰-영화 줄거리 어텐션 히트맵**: 리뷰(y축)가 영화 줄거리/설명(x축)의 어떤 부분에 주목하는지 시각화
3. **집계 어텐션 시각화**: 모든 리뷰의 어텐션을 합쳐서 정보/줄거리의 어느 부분이 가장 주목받는지 분석

## 설치 방법

### 필수 요구사항

- Python 3.9 이상
- CUDA 지원 GPU (권장, CPU에서도 실행 가능)

### 설치 단계

1. 저장소 클론
   ```bash
   git clone https://github.com/yourusername/movie-attention-dashboard.git
   cd movie-attention-dashboard
   ```

2. 가상환경 생성 (선택사항)
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   venv\Scripts\activate     # Windows
   ```

3. 필요 패키지 설치
   ```bash
   pip install -r requirements.txt
   ```

4. KoNLPy 설치를 위한 추가 요구사항
   - Java 8 이상 설치 필요
   - Mac: `brew install jpype`
   - Ubuntu: `sudo apt-get install openjdk-8-jdk python3-dev`
   - Windows: JDK 설치 후 환경변수 설정

## 사용 방법

1. 애플리케이션 실행
   ```bash
   streamlit run cross_attention_dashboard.py
   ```

2. 웹 브라우저에서 열리는 대시보드 사용
   - 영화 ID 입력
   - "데이터 로드" 버튼 클릭
   - 표시된 리뷰 중 하나 선택
   - "어텐션 시각화" 버튼 클릭하여 히트맵 확인
   - 여러 리뷰에 대해 반복 후 "모든 리뷰 어텐션 집계" 버튼 클릭

## 데이터 구조

프로젝트는 다음과 같은 데이터 파일 구조를 사용합니다:

- `movie_data/`: 영화 정보가 저장된 디렉토리
  - `movie_summary.json`: 영화 ID별 줄거리 정보
  - `{movie_id}_info.json`: 영화 정보 (제목, 장르, 감독, 배우 등)
  - `{movie_id}_reviews.json`: 해당 영화의 리뷰 목록

## 모델 설명

이 프로젝트는 KLUE-RoBERTa-base 모델을 사용하여 어텐션 분석을 수행합니다. 이 모델은 한국어 자연어 처리에 최적화된 사전훈련된 트랜스포머 모델로, Hugging Face 라이브러리를 통해 로드됩니다.

## 문제 해결

- **Mecab 로드 오류**: KoNLPy/Mecab 설치 문제 발생 시 다음과 같이 확인
  ```bash
  pip install konlpy
  pip install jpype1
  ```
  필요 시 Java 환경 변수를 올바르게 설정했는지 확인

- **GPU 메모리 부족**: `compute_cross_attention` 함수에서 batch_size와 max_length 값 조정

## 향후 개발 계획

- 다양한 사전훈련 모델 옵션 제공
- 어텐션 헤드/레이어 선택 기능 추가
- 감성 분석과 어텐션 결과 통합
- 대시보드 UI/UX 개선

## 기여 방법

1. 이슈 등록 또는 풀 리퀘스트 생성
2. 코드 개선 및 버그 수정 제안
3. 새로운 기능 아이디어 공유

## 라이센스

이 프로젝트는 MIT 라이센스를 따릅니다. 자세한 내용은 LICENSE 파일을 참조하세요. 