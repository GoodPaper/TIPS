# Eikon query tips


### Screen
* 어떤 조건에 해당하는 종목들을 Screening 할 때 사용한다.
```text
SCREEN(
  ( U( IN( Equity( active, public, primary ) ) ) ), # Equity 중 현재 살아있고, 상장, 비상장 회사를 포함하겠다.
  IN( TR.HQCountryCode, 'US' ), IN( TR.TRBCBusinessSectorCode, 5010 ),... # 조건을 여기에 입력한다. SQL의 WHERE 절이라고 생각하면 된다. 여기서는 본사가 미국, TRBC Sector code가 5010 인 것을 필터링 해달라고 적은 것이다.
  CURN=USD # 통화는 US Dollar로 사용하겠다.
)
```
* 이 구문은 instrument 부분의 입력으로 사용 가능하다. 아래는 Excel과 Python에서 사용한 예제이다.
```text
# Equity & Public 종목 중 NYSE에 상장된 종목들에 대해서, 회사 이름, 종목 타입, Exchange 이름을 뽑아라.
=TR(
  "SCREEN(U(IN(Equity(active,public))), IN(TR.ExchangeMarketIdCode,"XNYS"),CURN=USD)",
  "TR.CommonName;TR.InstrumentType;TR.ExchangeName",
  "curn=USD"
)
```
```python
import eikon

eikon.get_data(
  "SCREEN(U(IN(Equity(active,public))), IN(TR.ExchangeMarketIdCode,\"XNYS\"),CURN=USD)",
  [ 'TR.CommonName', 'TR.InstrumentType', 'TR.ExchangeName' ],
  raw_output = True
)
...

```

### Fields
|Name|Timeseries support|Subfield support|Description|More|
|--|--|--|--|--|
|TR.CIKNUMBER|X|?|EDGAR CIK 번호||
|TR.CommonName|X|?|회사 이름||
|TR.ISIN|O|O|ISIN 코드||
|TR.RIC|O|O|RIC 코드||
|TR.OPENPRICE|O|O|시작 가격|(Adjusted=0)을 붙이면 조정되지 않는 날 것 그대로의 가격, 1이면 조정된 가격|
|TR.HIGHPRICE|O|O|최고 가격|위와 동일|
|TR.LOWPRICE|O|O|최저 가격|위와 동일|
|TR.CLOSEPRICE|O|O|마지막 가격|위와 동일|
|TR.ACCUMULATEDVOLUME|O|O|누적 거래량|위와 동일|
|TR.EPSActualReportDate|O|O|EPS 실제 발표일||
|TR.RevenueActReportDate|O|O|매출액 실제 발표일||
|TR.DilutedEpsInclExtra|O|O|Dilute되고, Extraordinary items를 포함한 EPS|(ConsolBasis=Consolidated)를 사용하면 연결 데이터로 가져옴|
|TR.DilutedEpsExclExtra|O|O|Dilute되고, Extraordinary items를 포함하지 않는 EPS|위와 동일|
|TR.TotalRevenue|O|O|총 매출액|위와 동일|
|TR.LTDebt|O|O|장기 부채|위와 동일|
|TR.ShareHoldersEquityActual|O|O|실 주주 지분|위와 동일|
|TR.FreeCashFlow|O|O|잉여 현금 흐름|위와 동일|
|TR.RevenuePerShare|O|O|주당 매출액|위와 동일|
|TR.GICSSubIndustryCode|X|O|GICS 세부 산업 코드||
|TR.CompanyMarketCap|O|O|회사 시가 총액, 관련 주식 및 회사의 총합|(ShType=OUT)는 전체 주식으로 계산, (ShType=FFL)은 유통 주식으로 계산|
|TR.IssueMarketCap|O|O|주식 시가 총액, 본 주식만 해당|위와 동일|
|TR.ExpectedReportDate|X|O|다가올 실적 발표일||
|TR.CompanyFYearEnd|X|O|회사 결산일자||
|TR.EPSEstValue|O|O|EPS 추정치||
|TR.RevenueEstValue|O|O|매출액 추정치||

### Parameter
* SDate: 시작 일자, 시계열로 요청하는 경우의 시작 일자. YYYYMMDD 혹은 YYYY-MM-DD 로 사용가능. Type은 String.
* EDate: 종료 일자, 시계열로 요청하는 경우의 마지막 일자. 나머지는 위와 동일
* Frq: Frequency, 시계열로 요청하는 경우의 데이터 간격.
  * Y: Yearly, Q: Quarterly, M: Monthly, W: Weekly, D: Trading days
  * FY: Fiscal year, FS: Fiscal semi annual, FQ: Fiscal quarter
  * CY: Calendar year, CQ: Calendar quarter, CM: Calendar month
  * F: Fiscal periods
