# 210729) Lesson 2 - meeting record

### 👾 **보윤님 발표**
> 간단한 메타정보를 이용한 책 추천 시스템 구축

  - 분석 배경 <br>
: 책의 내용보다 간단한 책의 제목, 작가, 태그 정보만으로 추천 모델을 만들수 있을지에 대한 아이디어로부터 시작. <br>
만약 가능하다면, 추천 시스템 구축이 더 쉬워질 것이라고 생각하였음. <br>
가벼운 모델을 만드는 것을 목표로 함

  - 데이터셋 <br>
: 책의 아이디, lsbn, 책에 대한 평가 정보 등 <br>
유저가 어떤 책을 읽었는지에 대한 데이터셋 => **훈련 + 테스트 데이터셋으로 사용**

  - EDA <br> 
: 작가당 출판한 책의 수를 시각화 하였음 => 5권 이상의 책을 출판한 작가는 매우 적은 수<br> 
    - 미니 가설) 다양한 언어로 된 데이터셋이기 때문에 영어로 된 데이터만 사용했을 시 더 좋은 성능을 거둘 수 있을 것이다 <br>
    => 하지만 다양한 언어일 때 더 좋은 성능을 보였음.

- Base line model <br> 
: 많이 읽힌 책들을 추천하도록 함

- Modeling (TF-IDF, 코사인 유사도 이용) <br> 
  - 각 유저별로 읽은 책의 목록을 수집한 뒤 읽은 책과 유하 책을 추출한다.
  - 모든 책에 대해서 유사도를 더한 값을 계산한다.
  - 위에서 계산 한 값 중 가장 높으 순서댈 추출한다.

- 추후 계획 <br>
  - EDA 통해 데이터셋 더 자세히 파악
  - 딥러닝 모델로 분석

- Comments
  - 병욱님) 텍스트 인코딩 방식에 대한 질문
  - 소진님) 다양한 언어로 된 데이터셋이 더 높은 성능을 보인 이유는 언어 자체가 분류하는 기준이 되기 때문이 아닐까요?

- 기타 꿀팁 🍯 <br>
  - 미리캠퍼스 => 유용한 템플릿이 많음!!



### 👾 **병욱님 발표**
> FinanceDataReader를 통해 KOSPI 지수를 가져와 예측 모델 만들기

- 데이터셋 <br>
: FinanceDataReader라는 library를 이용해 KOSPI 지수를 가져왔음.<br>
2000년도부터 현재까지의 데이터를 가져와 분석하였음

- OHLC(시가/고가/저가/종가)데이터 분석 <br>
: 해당 데이터는 특정 날짜에 가격이 어떻게 변했는지 보여준다. 과거 가격을 이해하기 위해 분석하였음.
  - 거래량(Volume)<br>
: 특정 기간 동안 거래(구매, 판매)된 주식의 수를 보여주는 기본적인 척도. 주식 거래의 활동을 나타냄.거래량 가치가 높을수록 주식 거래에 대한 관심이 높음을 나타낸다.

- 시각화 <br>
: plotly를 이용해 OHLC 정보를 동적으로 보여줌

- Decomposition <br>
: 시계열 데이터 분해하여 다양한 인사이트를 얻도록 도움을 주는 library
  - Observed : KOSPI의 값을 그려주는 plot
  - Trend(추세) : 시계열이 시간에 따라 증가, 감소 또는 일정 수준을 유지하는 경우
  - Seasonal(계절성) : 일정한 빈도로 주기적 반복되는 패턴
  - Residual(잔차) : Observed에서 추세와 계절성을 뺀 값을 보여주는 plot

<img width="1275" alt="image" src="https://user-images.githubusercontent.com/69139242/127502419-5cc38fe4-70d3-4ead-9fa9-ae4288b36cc8.png">


- Moving Average (이동평균) <br>
  - rolling(5) => 5일치를 평균을 가지고 6일을 예측하도록 하는 메소드
  - ewm(9) => rolling 과 같지만 대략적인 기능은 같지만 과거 데이터에 가중치를 적게 주고 최근에 가중치를 높게 준다.


- RSI 분석 <br>
: 최근 가격 변동의 규모를 나타내는 상대 강도 지수(RSI) <br>

- Modeling <br>
: XGBoostRegressor. 22min 32s초간
  - validation score (MSE) = 0.88 <br>
  => 좋은 성능을 보이지는 못했다.
  => 하지만 종가를 가지고 예측하는 것이 가장 정확도가 높았다.
  => 가중치를 주면서 학습시킨 것이 확실히 F score가 높게 나왔다.

- Comments
  - 보윤님) 시계열 기준으로 데이터를 나눈 것인지? 모델 평가방법에 대한 질문. 주가 데이터 자체가 예측이 어렵기 때문에 잘 안나온 것 같다.
  - 소진님) Decomposition이라는 시계열 데이터에 유용한 라이브러리가 있다는 점이 인상깊었다.



