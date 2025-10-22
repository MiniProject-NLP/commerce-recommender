# commerce-recommender
"AI Shopping Concierge" — an intelligent stylist that turns your one-line prompt into a Reels-style shopping experience.

# 🛍️ AI 쇼핑 컨시어지 (AI Shopping Concierge)

NLP와 의미 검색(Semantic Search)을 활용한 개인 맞춤형 상품 추천 데모

![Project Banner Image] ---

## 1. 🚀 프로젝트 개요

* **프로젝트명:** AI 쇼핑 컨시어지
* **개발 기간:** 2025.10.22 ~ 2025.10.24 (3일 미니 프로젝트)
* **핵심 기능:** 사용자의 자연어 쿼리(한국어)를 AI가 '의미'로 이해하고, 실제 구매자들의 '영어 리뷰' 텍스트를 분석하여 최적의 상품을 추천하는 시맨틱 검색 데모 서비스입니다.

---

## 2. ✨ 주요 기능

1.  **다국어 의미 검색 (Cross-lingual Search)**
    * 사용자가 "귀여운 봄 원피스"처럼 한국어로 검색어를 입력합니다.
    * AI가 이 쿼리를 영어("cute spring dress")로 자동 번역합니다.
2.  **리뷰 기반 추천 (Review-based Recommendation)**
    * 단순 상품명이 아닌, 실제 구매자가 작성한 영어 리뷰 텍스트(e.g., "This dress is so **cute** and perfect for **spring**!")와의 의미적 유사도를 계산하여 상품을 추천합니다.
3.  **'이유 있는 추천' (Explainable Recommendation)**
    * AI가 왜 이 상품을 추천했는지, 가장 유사도가 높게 매칭된 '실제 리뷰 텍스트'를 근거로 함께 제시합니다.
4.  **품목(Class) 필터링**
    * 사용자 쿼리에서 "원피스(dress)", "치마(skirt)" 등의 핵심 품목 키워드를 감지하여 1차 필터링을 수행합니다.
5.  **웹 데모 시연 (Streamlit)**
    * Streamlit을 활용하여 사용자가 직접 쿼리를 입력하고 추천 결과를 실시간으로 확인할 수 있는 인터랙티브 웹 데모를 구현했습니다.

---

## 3. ⚙️ 시스템 아키텍처

본 프로젝트는 **[1단계: Offline 전처리]**와 **[2단계: Online 서비스]**로 구성됩니다.

![System Architecture Diagram] 1.  **[Offline] 데이터 전처리 (Colab)**
    1.  Hugging Face Hub에서 `Censius-AI/ECommerce-Women-Clothing-Reviews` 데이터셋 로드.
    2.  `Review Text`가 비어있는 데이터 등 결측치 정제.
    3.  영어 `sentence-transformers/all-MiniLM-L6-v2` 모델로 2만+개의 리뷰 텍스트를 임베딩.
    4.  결과물(`review_embeddings.npy`, `review_metadata.pkl`)을 저장.
2.  **[Online] Streamlit 서비스 (Local)**
    1.  사용자가 **한국어 쿼리** 입력.
    2.  `Helsinki-NLP/opus-mt-ko-en` 모델로 **영어로 번역**.
    3.  번역된 쿼리를 Offline과 동일한 SBERT 모델로 **임베딩**.
    4.  저장된 `review_embeddings.npy`와 **코사인 유사도(Cosine Similarity)** 계산.
    5.  (중복 `Clothing ID` 제거 로직 포함)
    6.  `metadata.pkl`에서 매칭된 상품의 정보(리뷰, 평점 등)를 가져와 UI에 시각화.

---

## 4. 🛠️ 기술 스택 및 데이터

* **Language:** Python 3.10+
* **Core NLP/ML:** `Hugging Face Transformers`, `Sentence-Transformers`, `PyTorch`
* **Search Model:** `sentence-transformers/all-MiniLM-L6-v2` (English SBERT)
* **Translation Model:** `Helsinki-NLP/opus-mt-ko-en` (Korean-to-English)
* **Data Handling:** `Pandas`, `Numpy`
* **App Server:** `Streamlit`
* **Collaboration:** `Git`, `GitHub (Organization)`
* **Data Source:** `Censius-AI/ECommerce-Women-Clothing-Reviews` (Hugging Face Datasets)

---

## 5. 🖥️ 설치 및 실행 방법

### 1. 프로젝트 복제 (Clone)

```bash
# (본인 Organization의 저장소 주소로 변경)
git clone [https://github.com/YOUR-ORGANIZATION/YOUR-REPOSITORY.git](https://github.com/YOUR-ORGANIZATION/YOUR-REPOSITORY.git)
cd YOUR-REPOSITORY
