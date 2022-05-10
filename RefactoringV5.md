# 기본형 집착

- 애플리케이션이 다루고 있는 도메인에 필요하 기본타입을 만들지 않고 **프로그램 언어가 제공하는 기본타입을 사용하는 경우가 많다.**

- **기본형으로** 단위 또는 표기법을 표현하는데에 **한계**가 있다.

### 관련 리팩토링 기술

> - 기본형을 객체로 바꾸기
> - 타입 코드를 서브클래스로 바꾸기
- 조건부 로직을 다형성으로 바꾸기
- 클래스 추출
- 매개변수 객체 만들기



## 기본형 집착/ 기본형을 객체로 바꾸기

- 개발 초기에는 **기본형으로 표현한 데이터가 나중에는 해당 데이터와 관련있는 다양한 기능을 필요**로 하는 경우가 발생한다.

- 예) 숫자로 표현하던 온도의 단위 -> 화씨,섭씨로 변환하는 경우

- **기본형을 사용한 데이터를 감싸 줄 클래스를 만들면 해결 가능**

![](https://velog.velcdn.com/images/wnsqud70/post/a3daf145-6c1e-4173-aaff-c5134d7cd801/image.png)

- 지금은 단순히 Priority 지역변수의 값을 가져와  계산하는 방식이다. 하지만 이후에는 어떤값이 더 높은지 우선순위 분별 코드가 필요로 해질것이다.

![](https://velog.velcdn.com/images/wnsqud70/post/9c4aa666-e63e-43f8-b123-461f2aec8815/image.png)

- Priority class 에서는 데이터 타입의 안정성이 보장되지 않는다. 그냥 String 라 아무값이나 들어올수 있다.

![](https://velog.velcdn.com/images/wnsqud70/post/cd6ab7fa-c52a-4087-952c-3516fee818b1/image.png)

- 타입의 안정성을 위해 **리스트안에 존재하는 값만 들어올수 있도록** 해준다.

- Value index를 구해주는 메서드와  현재 객체의 value값과 매개변수로 들어오는 값의 index를 비교하는 메서드도 만들어준다.

![](https://velog.velcdn.com/images/wnsqud70/post/47e538f7-4943-4fd3-b8e1-37436b25ee11/image.png)

- Oder 클래스에서는 Priority 를 필드와 생성자로 받고 getter도 만들어준다.  

![](https://velog.velcdn.com/images/wnsqud70/post/5787c5da-55f3-4139-b098-6df5046dc320/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/ef306017-53da-4e7a-8074-b21d67a57db1/image.png)

- order 클래스에서 기존에 있던 **String 타입은 지워준다.**
- 테스트 코드도 무리없이 잘 진행된다.


> => 일반 문자열, **기본타입을 쓰던것을 객체타입으로 만들고 **그 객체를 사용하도록 만들면 **해당 데이터의 기능을 쓰기 쉽다.**

# 기본형 집착/ 타입 코드를 서브 클래스로 바꾸기



![](https://velog.velcdn.com/images/wnsqud70/post/ddfe03a6-ad36-4a08-bd71-f0ab96e5bcd4/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/cb1ed8ca-6c46-4f1f-8f1f-b5e150c40415/image.png)


- 크게 두가지가 있다. 첫번째는 **아무것도 상속받지 않아 이 클래스를 상속을 통해 서브클래스로 뺴낼수 있는 클래스**.

- 두번째는 **이미 상속이 진행되있어서 간접적인 상속을 활용해야하는 클래스**

![](https://velog.velcdn.com/images/wnsqud70/post/fe12161c-913d-4c62-afc8-515e53f84d0e/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/5020f6dd-08fe-4dd1-bd71-489917948661/image.png)


- 일단 첫번쨰 클래스 타입이 추후에 각각의 타입마다 하는일이 많이 달라진다는 가정하에 타입을 서브클래스로 만들어보자

- 각각 Engineer , Salesman , Manager 클래스를 만든뒤 위와 같이 만들어 준다.


![](https://velog.velcdn.com/images/wnsqud70/post/0f0e46d6-3b3b-4828-833b-1678fe5212e1/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/33227006-c46d-4eb9-8386-110b984a68b1/image.png)

- 더 이상 Employee 에 **type 이란 필드는 필요하지 않다**. 그에따라 생성자 및 다른 코드들도 수정해주자.

- 각각 자식클래스에서 오버라이드한 메서드는 당연히 abstract로 바꿔준다.

- 기존에 사용하던 메서드 validate도 더이상 필요가 없으니 지워준다.

![](https://velog.velcdn.com/images/wnsqud70/post/448942ae-f18e-4a9e-8a0e-dbde05b0f8be/image.png)


- 테스트 부분도 우리가 만든 static메서드로 교체 해준다.

### 두번째 클래스 타입인 경우

![](https://velog.velcdn.com/images/wnsqud70/post/4e7f91bc-f442-4e20-becf-3322424ad157/image.png)

- 이미 상속을 받는 상태인 경우


![](https://velog.velcdn.com/images/wnsqud70/post/38893552-faa5-475c-9d37-c5301f57136f/image.png)

- **EmployeeType** 라는 클래스를 만든뒤 각각 자식클래스들이 **이 클래스를** **상속** 받게 한다. (자식클래스들도 새로)

![](https://velog.velcdn.com/images/wnsqud70/post/fd5f471b-0dc1-4152-85ae-f3bc9091f648/image.png)



- EmployeeType 를 적용시켜보자 . Emploee 에서는 참조를 하며 이전방법과 같이 메서드를 만들어준다.

- **Employee도 부모클래스이지만 다른 부모클래스 EmployeeType 도 참조중인 상황**


![](https://velog.velcdn.com/images/wnsqud70/post/4f34147b-6cf3-4b51-b147-fa3653426109/image.png)

- 필요가 없는 필드와 메서드를 지워서 코드를 정리 해준다.

- capitalizedType() 는 **다른부모 클래스에게 위임**해준다.

![](https://velog.velcdn.com/images/wnsqud70/post/912f2e2b-5274-4e79-a3ce-5066b8627a07/image.png)

- 다른부모 **자식클래스에 오버라이드한 toString**이 동작한다.

![](https://velog.velcdn.com/images/wnsqud70/post/94aa9fbc-86a3-4d8f-8d6a-a8785ed248c1/image.png)

- 생성자 -> 필드(다른객체) 초기화 -> 그객체의 메서드

# 기본형 집착/ 조건부 로직을 다형성으로 바꾸기

- 복잡한 switch, if- else 문은 **상속**이나 **다형성**을 활용해 해결할수 있다.

예) 이러한경우에는 이렇게 동작하고 , 저러한 경우에는 저렇게 동작

![](https://velog.velcdn.com/images/wnsqud70/post/d82f1435-b62c-4e8a-bd5d-75bf7a3f3335/image.png)

- 이 예제인 경우에도 적용이 가능하다 (switch 문)

![](https://velog.velcdn.com/images/wnsqud70/post/e9c75c84-126a-450f-a56e-067a2c9bf6a4/image.png)


- 일단 상속을 받는 자식 클래스들을 만들어준다

![](https://velog.velcdn.com/images/wnsqud70/post/8cbda2c3-5d56-490a-bef5-9c79a658cee2/image.png)

- 부모 클래스의 메서드들도 수정 해준다.


![](https://velog.velcdn.com/images/wnsqud70/post/2968d8f8-f7aa-4be8-a8c0-993cf75d63fc/image.png)


- type 라는 필드는 더이상 필요가 없으므로 지워주고 그에 해당하는 생성자도 지워준다.

- 오버라이드를 당하는(?) 메서드들도 한눈에 보기좋게 abstract로 만들어준다

- **자식클래스 중에서 중복되는 메서드는 위로 (부모클래스로) 올려준다.**

# 반복되는 Switch 문

-  위에서 함

# 반복문을 파이프라인으로 바꾸기

-  반복문을 필터나 맵핑과 같은 파이프라인 기능을 사용해 적용시켜주면 보다 빠르게 어떤 작업을 하는지 파악할 수 있다.

![](https://velog.velcdn.com/images/wnsqud70/post/91b332b2-23ed-4089-9cee-873a7a56b7ef/image.png)


- 반복문을 보면 **한눈에 보기가 쉽지않다. 한줄한줄 해석해서 읽어야함.**
- 이 반복문을 **파이프라인으로 바꿔 좀더 명확한 코드**로 만들어주자


![](https://velog.velcdn.com/images/wnsqud70/post/61b5ed06-45c1-46a4-90a5-aed6e29f8209/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/0f97ad33-5517-4245-99e8-1ea6bf55fb95/image.png)

- 첫 if문부터 바꿔주자 . ** stream/filter/lamda **


![](https://velog.velcdn.com/images/wnsqud70/post/ce21c7c8-3e14-4b6c-abc3-9549d3b44abd/image.png)


- map 으로는 해당 데이터 안의 데이터 타입을 바꿔준다.


![](https://velog.velcdn.com/images/wnsqud70/post/f1f66b8e-b9af-4b13-9dc1-f057a840987d/image.png)

- 마지막으로 **collect**를 사용해 List에 해당 값들을 넣는것을 표현해준다. 이러면 기존코드들(주석처리된)은 더 명확하게 대체 될수 있다.


# 성의없는 요소

- 가끔 **예상하고 만들어 놓은 요소**들이 부응하지 못하는 경우가 있는데 그런 경우에 해당 요소들을 제거 해야한다.

### 관련 리팩토링 기술
- 함수 인라인
- 클래스 인라인
- 불필요한 상속 구조는 **계층 합치기**


# 추측성 일반화

- 나중에 이런저런 기능이 생길것을 예상하여 여러 기능을 만들어 놨지만 결국에 쓰이지 않는 코드가 발생할 경우..

- YAGNI(u r not gonna need it) 원칙을 따르자

# 추측성 일반화 / 죽은 코드 제거하기

- 사용하지 않는 코드가 애플리케이션 성능이나 기능에 영향을 끼치지는 않는다.

- **나중에 필요해질 코드라 하더라도 지금 쓰이지 않는 코드라면 (주석으로 감싸는게 아니라) 삭제 해야한다.**
