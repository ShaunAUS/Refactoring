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
 
