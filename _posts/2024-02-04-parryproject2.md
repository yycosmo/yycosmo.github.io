---
title:  "[ParryProject] 클래스 제작 및 기타 기능 구현"
date:   2024-02-04
categories: [ParryProject]
tag: [unity, game, study, 유니티, 게임, 게임개발]
image:
  path: /assets/img/20240204/IMG_20240204_210104_667.jpg
  alt: 뭔가 보여드리겠습니다
---

## **무엇을 했는가**
---

크게 다음을 구현했다:

- 클래스 작성, 상속 구현
- 패링 세부 구현
- 플레이어 이동 보완

### **클래스 작성, 상속 구현**

플레이어, 적 개체의 기초가 되는, 체력과 피격 및 사망이 가능한 개체의 토대로 쓸 Character 클래스<br>
피격이 가능한 오브젝트들을 구현할 IDamageable 인터페이스<br>
공격 오브젝트들의 기초가 될  BaseAttack 클래스

[다음 글](https://kimyir.tistory.com/16)을 참고해서 위 클래스와 인터페이스들을 작성했다.<br>
아직 무엇을 클래스로, 무엇을 인터페이스로 구현하고 상속하는 게 유리한지 감을 잡기 힘들지만, 맨땅에 헤딩하듯이 계속 해 나가다 보면 나만의 기준이 잡힐 거라고 생각한다.

### **패링 세부 구현**

패링을 전담하던 플레이어의 자식 오브젝트의 역할을 플레이어의 공격 전반을 맡도록 설정했다.
이름도 Weapon으로 변경

- 적 투사체 제거시 투사체 데미지만큼 sp 획득
- 스킬 사용시 요구 sp만큼 보유 sp 차감
- 투사체 패링, 적 타격시 이펙트 생성

![sp 수급 및 스킬 사용](/assets/img/20240204/getspandusesp.gif)

투사체만 지우던 기존 패링에서, 제거한 투사체로부터 sp를 수급하고 스킬 사용에 sp를 소모하도록 변경

![패링 및 근접공격 이펙트](/assets/img/20240204/atkFx.gif)

패링 및 근접공격으로 적 타격 시 이펙트 생성 구현.<br>
방향 전환시 이펙트도 좌우 반전이 되서 나오도록 Weapon이 방향 전환을 감지할 수 있게 한 뒤 이펙트를 생성하는 Instatiate 함수에서 반전 여부를 결정해 주었다.
왠지 다른 더 좋은 해결 방안이 있었을 것 같아서 아쉬운 부분. 꾸준히 생각해 봐야겠다.

### **플레이어 이동 보완**

플레이어가 천장에 머리를 부딪힐 시 점프를 중단하고 낙하할 수 있도록 변경

![벽 달라붙기 1](/assets/img/20240204/wall_1.gif)

공중에서 벽을 향해 이동 시 벽에 붙어버리는 현상 발생

![벽 달라붙기 2](/assets/img/20240204/wall_2.gif)

은 Physics Material 2D의 friction을 0으로 설정해서 플레이어의 리지드바디에 붙여서 해결<br>
혹이 이에 대해 코드 차원의 해결 방안이 있는지도 알아볼 것

## **무엇이 문제였나**
---

크게 문제가 됐던 오류는 없었다. 대신 상술했듯 클래스를 구상하는 과정에서 골머리를 싸맸다.<br>
일단 지금 준배해 놓은 것 까지는 구현하고 이후 본격적으로 준비할 때 코드 차원과 상호작용 관해서 자세히 준비를 해 놓아야겠다. 계획의 중요성을 뼈저리게 실감한 시간

플레이어가 플랫폼 끄트머리에 걸쳐있을 때, 공중에 떠 있는 판정이 발생해 점프가 불가능한 현상 발생.
해당 현상은 플레이어의 착지 판정을 콜라이더 하단 위치로 OverlapCircle을 사용해서 판별하는데, 파라미터로 들어간 반지름 값이 작기 때문이었다.<br>
반지름 값을 증가시키면 반대로 플랫폼에서 떨어질 때 잠깐 착지 판정이 유지된다. 또한 점프 중 플랫폼에 딱 붙으면 점프 도중 착지 판정이 발생하기도 한다.<br>
해당 현상은 OverlapBox나 RayCast를 사용해서 착지 판정을 대체하거나, 추가로 다른 해결책을 검색해볼 것

## **무엇을 할 것인가**
---

플레이어 액션은 어느정도 구상한 부분까지 토대가 마련되었으니, 스프라이트로 작업했던 간이 보스를 구현하고자 한다.<br>
그 이후에는 UI와 메인메뉴를 찍먹하듯이 간단하게 구현해보고 전체적인 코드 리펙토링을 할 예정

그 외 중간중간 메모해 놓은 세부 사항은 다음과 같다:

- 카메라 팔로잉
- 참격 패링 관련 매커니즘

## **여담**
---

지금까지 메모장에 작성해 온 일지, 중간중간 떠오르는 개선점, 의문사항, 이후 계획들에 관해서는 노션을 따로 만들어서 그 곳에 정리하는 것이 좋을 것 같다.<br>
언제까지고 노션을 안 쓰면서 아집만 내세울 수는 없을테니까, 사용법 제대로 익힐 겸 해서 말이지.<br>
그 쪽에 정리하는 게 확실히 더 편하고 한 눈에 보기 좋을 것 같다.

{% include embed/youtube.html id='2S3g8CgBG1g' %}
점프 관련 로직을 수정하면서 자료를 찾다가 위 영상을 접하게 되었다.<br>
플랫포머 게임의 점프에 관해서 생각할 수 있는 다양한 요소가 정리되어 있었고, 그걸 구현한 깃허브 링크도 마련되어 있었다.<br>
해당 채널에 플랫포머 게임의 움직임에 관해 다룬 영상들도 있었다. 참고해서 정리하면 아주 유용할 듯.

조만간 블로그 테마 깃허브 들어가서 블로그 사용법 좀 정독해야겠다.<br>
기능이 무궁무진한데 아무것도 안 쓰고 있었네.
