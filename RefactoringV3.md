# 전역데이터(=static)

![](https://velog.velcdn.com/images/wnsqud70/post/bf2fd8d7-f028-4fd2-95f5-cdd14e13fe60/image.png)

- 전역 데이터는 **아무곳에서나 변경될 수 있다는 문제**가 있다.
- 어떤 코드로 인해 값이 바뀐 것인지 파악하기 어렵다.

- **클래스 변수도 비슷한 문제**를 겪을 수 있다.

=> **변수 캡슐화**하기 적용!

### 전역데이터/ 변수 캡슐화

![](https://velog.velcdn.com/images/wnsqud70/post/a2a06b3c-ad78-430e-8dcf-074a68769d78/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/2a5ab438-f4f1-4f94-b68c-dfaf4accac29/image.png)

- 이것을 적용해서 접근을 제어하거나 어디서 사용하는지 파악하기 쉽게 만들수 있다.

- 허용되지않는 , 말도안되는 값이 들어오는것을 방지하기위해 우리는 **validation 을 쓰는데 이런것들은 메서드로 감싸져있어야 적절한 사용이 가능**하다

- **글로벌한 데이터 접근가능하게 하는것은 보통 상수 , final값들이다**

- 메소드는 점진적으로 새로운 메서드로 변경가능하지만 , 데이터는 한번에 모두 변경해야한다.

### 결론
> 1. 데이터 사용범위가 global 일경우느 더더욱 메서드로 감싸주자(그만큼 수정을쉽게하면 전코드에 영향을 쉽게주니까)
2. global 할수록 사이드이팩트가 심하다 -> 메서드로 감싸고 +Validation 추가

# 가변데이터

- 데이터 변경을 하다보면 예상치 못했던 결과나 해결하기 어려운 버그가 발생하기도 한다.

- **변경할수 있는 데이터를 최대한 줄이도록 노력해야 한다.(그 변경으로 인한 사이드 이팩트 떄문)**

## 사용할 수 있는 리팩토링 기술

> - **변수 캡슐화** = 데이터를 변경할수 있는 메소드를 제한하고 관리
- **코드 정리하기** = 데이터를 변경하는 코드를 분리하고 피할수 있다.
- **변수 쪼개기** = 여러 데이터를 저장하는 변수를 나눌수 있다.
- **함수 추출하기** = 이것으로 데이터를 변경하는 코드로부터 사이드 이펙트가 없는 코드를 분리할수 있다.
- **질의 함수와 변경 함수 분리하기** = 클라가 원하는 경우에만 사이드 이팩트가 있는 함수를 호출하도록 API 개선 가능
- **파생 변수를 질의 함수로 바꾸기** = 계산해서 알아낼 수 있는 값에  적용한다.
- **여러 함수를 클래스로 묶기** = 변수가 사용되는 범위를 제한
- **참조를 값으로 바꾸기** = 데이터 일부를 변경하기보다는 데이터 전체를 교체

- 양이 많지만 그리 어렵지 않다. 한번보자

### 가변데이터/변수쪼개기

- **반복문 순회, 데이터 축척용 변수** 말고 그밖에 재할당 되는 변수가 있다면 한번쯤 변수 쪼개기를 생각해보자

- **변수 하나당 하나의 책임을 지도록 만든다.**

![](https://velog.velcdn.com/images/wnsqud70/post/b4f830d7-49aa-4435-9fe5-f4c4b443b6a8/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/04cdabab-d66c-4c41-84a3-49362fb9b3c2/image.png)

- 똑같은 변수가 여기 저기쓰이면 헷갈리기도하고 가독성도 안좋다, 변수하나당 하나의 책임을 가지도록 만들어주자

![](https://velog.velcdn.com/images/wnsqud70/post/f7cc462b-8558-4bff-a710-c272553bb0a1/image.png)

- result는 **값을 축척하는 용도**로 사용해서 괜찮다.

- **반복문 순회, 데이터 축척용은 괜찮다.**

### 가변데이터/ 질의 함수와 변경 함수 분리하기

- **"눈에 띌만한" 사이드 이펙트 없이 값을 조회할 수있는 메소드**는 테스트 하기도 쉽고 메소드를 이동하기도 편하다

- **어떤 값을 리턴하는 함수 (조회) 는 사이드 이펙트가 없어야 한다.**

- **캐시는 중요한 객체 상태 변화가 아니라** 어떤 메소드의 사이드 이펙트로 캐시데이터를 변경하더라도 분리할 필요 없다.

- **조회함수와 변경함수(modifier) 를 구분하자**

![](https://velog.velcdn.com/images/wnsqud70/post/ea3f3706-0603-42b9-a491-88dfefcccfe4/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/a47ae9d2-39af-45f9-8eae-4daafe01d9c7/image.png)

- 메서드 하나에서 result라는 값을 리턴하며 sendBill()이라는 메서드도 수행한다.

- 두개의 역활을 하는 **메서드를 하나의 역활만 하도록 나누자**   ( 조회와 변경을 나누자!)


![](https://velog.velcdn.com/images/wnsqud70/post/918c5b6b-e760-4e87-857e-e4c0b1b14328/image.png)

- 이것 또한 **조회와 modifier가 같이 있는 메서드**이다! 나누어보자

![](https://velog.velcdn.com/images/wnsqud70/post/c8f957c5-8946-4922-8080-56f9e3d2a5f7/image.png)

- 조회와 Modifier을 나눴다. 하지만 코드가 중복됀다. 이것도 정리를 하면

![](https://velog.velcdn.com/images/wnsqud70/post/47dce1ac-cc68-4cc4-b31a-b856ee3c9f8c/image.png)


- 이렇게 최종적으로 조회와 Modifier을 분리해냈다.


### 가변데이터/ 세터 제거하기 

- 세터가 제공된다는 것은 해당 필드가 변경될수 있다는 뜻이다.

- 안전한 데이터를 위해 **세터를 없애고 생성자로만 값초기화**를 가능 하도록 한다.

### 가변데이터/ 파생 변수를 질의 함수로 바꾸기


- 어떠한 **계산식을 통해 알아낼수 있는 변수는 제거하는게 좋다** . 하지만 그 **변수데이터가 불변이면 상관없다**.

- 변수를 제거하고 그 계산식을 아예 함수에 넣어버리자.

![](https://velog.velcdn.com/images/wnsqud70/post/595f468b-ae66-4d48-b687-32b0a76eaeed/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/be020810-4c1e-464c-8304-224e26492411/image.png)
- 이런 식이면 discountedTotal을 구할수가 없다. (setDiscount가 먼저 실행되야하기 떄문)

![](https://velog.velcdn.com/images/wnsqud70/post/d06b7b72-378a-4c61-af34-593d01d38152/image.png)

- **계산식을 이용해 구하는 변수를 없애고 계산식을 직접 넣어주자.**

- 변수를 줄임으로서 복잡도도 낮아지고 코드도 깔끔해진다.


![](https://velog.velcdn.com/images/wnsqud70/post/f54d3e52-b7c9-4b7f-88f6-1dc188fe9df3/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/ad665352-b29f-44fc-9e2d-a4f4bd4158eb/image.png)

- 이 예제 또한 계산식으로 변수를 구하지말고 **계산식 자체를 바로 함수안으로 넣어준다.**




### 가변데이터/ 여러 함수를 변환 함수로 묶기


- 관련있는 여러 파생 변수를 만들어내는 함수가 여러곳에서 만들어지고 사용된다면 그러한 파생 변수를 **변환 함수** 를 통해 한곳으로 모아둘 수 있다.



- **소스 데이터가 변경될수 있는 경우**에는 **"여러 함수를 클래스로 묶기"** 를 사용하는 것이 적절하다 

- **소스 데이터가 변경되지 않는 경우**에는  두 가지 방법 다 사용 가능하지만 변환 함수를 사용해서 불변 데이터의 필드로 생성해 두고 재사용할 수도 있다.

> **변환함수** :기존데이터를 받아서 새로운데이터 만들어주기
> **데이터가 불변이면** = 클래스로 묶거나 , 트랜스폼으로 묶거나
**데이터가 변경되면** =  클래스로 묶기

![](https://velog.velcdn.com/images/wnsqud70/post/3ae5ab56-fc44-4914-be17-431303afc84f/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/33c18c76-5b4c-43c0-a024-10ef9e72265f/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/ce221b62-b7b0-4eb1-a236-e183415f6f9c/image.png)

- 비슷한 로직을 가지고 있는 클래스가 각각 존재한다. 상속으로 상위 클래스로 빼내도 되지만 여기서는 변환함수를  사용해서 새로운 데이터타입을 만들어내는 방법을 적용할예정

![](https://velog.velcdn.com/images/wnsqud70/post/ca0bdb36-bbb1-44c9-8474-1added0073bf/image.png)

- **record로 불변데이터를 만들어준다.  클래스들이 공통으로 자주사용하는 로직을 여기에 넣어준다.**

![](https://velog.velcdn.com/images/wnsqud70/post/2bcdb1ac-d9e7-4a07-a211-99067e3e6798/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/e62a17be-4bf6-4c03-b638-509caa9b7087/image.png)

- 공통적으로 사용하는 로직을 record 불변데이터에서 받아오도록한다.

![](https://velog.velcdn.com/images/wnsqud70/post/fab80989-11d6-4abf-bbae-0a55bfdf9f5d/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/99f36e47-3b46-4a97-bb46-34c641458735/image.png)

- 클라 1.  ,클라 2 도 역시나 **공통적으로 자주쓰는 로직을 똑같이 한곳에서 가져올수있도록 고쳐준다. **

- 부모클래스에서 그냥 상속으로 빼내도 되고, 이방법은 뭔가 부모 -> record 클래스 가는 느낌(?)

> => 변환함수를 통해 새로운 **record를 만들고 그 recored 에 불변하는 필드(공통된 로직)를 추가**함으로써 중복되던 메서드들이나 로직을 제거 할수있다.



### 가변데이터/ 참조를 값으로 바꾸기

= 변하는 값을 변하지 않는 값으로 바꾸기

> 1. 객체는 크게 두가지로 볼수있다.
- **레퍼런스 객체**: 가변 
- **Value 객체**: 불변 

![](https://velog.velcdn.com/images/wnsqud70/post/6663185f-efac-4061-9477-06a83e88d8e5/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/954f4ec9-08fd-4924-aacc-fc2c1bb79463/image.png)


- TelephoneNumber 는 reference 객체,  person은 value 객체

![](https://velog.velcdn.com/images/wnsqud70/post/f6733ea9-40d7-4d8d-9382-1657f72b8500/image.png)

>  Reference Object -> Value Object   
 - setter없애기
 - 필드 private
 - 오직 생성자로만 데이터 초기화 가능,
 - hashCode,equals
- 이건 자바 11버전.  


- 자바 14버전이후로는 그냥 **record** 
![](https://velog.velcdn.com/images/wnsqud70/post/7aaead84-97be-4c87-a65e-bc1fb2dc7042/image.png)

- 객체를 참조해서 수정할떄코드들도 수정해준다.

- **setter를 사용할수 없으니 생성자를 통해 값 초기화** 

![](https://velog.velcdn.com/images/wnsqud70/post/a659b05c-4617-4ac0-bab8-7e4e8b1814bc/image.png)

- 하지만 자바 14버전 이후로 recored 를 사용하면 저 한줄로도 가능하다

> Record 간단 설명
- 불변
- 참조만 가능한 getter만 존재(메서드명은 필드이름이다)
- hashCode,Equals 구현되있음
- 코틀린의 Data class 와 매우 흡사




 

