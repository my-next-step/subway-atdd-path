# Step1 시나리오 
> 요구사항 명세서에 필요한 시나리오만 작성 예정   
> 이전 미션에서의 시나리오는 생략   

**정상적인 시나리오**
```properties
Feature: 지하철 노선 관리 기능

    Scenario: 지하철 노선에 새로운 하행 종점역 구간을 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선에 새로운 하행 종점역 구간 등록을 요청 하면
      Then 지하철 노선에 새로운 구간이 등록된다.
      예시) 강남 판교 - 판교-정자

    Scenario: 지하철 노선에 새로운 상행 종점역 구간을 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선에 새로운 상행 종점역 구간 등록을 요청 하면
      Then 지하철 노선에 새로운 구간이 등록된다.
      예시) 강남 판교 - 논현 강남

    Scenario: 지하철 노선에 하행을 기준으로 중간 역과 연결되는 새로운 구간을 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선 하행을 기준으로 중앙 방향의 새로운 구간 등록을 요청 하면
      Then 지하철 노선에 새로운 구간이 등록된다.
      예시) 강남 판교 - 양재 판교

    Scenario: 지하철 노선 상행을 기준으로 중앙 방향의 새로운 구간을 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선 상행을 기준으로 중앙 방향의 새로운 구간 등록을 요청 하면
      Then 지하철 노선에 새로운 구간이 등록된다.
      예시) 강남 판교 - 강남 양재

    Scenario: 지하철 노선 목록 조회
      Given 지하철 노선 생성을 요청 하고
      And 새로운 지하철 노선 생성을 요청 하고
      When 지하철 노선 목록 조회를 요청 하면
      Then 두 노선이 포함된 지하철 노선 목록을 응답받는다
```
   
**비정상적인 시나리오**  
```properties
    Scenario: 지하철 노선에 있는 역 사이 길이보다 긴 새로운 지하철 노선 구간 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선에 있는 역 사이 길이보다 긴 새로운 구간 등록 요청을 하면
      Then 지하철 노선에 새로운 구간 등록이 실패한다.

    Scenario: 지하철 노선에 기존 구간에 있는 역들로 새로운 구간 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선에 기존 구간에 있는 역들로 새로운 구간 등록 요청을 하면
      Then 지하철 노선에 새로운 구간 추가가 실패한다.

    Scenario: 지하철 노선에 기존 등록되지 않은 역으로 새로운 지하철 노선 구간 등록
      Given 지하철 노선 생성을 요청 하고
      When 지하철 노선에 기존 등록되지 않은 역으로 새로운 구간 등록 요청을 하면
      Then 지하철 노선에 새로운 구간 추가가 실패한다.
```
* 1주차에서 아래 요소에 대해서 검증했기에, 이 부분은 인수테스트 만들지 않고 진행하겠습니다.(기능은 구현할 예정)    
    * 공백 이름으로 지하철 역 생성    
    * 중복 이름으로 지하철 역 생성    
    * 지하철 역이 없는 상태에서 지하철 노선 생성  
    * 중복 이름으로 지하철 노선 생성  
    * 중복 색깔로 지하철 노선 생성
    * 공백 이름으로 지하철 노선 생성
    * 공백 색깔로 지하철 노선 생성

