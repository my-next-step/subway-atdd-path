# Step1 요구사항 명세서 

## 정상적인 기능 설명
**역 사이에 새로운 역을 등록할 경우**
* 기존 구간의 역을 기준으로 새로운 구간을 추가
    * 기존 구간 A-C에 신규 구간 A-B를 추가하는 경우 A역을 기준으로 추가
    * 기존 구간과 신규 구간이 모두 같을 순 없음(아래 예외사항에 기재됨)
    * 결과로 A-B, B-C 구간이 생김
* 새로운 길이를 뺀 나머지를 새롭게 추가된 역과의 길이로 설정
* 정리하자면, **새로 추가되는 구간은 하행/상행이어야하고 나머지는 기존에 존재하던 역이 아니어야한다.**   

  
**노선 조회시 응답되는 역 목록 수정**   
* 구간이 저장되는 순서로 역 목록을 조회할 경우 순서가 다르게 조회될 수 있음
* 아래의 순서대로 역 목록을 응답하는 로직을 변경해야 함 
    1. 상행 종점이 상행역인 구간을 먼저 찾는다. 
    2. 그 다음, 해당 구간의 하행역이 상행역인 다른 구간을 찾는다. 
    3. 2번을 반복하다가 하행 종점역을 찾으면 조회를 멈춘다.
* 정리하자만, 상행종점 찾고 -> 이전상행역 == 이후상행역 찾고 -> 하행 종점 찾으면 끝 

## 변경된 스펙 - 예외 케이스

**역 사이에 새로운 역을 등록할 경우 기존 역 사이 길이보다 크거나 같으면 등록을 할 수 없음**
* 기존 하행 == 새로운 구간 하행 : 상행과 기준이 되는 하행과의 길이보다 크면 예외다.    
* 종점이라고 작성 안한 이유는, 중간 하행을 기준으로 추가할 수 있기 때문이다.

**상행역과 하행역이 이미 노선에 모두 등록되어 있다면 추가할 수 없음**   
* A-B, B-C 구간이 등록된 상황에서 B-C 구간을 등록할 수 없음(A-C 구간도 등록할 수 없음)

**상행역과 하행역 둘 중 하나도 포함되어있지 않으면 추가할 수 없음**
* 상행역과 하행역 둘 중 하나만 기존 노선에 포함되어 있어야한다는 말이기도 하다.  

# 추가된 기능에 대한 인수 테스트 작성  
* 요구사항이나 스펙이 변경될 경우 인수 테스트를 수정해야 함
* 아래에 기재된 변경된 요구사항을 충족하는 인수 테스트를 작성
* 예외 케이스까지 함께 인수 테스트 작성
* 인수 테스트들이 공통으로 필요로 하는 코드의 중복 처리를 고민

# 인수 테스트 이후 TDD
* 인수 테스트 작성 이후 개발 시 TDD를 활용     
* 도메인 부분은 필수로 진행     
* 서비스 레이어 부분은 선택적으로 진행     
    * 실제 작성하면서 Classit VS Mockito 비교도 재밌을것 같다.   
    * 둘을 따로 한다기보다는, 미리 Mockito 로 작성하고 Classit으로 리팩토링은 어떨까?
  
## 기능 구현 팁  
세부적인 예외 상황을 고려하지 않고 Happy Path 경우를 검증하기 위한 인수 테스트를 먼저 만드세요.    
"Happy Path"는 '아무것도 잘못되지 않는 사용자 시나리오'를 의미한다    
(All-Pass Scenario / Positive Test).   
이는 사람의 실수, 엣지 케이스, 의도를 벗어난 행동을 포함하지 않기 때문에       
이 시나리오 대로 테스트를 수행하면 이슈나 버그가 발생할 가능성이 현저히 낮아진다.   
