# 뒤엉킨 변경

- 소프트웨어는 **변경에 유연**하게 대처할 수 있어야 된다.

- **응집력은 높고 결합도는 낮게**

- 어떠 한 모듈이(함수 또는 클래스가) 여러가지 이유로 다양하게 변경되어야 하는 상황.

## 관련 리팩토링 기술

> 1. **단계 쪼개기** => 서로 다른 문맥 코드 분리
2. **함수 옮기기** =>  적절한 모듈로 옮기기
3. **함수 추출하기** => 여러가지 일이 하나의 함수에 모여 있으면
4. **클래스 추출하기** => 모듈이 클래스 단위 이면


### 뒤엉킨 변경/단계 쪼개기

- 서로 다른 일을 하는 코드를 각기 다른 모듈로 분리 
=> 그래야 오류가나도 서로 영향을 주지않고 해당 부분만 수정 하면된다.

- 여러 일을 하는 **함수의 처리 과정을 각기 다른 단계로 구분**
예) 컴파일러: 텍스트 읽어오기 -> 실행 가능한 형태로 변경

- **중간 데이터**를 만들어 **단계를 구분하고 매개변수를 줄이는데 활용!**


![](https://velog.velcdn.com/images/wnsqud70/post/b48f4238-d69f-4c8f-a0a8-34a51ceb30d0/image.png)

- 함수 하나의 여러 기능이 들어있다. 분리해주자!

![](https://velog.velcdn.com/images/wnsqud70/post/baef4ec8-38a3-4d6f-a3e1-937ccfabb837/image.png)

- 각각 다른일을 하는 코드들을 분리한다.

![](https://velog.velcdn.com/images/wnsqud70/post/eacec584-65f2-4962-9b62-7181ff7e6e17/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/770c4d91-ff0d-4957-ad90-41fa1cebc388/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/6685f728-f54c-4213-b309-ee375829342a/image.png)

- 다른 역활을 하는 한쪽을 메서드 추출로 분리해준다. 

- **중간데이터(Record) **를 활용해  단계를 구분하고  중간데이터를 활용

- Record에다가 필요한 매개변수들을 넣어서 통쨰로 보낸다. -> **메서드 실행하는쪽의 매개변수를 줄일수 있다.**

![](https://velog.velcdn.com/images/wnsqud70/post/6ece08e9-6ebb-4891-96b0-2403343d34af/image.png)

- 최종적으로 **인라인** 리팩토링으로 코드를 줄여준뒤 정리해준다.

## 뒤엉킨 변경/ 함수 옮기기

- 함수가 포함된 문맥(클래스) 에서  **외부에서 더 참조를 많이 한다면** 함수 옮기기를 고민해보자

- **함수를 어디다 둬야할지모르면 ( 애매하면 = 여기저기쓰이면). 그냥 그대로 둬도 좋다**

- 함수의 위치 고려하기

![](https://velog.velcdn.com/images/wnsqud70/post/34c098a6-f58f-43c7-b8fc-fe3073d8c074/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/02275340-0141-433d-ad1a-7387d89b5ce5/image.png)

- 위 overdraftCharge는  사실상 참조반  포함된 문맥 반 이지만  한번 참조한 클래스로 함수를 옮겨보자

![](https://velog.velcdn.com/images/wnsqud70/post/341b7b10-82e7-4c84-8f7e-9ff53f40b776/image.png)

- Refactor -move instance method 
- Account 안에 데이터중 여러데이터를 사용하면 Account 통쨰로 받는것이 좋지만 우리는 필드값 하나만 필요함으로 그값 하나만 파라미터로 받는다

![](https://velog.velcdn.com/images/wnsqud70/post/955ae7c6-763d-4c02-8cf3-ddcfa94e1a45/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/5c517bf7-b9c0-4f19-8658-ffbd3746f44d/image.png)

- 함수를 옮겼을때 Account 객체 통쨰로 넘겨주면  Account ->  AccountType 참조연관/. 그반대로도 성립하기떄문에 좋지않다. 그래서 필요한 필드값만 매개변수로 넘겨준다

- 이렇게 하면 **응집력은 높아지면서 결합도는 낮아지는 좋은 코드**가 된다
