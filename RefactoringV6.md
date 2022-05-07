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
