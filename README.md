# cohort_RFM
## 데이터 출처
데이콘 DACON

이커머스 고객 세분화 분석 아이디어 경진대회

RFM, Cohort, 지역별, 성별 고객 군집 분석 코드입니다.

데이터 출처:
https://dacon.io/competitions/official/236222/overview/description

## 고객 세분화 분석 결과
#### 1. RFM 분석
- RFM 분석을 위하여 백분위수를 기준으로 Recency, Frequency, Monetary를 각각 4개의 구간으로 구분
- 각 구간별 zscore 값을 확인하며 각 구간 이상치 최소화
- KMeans를 통해 "미관심 고객", "VIP 고객", "신규 고객", "수면 고객"으로 군집화 (값의 크기 "미관심 고객" >
"VIP 고객" > "신규 고객" > "수면 고객" 순서)
- 월별 VIP 고객의 수와 월별 마케팅 비용을 시각화하여 분석한 결과, 둘 간의 유의미한 상관관계 부재
  
#### 2. Cohort 분석
- 월 단위로 코호트 군집 형성한 뒤, 재방문률의 변화, 거래금액의 변화 추이 관측
- pearson 상관분석을 통해 온라인 마케팅 비용과 오프라인 마케팅 비용이 이들과의 상관관계가 약함 확인
  
#### 3. 지역별 분석
- 지역별 [고객 숫자], [거래 횟수], [거래 금액], [고객당 평균 거래금액 평균], [1건당 평균 거래금액], [고객당 평
균 거래 수횟], [제품별 거래금액], [성별 구성 및 각 성별의 제품별 거래금액] 분석

• California
- [고객 숫자], [거래 횟수], [소비 금액] : 높다.
- [고객당 평균 평균 거래금액], [1건당 평균 거래금액], [고객당 평균 거래 횟수] : 보통
  
• Chicago
- [고객 숫자], [거래 횟수], [소비 금액], [고객당 평균 평균 거래금액], [고객당 평균 거래 횟수] : 높다.
- [1건당 평균 거래금액] : 낮다
  
• New Jersey
- [1건당 평균 거래금액] : 높다
- [고객 숫자] [거래 횟수], [소비 금액], [고객당 평균 거래금액], [고객당 평균 거래 횟수] : 낮다.

• New York
- [고객 숫자], [거래 횟수], [소비 금액] : 보통
- [고객당 평균 거래금액], [고객당 평균 거래 횟수], [1건당 평균 거래금액] : 낮다.
  
• "Washington DC"
- [고객당 평균 거래금액], [1건당 평균 거래금액], [고객당 평균 거래 횟수] : 높다
- [고객 숫자], [거래 횟수], [소비 금액] : 낮다

#### 4. 장바구니 분석
- 규칙 0: 제품 0917을 구매했을 때, 제품 0915를 함께 구매할 확률이 약 72.75% 이 규칙의 lift 값이 41.15로 매우 높으므로, 두 제품 간의 매우 강한 양의 연관성이 있음
- 규칙 1: 제품 0915를 구매했을 때, 제품 0917을 함께 구매할 확률이 약 60.27% lift 값이 규칙 0과 동일하게 높으므로, 이 두 제품은 서로 매우 강한 양의 연관성
- 규칙 2, 3: 제품 0976을 구매했을 때, 제품 0983을 함께 구매할 확률은 약 21.45%, 그리고 그 반대의 경우도 비슷한 확률. 이 규칙들의 lift 값은 1.61로, 두 제품이 서로 구매될 확률이 독립적인 경우보다 약간 더 높음

## 솔루션 제안

#### 1. 지역별 전략
- 충성 고객 대상 프로모션 행사 지역 : "California", "Chicago", 'Washington DC'
- 신규 고객 대상 프로모션 행사 지역 : "Washington DC", "New Jersy“
1. 지역별 고객이 많은 California, Chicago, Newyork에 전광판 등 오프라인 마케팅 집중하여 고객에게
쇼핑몰을 노출시키는 전략 활용
2. 뉴저지나 워싱턴의 경우 오프라인 마케팅 보다는 배너 등의 온라인 마케팅을 통해 고객 수를 늘리는
것에 집중
- 제품 카테고리
- Apparel, Nest-USA, Office, Nest에 대한 거래금액이 크므로 이를 고려할 필요 있음.
※ New Jersey 남성의 경우 다른 지역과 달리 Office에 대한 선호도가 Nest보다 높음.

#### 2. 장바구니 분석 기반 전략
- 상품을 배치하거나 프로모션을 기획할 때 관련성 높게 나온 제품들을 함께 추천하거나 패키지로 묶어 판
매하는 전략.
- LifeStyle 카테고리에서 함께 구매한 상품의 연관성이 높은 것으로 나타남
- LifeStyle 카테고리에서 연관 상품을 묶어서 추천하는 전략 추진
- (예를 들어, 제품 0917과 0915는 함께 묶어 할인을 제공하거나, 함께 구매를 유도하는 마케팅 캠페인을
진행)

#### 3. 선호도 기반의 전략
VIP 군집의 성별에 따른 프로모션 전략
- 남성의 경우 'Bottles', 'Fun', 'Headgear' 상품을 위주로 프로모션 진행
- 여성의 경우 'Google', 'More bags', 'Gift Cards' 위주로 프로모션 진행
- 성별에 관계 없이 'Nest', 'Notebooks & Journals'의 프로모션은 지속적으로 진행
- 
#### 4. 월 별 구입 내역에 따른 프로모션 전략
- 지속적으로 'Apparels', 'Nest', 'Office'는 상위권임 -> 지속적인 프로모션 진행
- 다만, 겨울에 'Nest' 수요가 높아지는 것을 봐서 겨울 시즌에 Nest 프로모션 진행 추진
- 학기 시작 전인 7,8월에 'notebook & journal' 수요 증가 -> 신학기 프로모션 진행
