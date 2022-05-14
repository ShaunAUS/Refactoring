# 메시지 체인

- 레퍼런스를 따라 계속해서 메소드 호출이 이어지는 코드
예) this.member.getCredit().getLeverl()....

- **체인중 일부가 변겨된다면 클라이언트 코드도 변경 해야한다.(전체수정)**

- 해당 코드의 클라이언트가 코드 체인을 모두 이해해야함.



### 메시지 체인/ 위임 옮기기

- 클라이언트가 **최소한의 정보만 알고 코드를 사용할수있게** 만드는게 가장 큰 목적

- **캡슐화는 연쇄적인 변경 전파를 최소화 시킨다**

![](https://velog.velcdn.com/images/wnsqud70/post/85153bdb-6959-4802-ad6f-190c6cc08824/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/57d9fbdb-a4b8-42a8-b678-1d75877e31cf/image.png)

-  드래그 친부분은 캡슐화가 필요한 부분이다. 저렇게 작성하면 나중에 변경사항이 있을때 저 테스트 코드 전체가 영향을 받아 하나하나 다 수정 해줘야한다.
![](https://velog.velcdn.com/images/wnsqud70/post/ae9af501-4b1c-4746-baa4-39718275029e/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/30cc3cae-745b-47e4-aa72-f95a1b27898d/image.png)

- 메서드 추출로 캡슐화를 진행해준다음 Person클래스에 메서드를 올린다.

- 이렇게 되면 나중에 **변경사항이 있어도 getManager()를 호출하는 부분은 수정을 안해도되고 직접적으로 메서드가 있는곳 Person 클래스만 수정하면 된다.**


이 내용은 예전에 포스팅한 내용과 비슷해서 링크를 남긴다

[캡슐화
](https://velog.io/@wnsqud70/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5#%EC%BA%A1%EC%8A%90%ED%99%94)

# 중재자

- 캡슐화와 반대되는 기술

- 어떤 **클래스의 메소드가 대부분 다른 클래스로 메소드 호출을 위임**하고 있다면 중재자를 제거하고 클라이언트가 해당 클래스를 직접 사용할수 있도록 개선할수 있다.

### 관련 리팩토링

> - 중재자 제거하기
- 슈퍼클래스를 위임으로 바꾸기
- 서브클래스를 위임으로 바꾸기

### 중재자/ 중재자 제거하기

- 필요한 캡슐화의 정도는 시간에 따라 그리고 상황에 따라 바뀔수 있다.

- 캡슐화의 정도를 조정하자. (**항상 캡슐화가 옳은것은 아니다**)

- **Law of Demeter를 지나치게 따르기 보다는 상황에 맞게 활용**


![](https://velog.velcdn.com/images/wnsqud70/post/47a8e40d-42ea-4f42-8221-1548e5e0255a/image.png)

- 서로 참조하는 클래스 두개가 있다.

![](https://velog.velcdn.com/images/wnsqud70/post/a79b81df-32d2-4149-93c2-f00febba15c3/image.png)

- getManager() 메서드를 보면   Person -> Department -> Person  클래스를 거치면서 데이터를 가져오고 있다.

- 만약 가져와야할 데이터가 이것저것 많다면? 캡슐화는 좋지만 굳이 Person클래스를 거쳐서 갈 필요가 있을까??


![](https://velog.velcdn.com/images/wnsqud70/post/40bd6a27-f0f6-4d6d-ac25-97b149280975/image.png)


- 중재자(캡슐화한 메서드) 를 제거 해주고 바로 Department로 접근할수 있도록 getter을 만들어준다.

### 중재자/ 슈퍼클래스를 위임으로 바꾸기(=상속끊기,위임,주입)

-  "**상속**" 은 쉬우면서도 강력한 방법이지만 때로는 적절하지 않는 경우도 있다.

- 서브클래스는 슈퍼클래스의 모든 기능을 지원 해야한다.

- 서브클래스는 슈퍼클래스의 변경에 취약하다/ 서브클래스가 많아 질수록 관리가 힘들다.(상속구조가 어떻게 되어있는지 파악하기 힘듬)

- **우선 상속을 적용한 이후에, 적절치 않다고 판단이 된다면 그때 이 리팩토링 적용**

![](https://velog.velcdn.com/images/wnsqud70/post/2adf76f3-c888-48ff-80e9-55703b86999e/image.png)


![](https://velog.velcdn.com/images/wnsqud70/post/becc2e7f-c9f0-4e8e-a5c1-fe043ae19bbd/image.png)


- 상속 관계가있는 두 클래스가 있다.

- 상속 관계를 끊는 방법은 **필드로 그 객체를 주입 받는 방법**이다. 이렇게 하면 상속관계를 끊었지만 여전히 슈퍼클래스에 해당했었던 클래스를 주입을 받아 사용 가능하다.


### 중재자/ 서브클래스를 위임으로 바꾸기

- **"상속"  대신 "위임" 을 선호하라는 말은 결코 "상속은 나쁘다" 라는 말이 아니다.**

- **처음에는 상속을 적용하고 언제든지 위임으로 전환할수 있어야 한다.**


![](https://velog.velcdn.com/images/wnsqud70/post/e28dea88-f548-444d-8477-cd4a5362b9fc/image.png)


- 비슷한 기능을 하지만 특수한 경우에만 다른 기능을 하는 상속관계 두 클래스가 있다. 서브 클래스는 PreminumExtra 라는 클래스를 참조함 

![](https://velog.velcdn.com/images/wnsqud70/post/7a9b6ae2-7616-4876-a11d-4ed4e58788ed/image.png)



![](https://velog.velcdn.com/images/wnsqud70/post/d9aa92b0-2667-4ff6-ae6b-2f52db12c8f8/image.png)


- 또한 생성자 이외에 **팩토리 메서드**도 만들어준다.

> - ** 팩토리 메서드와 생성자의 큰 차이점은 네이밍에서 자유롭고 return값에 서브클래스 반환 가능.**


![](https://velog.velcdn.com/images/wnsqud70/post/9a05d213-b399-43ae-a256-2d8471035d02/image.png)


- **나중에 최종적으로는 PremiumBooking 을 premiumDelegate로 옮길꺼고 서브클래스 PremiumBooking 을 삭제 예정**

- 왼쪽 클래스의 hasTalkback () 메서드를 오른쪽 클래스로 옮겨준뒤 그것을 호출하도록 만듬

- **오른쪽 클래스는 서브클래스를 대신하는 클래스 , 슈퍼클래스를 상속받지 않고 주입(위임)을 받는다**

- **점점 왼쪽클래스 (PreminumBooking) 클래스는 중재자가 된다.(아무의미 없는 코드)**


![](https://velog.velcdn.com/images/wnsqud70/post/8342fa62-4167-433c-8d6f-f55ccd776510/image.png)
![](https://velog.velcdn.com/images/wnsqud70/post/7bb21d9d-f662-4a5e-a32e-aa8c4e67d5c1/image.png)


- **슈퍼클래스의 hasTalkBack() 메서드에서 premiumDelegate 유무에 따라 실행코드를 좌지우지 해준다.**

- 존재하면 Delegate -> hasTalkBack()  / 없으면 기존코드

- 이렇게 해주면 중재자 역활을 하는 PremiunmBooking - hasTalkBack() 메서드는 필요 없어진다.

- **Delegate가 서브클래스 역활을 함**




![](https://velog.velcdn.com/images/wnsqud70/post/43d60a17-e53a-4319-ac70-fd36724cbdc4/image.png)

- 서브클래스의 **나머지 메서드들도 Delegate 로 옮겨주고 **

- Booking 의 나머지 메서드들도 **특수한경우(Delegate가 있는경우) 다르게 동작**하도록 바꿔주자 


![](https://velog.velcdn.com/images/wnsqud70/post/d4a66e9d-cee8-4402-8743-fabff48418cc/image.png)


- 나머지 메서드 두개도 첫 메서드 처럼 슈퍼클래스에서 Delegate가 있냐 없냐 에 따라 다르게 동작하도록 설정 했다.

- 있으면 실질적 로직이 들어있는 Delegate클래스의 메서드를 사용하도록 했고 없다면 기존 결과 값을 반환 하도록 했다.

- 그리고 **팩토리메서드에서 중재자 역활을 하던 PremiumBooking 클래스(서브클래스) 는 더이상 필요없으므로 지우고 슈퍼클래스만 받아도 된다.(필요한것, 특수한경우 는 Delegate 클래스로 다 옮겼으니까.)**


> -> **특수한 경우에만 다르게 동작할수 있도록 코드를 설정하고 클래스로 빼냈다.**
->** 서브클래스를 다른 클래스로 뺴내기**


 
