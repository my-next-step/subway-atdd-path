# Step2 요구사항 명세서

## 정상적인 기능 설명

**노선 맨앞에 있는 역을 삭제할 경우**
* 노선이 최소 2개이상이라고 가정
* 노선의 맨 앞의 역을 삭제하는 작업
  * 기존 A-B, B-C 구간에서 A를 삭제
  * B-C라는 노선만 남게 된다.
* 생각해볼점 : 노선이 3개이상이라고 가정 
  * 기존 A-B, B-C, C-D 구간에서 A를 삭제  
    * 이때, 기존 노선의 상행선을 기준으로 A를 찾고 삭제한다.      
  * B-C, C-D 라는 노선만 남게 된다.   
  
**노선 중간에 있는 역을 삭제할 경우**
* 노선이 최소 2개이상이라고 가정
* 노선의 중간 역을 삭제하는 작업
  * 기존 A-B, B-C 구간에서 B를 삭제
  * A-C라는 노선만 남게 된다.
* 생각해볼점 : 노선이 3개 이상이라고 가정
  * 기존 A-B, B-C, C-D 구간에서 B를 삭제
    * 이때, 일치하는 상행성 및 하행성을 각각 찾는다.  
    * 하나는 지우고, 하나는 서로의 상하행선으로 업데이트한다.  
  * A-C, C-D 라는 노선만 남게 된다.

**노선 마지막에 있는 역을 삭제할 경우**
* 노선이 최소 2개이상이라고 가정
* 노선의 마지막 역을 삭제하는 작업
  * 기존 A-B, B-C 구간에서 C를 삭제
  * A-B라는 노선만 남게 된다.
* 생각해볼점 : 노선이 3개 이상이라고 가정
  * 기존 A-B, B-C, C-D 구간에서 D를 삭제
    * 이때, 기존 노선의 하행선을 기준으로 D를 찾고 삭제한다.
  * A-B, B-C 라는 노선만 남게 된다.  

### 로직을 생각해보면

1. 삭제하는 역을 파라미터로 받는다.   
2. 상행선에 속하는지, 하행선에 속하는지 각각 찾는다.   
3. 아래와 같은 분기가 나뉘어진다.
   1. 상행선만 존재한다 -> 상행선만 찾아서 삭제하는 로직   
   2. 하행선만 존재한다 -> 하행선만 찾아서 삭제하는 로직   
   3. 상하행선 존재한다 -> 두 구간을 찾고 하나는 삭제, 하나는 변경한다.(삭제후 새로 생성도 고려가능)
       1. 단, 업데이트하면 거리를 다시 조정해야한다.   
       2. 기존 distance 를 서로 더한 값을 새로운 distance 값으로 해야한다.  
   4. 상하행성 둘다 존재하지 않는다 -> 예외 발생
4. 삭제 작업이 종료된다.  

## 비정상적인 기능 설명

**노선에 등록되지 않은 역을 기준으로 삭제**    
* 앞선, 상하행선 모두 존재한지 않는 역을 의미한다.   
* IllegalArgument 및 BAD_REQUEST 응답을 사용한다.  
  
**노선 등록된 구간의 갯수가 1개일 때의 삭제**  
* 노선에 등록된 구간의 갯수가 1개임을 의미한다.     
* IllegalState 및 BAD_REQUEST 응답을 사용한다.  


