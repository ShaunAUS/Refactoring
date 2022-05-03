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

## 뒤엉킨 변경/ 클래스 추출하기

- 클래스가 다루는 책임이 많아질수록 클래스가 점차 커진다

#### -클래스를 쪼개는기준-

> 1.데이터나 메소드 중 일부가 매우 **밀접한 관계**가 있는 경우
2.일부 **데이터가 대부분 같이** 바뀌는 경우


![](https://velog.velcdn.com/images/wnsqud70/post/bcbd166c-96c2-45b2-af25-d6b0290d4739/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/07424b82-fc49-47dd-9423-af28a5019108/image.png)

- 클래스가 한눈에봐도 들어가있는게 많다.(= 책임이 많다)

- 서로서로 **조금더 밀접한 관계가 있는것들을 찾아준다.** 위에서는 officeAreacode 와 officeNumber

![](https://velog.velcdn.com/images/wnsqud70/post/3b396729-33a4-42a2-a156-5fece4352c0e/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/eeae2673-1eb5-4026-be75-40657eb08e92/image.png)


- 밀접한 관려이 있는것들 끼리 모아서 따로 클래스로 만들고 기존 클래스가 이 클래스를 참조하도록 만들었다.

![](https://velog.velcdn.com/images/wnsqud70/post/e4a396c1-9f60-4fe2-989d-5e60e316046c/image.png)


- TelephoneNumber 문맥에서는 필드명들이 어울리지 않다. 수정해주자

![](https://velog.velcdn.com/images/wnsqud70/post/4f90e57d-05f1-49ab-916c-52f4602cace7/image.png)


- 호출 하는쪽도 이름을 그에 걸맞게 수정해준다.

- getTelephoneNumber은 메서드위치기  TelephoneNumber 클래스가 더 적절함으로 옮겨준다.


# 산탄총 수술

- **어떠 한 변경 사항이 생겼을때 여러 곳을 수정 해야 하는 상황**(산탄총을 맞으면 여러곳이 구멍 슝슝)

- "뒤엉킨 변경" 과 흡사하지만 반대의 상황/ 산탄총 수술은 반대로 합친다.


## 관련 리팩토링 기술

> - **함수 옮기기/ 필드 옮기기**  => 필요한 변경 내역을 하나의 클래스로 모으기
- **여러 함수를 클래스로 묶기** => 비슷한 데이터를 사용하는 여러 함수 묶기
- **단계 쪼개기** => 공통으로 사용되는 함수의 결과물 하나로 묶기


## 산탄총 수술/ 필드 옮기기

- 좋은 데이터 구조를 가지고 있다면, 해당 데이터에 기반한 어떤 행위를 코드로 옮기는 것도 간편하고 단순해진다


![](https://velog.velcdn.com/images/wnsqud70/post/957ba840-4f17-461b-aea7-90f9a11f2716/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/71acb0fa-a19a-4c8f-b86b-a74a7b2c65f4/image.png)

- 이러한 두클래스가 있다는 가정하에 discountRate가 지금은 Customer에 있지만 CustomerContract 로 옮긴다는 가정을 해보자

![](https://velog.velcdn.com/images/wnsqud70/post/48f8c332-492b-4235-8f52-b1823deafa9c/image.png)


- 일단 this 로 지역변수에 직접적으로 접근하고 있지만 getter/setter 접근하게 만들어  캡슐화를 진행 해준다.

![](https://velog.velcdn.com/images/wnsqud70/post/9db17481-ca88-45b6-8cd3-e62e1808f8bd/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/fb361a09-de78-445a-929b-14a19b6a07c8/image.png)

- 필드를 넘겨주자 CustomerContract 생성자에 discopuntRate 를 넘겨주고  getter/setter 도 CustomerContract의 getter/setter 로 접근하도록 만들어준다(pritavte)


