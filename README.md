# Project1 : 서울시 어린이 환경지수 순위       

<img src="https://user-images.githubusercontent.com/115753833/227953568-62c36abc-9734-4800-a51f-646739434952.png" width="500" >

## 1. 주제선정 배경

### 1) 문제점 및 시사점
- 출산율이 점점 줄어들고 있으며, 그 원인은 맞벌이 가정이 점점 많아지는 추세, 육아 환경이 불안정함 등 복합적임
- 육아환경 관련하여 대안 정책이 늘어나고 있음

<img src="https://user-images.githubusercontent.com/115753833/227958226-6166344d-b6b0-4566-8537-71f469d8463e.png" width="700">
<br>

### 2) 서울시 선정이유
- 면적대비 서울시의 아동인구가 가장 많음
<br>

### 3) 육아환경 탐색
- 범죄로부터 보호받는 환경인가?
- 교통사고 예방 환경이 잘 구성되어 있는가?
- 아이 돌봄 보조시설과 병원이 얼마나 있는가?
<br>

## 2. 전체 프로세스
<img src="https://user-images.githubusercontent.com/115753833/227967961-ca887358-3f66-416b-9604-0490f47a4a71.png" width="700">

### 1) 각 항목선정 : "교통 / 범죄 / 주변시설"
<br>

### 2) 필요 데이터 수집(자치구별)
  - **교통**: 도로 면적, 어린이 교통사고 수, 교통사고 수, 단속카메라 수, 어린이 보호구역 수
  - **범죄**: 대지 면적, 5대범죄 수, 방범 cctv 수, 유흥주점 수
  - **주변시설**: 어린이 인구 수, 돌봄센터 수, 병원 수
<br>

### 3) 데이터 전처리(라이브러리, 오픈 API활용)
- 결측치, 이상치 제거 및 데이터 셋 구축
- 주소 및 위도,경도 변환
- 지도 시각화
- 각 항목 시각화 <br>
<img src="https://user-images.githubusercontent.com/115753833/227980162-e0cec9ef-a281-44af-a66b-7ae017ad334c.png" width="700">
<br>

### 4) 데이터 분석을 통한 각 항목의 점수 계산

**`(상관계수) X (실루엣 계수) X (각 핵심지표의 자치구별 비율)`**<br>

- **Scikit-Learn(Linear Regression)**: 회귀 분석 + **상관도(Corr)**
    - **상관계수는 가중치로 작용**
    - 범죄 데이터: 자치구 별 평균 범죄 건수 대비 CCTV, 유흥 주점
    - 교통 데이터: 자치구 별 평균 교통사고 건수 대비 단속 카메라, 어린이 보호 구역
    - 시설 데이터: 자치구 별 어린이 인구 대비 병원, 돌봄 센터

- **Scikit-Learn(K-means): 군집화와 실루엣계수**
  - 엘보우 기법을 통한 최적 군집 개수로 군집화
  - 실루엣계수와 중심좌표 획득
  - 중심 좌표의 주소를 통해 해당 자치구 판별
  - 실루엣 계수를 통한 점수 계산
<br>

### 5) 환경 지수 식
<img src="https://user-images.githubusercontent.com/115753833/227988040-e025da65-4205-4cdc-9772-d96d4092e5e8.png" width="700">
<br>

## 3. 데이터 시각화
### 1) 상관계수 데이터
<img src="https://user-images.githubusercontent.com/115753833/227988580-012f734f-453c-49b8-9812-ab50c2193b84.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227988800-fbcf5b26-5ead-4b42-8735-0ac21dd85a46.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227989158-622ce843-5060-4be2-a760-04e0fd3c23ec.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227989260-9de01066-882d-4925-ae5d-f00af2a58764.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227990235-d0229f51-6de6-4d35-954d-555b739ac68a.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227990673-b506e073-db48-4be8-abf6-4ee360e3c742.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227990860-5526e29e-29cd-4247-871d-f40178513160.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227990975-93955e6e-7906-47fe-9f5f-b80307e6557e.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227991906-d72dabbc-5271-4a7a-b58b-234091ce49b7.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227991970-745e958f-b32f-4b8f-ad06-cdb93d2d5ad1.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227992108-569c01d0-a261-4229-9b93-7bf11218bdeb.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227992186-7876a813-51d3-4718-beea-2b291605384f.png" width="50%">
<br><br>

### 2) 클러스터링
<img src="https://user-images.githubusercontent.com/115753833/227993027-42726a05-820c-4251-ae03-552f041da9f3.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227993837-2afa3edc-0024-41d5-bb43-dbf00b0bb859.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227994355-3c2bb83b-c299-4bdc-aa49-75c141201c2b.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227994451-c5fb64ad-cc29-41b0-b685-3f65671b59aa.png" width="50%">
<br><br>
<img src="https://user-images.githubusercontent.com/115753833/227994774-5e21a8af-cca6-468d-8cb1-e5f7c1027d81.png" width="50%"><img src="https://user-images.githubusercontent.com/115753833/227994986-031463d2-b4da-45da-a8a9-8090e8b4d2e1.png" width="50%">
<br><br>

## 4. 결과
<img src="https://user-images.githubusercontent.com/115753833/227995470-8daff833-b08c-4519-aa8e-46fa92300b91.png" width="700">
<br>

## 5. 기대효과 및 한계점
### 1) 기대효과
- 자치구별 항목간 비교를 통해 부족하거나 필요한 정책 제안 가능
- 아이 및 부모에게 좋은 환경 추천 및 제공 가능
- 서울시를 표본으로 다른 지역의 어린이 환경 조성 시 참고 가능
### 2) 한계점
- 항목의 군집 중심점이 있는 자치구의 경계에 있는 다른 자치구에 대한 값은 반영이 어려움
- 서울시에 자치구가 25개이므로 구별 상관도 분석하는데 있어 비교 데이터가 너무 작음
- 환경 순위를 매기는데 있어서 현재 분석 한 것 이외에 영향을 끼치는 항목이 많음



