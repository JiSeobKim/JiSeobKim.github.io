---
layout: post                       
title: "Swift - 타입 메소드 & 인스턴스 메소드"
categories: [Swift]
---

Swift 코드를 보다 그런적이 있었다.

"이건 분명 클래스인데, 인스턴스를 안만들고 함수를 쓰네??"



오늘 나오는 메소드의 종류 다음과 같다.

1. 인스턴스 메소드
2. 타입 메소드

<br>

# 메소드의 종류
아래의 이미지를 보자!

![](https://raw.githubusercontent.com/JiSeobKim/jiseobkim.github.io/master/static/img/_posts/2018-10-05/img1.png)
(App: Scapple)

오늘의 추천앱! Scapple이란 앱이에요!!

블로그도 리뉴얼 했으니 추천 카테고리도 만들어야지 ㅎㅎ

<br>
다시 본론으로 넘어가서!

구성은 다음과 같다
- 함수
- 클래스1
  - 함수1
  - 함수2
- 클래스2
  - 함수3
  - 함수4

여기서, **함수는 전역 함수다**. 즉, 어디서든 접근이 가능하다는 의미이다!

만약 지금 클래스1의 내부에 코드를 작성하고 있다면,

**클래스1이 2를 상속하고 하고 있다**거나 **클래스2의 인스턴스를 만들었다면**

클래스2 내부의 함수3,4를 접근할 수 있지만 **그 외엔 불가**하다. 하지만 우리의 <u>전역 함수님에겐 언제든 접근이 가능</u>하다!

<br>

그렇담 일반적 접근인 **인스턴스 메소드**를 보자.

<br>

## 인스턴스 메소드

---



```swift
class SomeClass {

    var something: String?

    func useInstance() -> String {
        return "Instance!!"
    }
}
```



위처럼 만들고 사용은 어떻게?

이렇게

![](https://raw.githubusercontent.com/JiSeobKim/jiseobkim.github.io/master/static/img/_posts/2018-10-05/img2.png)



'some'이란 인스턴스를 만들어주고, some의 내부함수인 useInstance()를 호출하여 값을 받아냈다.

중요한건, **<u>인스턴스를 만들고 내부함수 호출</u>**이다.

그렇담!! 인스턴스를 안만들고 호출을 하는 방법은?

<br>

## 타입 메소드

---





타입 메소드란 타입(여기선 some클래스를 의미) 자체에서 호출을 할 수 있는 메소드이다.
그건 케바케이겠지만? 우선, 책에서 본건 이런게 있었다
1. 사각형 면 숫자 return 하기
2. 괴물 울음 소리

다소 어이없는 예들이지만 공통점은 있다. 당연한 값들이란것 !
코드적으로 본다면 인자값 넣고 그

말이 낯설어서 이해가 안될수도 있다. 필자도 이번기회에 외움! 이 맛에 포스팅한다.

내용만 알아도 된다. 이름이야뭐... 일단 이해하는게 중요하니 설명부터!



일반 내부 함수랑 차이가 거의 없다 있다면 **키워드** 하나가 더붙는다는것?

`static`  또는 `class` 이다.



일반 책에서 잘나오지 않아서 굉장히 낯설었다... 나의 함수들은 func으로만 시작하였고,

그 앞에 뭐가 붙는다는건 상상도 못해봤다. 심지어 한개도 아니고 두개다(사실 하나 더 있다.)(내가모르는게 더있을수도?)





우선, `class` 부터 보자


<br>
### 키워드 : class

일단 코드부터 보자





```swift
class SomeClass {
    // 인스턴스 메소드
    func useInstance() -> String {
        return "Instance!!"
    }
    // 타입 메소드
    class func getSomething() -> String{
        return "Type!!"
    }
}
```



처음 저것을 보았을때, 신선한 충격이었다. 클래스는 클래스고 함수는 함수지 왜 한줄에 다있는걸까? 라고...

우선 일반적인 클래스랑 쓰임새가 다른건 확실하다!

그럼, 메인에서 일반적으로 사용을 해보자 (인스턴스 메소드 사용!)



![](https://raw.githubusercontent.com/JiSeobKim/jiseobkim.github.io/master/static/img/_posts/2018-10-05/img3.png)



없다. 완소 기능인 자동 완성 기능에 없다...

그렇다, 타입 메소드로 지정한것은 인스턴스 메소드처럼 사용이 불가능하다.

그럼, 이제 사용해보자.

![](https://raw.githubusercontent.com/JiSeobKim/jiseobkim.github.io/master/static/img/_posts/2018-10-05/img4.png)



됐다. 인스턴스를 안만들었음에도 불구하고, 사용이 가능하였다!!
그럼 이제 이걸 언제쓰냐가 궁금해질것이다. 책에서 본것들은 이런게 있었다.
1. 괴물 울음소리 String받기
2. 사각형 면수 받기 

귀여움이 가득한 예제들이었다. 
1의 경우 괴물의 울음소리를 언제 어디서든 인스턴스 없이 가져왔고
2의 경우는 사각형 면수인 4를 가져오는 것이었다.

공통점으론 당연한 것이었다. 어떻게 쓰냐에 달렸다.

<br>
#### 키워드 class의 장점

필자는 이런 경우도 보았다. 통신, UIView가져오기 등등
따로 인스턴스를 만들지 않고 바로 바로 처리를 한 것들을 보았다.

특정 반복되는 뷰라던가, 인자값으로 받아서 통신을 하고 델리게이트 패턴을 이용해 반복적으로 일어나는것을 처리하였다.

그런점들이 좋았던거 같다. 인스턴스를 생성하면 이게 해제가 될지도 걱정을 안해도되고 (평소에도 잘안하긴했다..) 고로 ARC 걱정이 없을것 같다.

다른 것들은 기억이 안난다, 단점으로 가자.

<br>
#### 키워드 class의 단점

음 확장성이 안좋았다. 아니 없었다.
당연한 값들로만 리턴을 한다? 근데 초기화가 안되어있어서 변수를 쓰지도 못한다.
내부의 변수를 사용할 수 없단건 정말 확장성에서 힘들었던거 같다. 다른 사람이 해둔 코드에 내가 변수 하나 추가해서 작업하고 싶은데, 그게 안된다;;;
파라미터를 하나 추가한다? 그럼 모든 그 함수에 추가 시켜버려야한다...

<br>
### 키워드 : static

무엇이 다른걸까?

우선! 위에 타입메소드의 특징?들은 똑같다. 그런데


오버라이드가 가능, 불가능이다.


```swift
class SubClass: SomeClass {
    override class func getSomething() -> String{
        return "wow"
    }
}
```
이걸 먼저 보자, `class func` 앞에 `override`가 붙었다!
키워드가 굉장히 길다.. 그렇지만 오버라이드 개념만 안다면 쉽게 이해할거라 생각한다.

결과도 보자

![](https://raw.githubusercontent.com/JiSeobKim/jiseobkim.github.io/master/static/img/_posts/2018-10-05/img5.png)

굉장히 잘 덮어썼다.

그럼, 이제 살짝 바꿔서 `class`대신 `static`을 써보자

![](https://raw.githubusercontent.com/JiSeobKim/jiseobkim.github.io/master/static/img/_posts/2018-10-05/img6.png)


오오 빨간색이다. **스태틱 메소드라고 오버라이드가 안된다한다**

<br>
그렇다, 큰 차이는 없지만 차이는 분명한 두가지 키워드였다!

> class 키워드를 써도 오버라이드를 막을수 있다.
> `final` 키워드를 `class` 키워드 앞에 붙이면 된다!!
> 키워드 많은건 내 취향이 아니니 나는 static을 쓰겠다.

# PS
처음엔 참 낯선 용어들이었는데, 블로그를 쓰니 머리에 더 들어오는 것 같아서 좋다.



 



