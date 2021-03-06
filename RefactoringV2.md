# 긴 매개변수

 - **매개변수가 많을수록 많은 역활을 한다**. 많은 역활을 한다는 뜻은 많은 기능, 서로 연관관계가 있는 많은 코드들이 **한곳** 에 있다는 소리다.
 
- 불필요한 매개 변수가 없나 체크해보자

- 자바 객체지향에서는 서로 코드들이 독립적일수록 좋다.

### 사용할 수 있는 리팩토링 기술

1. 어떤 매개변수를 다른 매개변수를 통해서 알아낼수 있다? 
-> **매개변수 질의 함수로 바꾸기**

2. **객체 통째로 넘기기**

3. 매개변수가 플래그로 사용된다면 ?
->**플래그 인수 제거하기**

4. 여러 함수가 일부 매개변수를 공통적으로 사용한다면?
-> **여러 함수를 클래스로 묶기**


# 긴 매개변수/ 매개변수를 질의 함수로 바꾸기

- 함수의 매개변수 목록은 함수의 다양성을 대변하며, **적을수록 이해하기 좋다.**

- 매개변수에 값을 전달하는 것은 "함수를 호출하는 쪽" 의 책임이다. **가능하며 함수를 호출하는 쪽의 책임을 줄이고 함수 내부에서 책임지도록 노력한다.**


![](https://velog.velcdn.com/images/wnsqud70/post/5de64503-0714-44c5-a9bf-f4d9c4880971/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/15ec16fb-cb0b-4c7a-aab5-b9cabbf4f768/image.png)

- 이렇게 매개변수로 사용하고 있는 부분을  메서드 추출뒤에  정리해주면 더 깔끔하다


# 긴 매개변수 / 플래그 인수 제거하기

- **플래그는 보통 함수에 매개변수로 전달해서, 함수 내부의 로직을 분기하는데 사용**


![](https://velog.velcdn.com/images/wnsqud70/post/0a4b9352-158c-4c2e-b65c-28405b439377/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/e45701d9-2b84-4fe8-94a1-d052e79865cd/image.png)



- 플래그를 사용한 함수는 차이를 파악하기 어렵다. 이러한경우 **실제 메서드 실행시 보내는 파라미터가 무엇을 의미하는지 직접 가보지 않고서는 알수가 없다.**


- 예전에 사용했던 decompose 방법을 사용해보자 ( **각각 기능별로 메서드추출!**)


![](https://velog.velcdn.com/images/wnsqud70/post/2e77b7ab-29f5-4dee-a57d-00cd24433884/image.png)


- 메서드 추출후 메서드이름까지 직관적으로 바꿔준다
-> ** 메서드를 분리함으로써 좀더 직관적이고 플래그 인수도 제거했다.**

-  또한 코드를 나눔으로써 서로 좀더 **독립적인 코드**가 됐다.


> => 메서드 하나가 너무 많은 기능을 처리하면 그만큼 수정시 전체 코드를 수정해야한다. 또한 서로 너무 의존적이다. 자바에서는  **서로 좀 더 독립적이게 만들어주자**

# 긴 매개변수 -여러 함수를 클래스로 묶기

![](https://velog.velcdn.com/images/wnsqud70/post/23902efa-9ed9-49cd-b1da-519d4bfde4ce/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/989d26b9-291e-46e6-94cd-beac0542cfe2/image.png)


- Print 라는 아주 긴 메서드가 있다고 하자.(여러 기능이 있다는 의미) 그 아래 메서드들은 Print메서드의 일부에서 필요한 메서드들( 서로 연관관계가 끈끈하다)


=> Print라는 긴 메서드를 분리할 생각이다.(그래야 좀더 독립적이니까)

![](https://velog.velcdn.com/images/wnsqud70/post/ce164bf8-3110-4cc1-a5ea-999e4379c2da/image.png)


 - print 코드중 일부를  **메서드 추출**시도해보자 
 -> **이 일부 메서드는 participants라는 매개변수로 필요함**

- 또한 Print 메서드에 필요한 메서드들 안에서 필요한 공통적인값( 맨위에 필드로 선언되있는) 

 그러면 **메서드 추출 메서드** 에 필요한 요소는
> 1. Participants
> 2. 공통적인값(메서드 추출 내부에서 필요한 공통값)

이 두가지만 있으면 메서드 추출로 만든 메서드를 따로 클래스로 빼서 Print(긴 메서드) 를 좀더 독립적으로 서로 분해할수 있지 않을까???


![](https://velog.velcdn.com/images/wnsqud70/post/12a9d761-69d4-4cc3-85b2-2c89b9be2c19/image.png)

- 메서드 추출로 만든 메서드에 필요한것들을 챙겨서 따로 클래스를 만들어준다.

![](https://velog.velcdn.com/images/wnsqud70/post/ceb36973-5b1b-4d3c-ad65-dbd17c9ed853/image.png)


- Print(긴 메서드) 에서 호출부분


=> 긴함수 ->분리 ->**분리하는 부분에서 필요한것들을 챙겨서 다른 클래스**로 옮겨준다. => 좀더 독립적인 코드가 됌

![](https://velog.velcdn.com/images/wnsqud70/post/7e91ceac-bb1d-4295-88b3-435d78bf5b6d/image.png)

![](https://velog.velcdn.com/images/wnsqud70/post/2b2a1f42-12b8-44a0-9a57-17b66b9c7a6c/image.png)


- 메서드 추출 메서드에 필요한 메서드 
- 공통된 값을 필드로 가져와 클래스에 묶어줬기 때문에 필드값을 쓰면 됨으로 **매개변수를 줄일수 있다.**


![](https://velog.velcdn.com/images/wnsqud70/post/0cffa643-3241-4319-aa51-e1c6c327b9f1/image.png)


- **필드값으로 선언한 요소들을 통해 값을 얻을수있다면 그만큼 매개변수도 줄어든다 **

- 매개변수와 필드변수 구별위해 this 를 사용화 하자


**결론**
> ==> 관련있는 데이터를 한곳으로 옮기고 메서드를 옮기면 매개변수도 줄면서 이해하기 쉬운코드가 됀다!



자세한 내용은 기술블로그에 포스팅 하였습니다 
-> https://velog.io/@wnsqud70/RefactoringV2



