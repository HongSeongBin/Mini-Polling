## 설계

#### 기능 목록

: 가장 기본적인 기능들을 바탕으로 구성

**1. 회원 기능**
* 회원 등록 (회원가입)
* 로그인
* 로그아웃


**2. 설문기능**
* 설문 생성
* 설문 전체 목록 조회
* 설문 조회 (자신이 생성한 것)
* 설문 조회 (자신이 투표한 것)
* 설문 실시
* 설문 삭제


**3. 기타 요구사항**
* 조회에서는 원하는 내용을 바탕으로 검색 가능
* 설문 생성은 객관식, 주관식 두가지 타입으로 가능


**4. 추가 사항**

: 만약 위의 기능들을 구현하고 시간이 남을 경우 (아마 그러긴 힘들지 않을까..) 고려해둔 사항들

* 카테고리 별로 분류
* 설문 결과에 대해 다양한 형태의 그래프로 시각화

<br/>



#### 도메인 설계

**Class Diagram**

: 여러가지를 생각했는데 어떤 것이 맞을까..

![1차본](https://user-images.githubusercontent.com/31160622/102178685-31e00880-3ee9-11eb-9bd5-d4761ac9e178.PNG)

: 초기에 위와 같이 생각하였으나 대답의 경우도 주관식과 객관식에 따라 다른 형태를 띄기에 수정이 필요하다고 느낌

<br/>


![2차본](https://user-images.githubusercontent.com/31160622/102178693-34daf900-3ee9-11eb-849c-e10c091a8872.PNG)

: 위와 같이 생각하였는데 현재로써 문제점이 눈에 뛰지는 않았으나 조금 이상하다는 느낌이 든다.... 

거기다 질문과 대답의 경우 상속을 이용하였는데 부모가 자식에게 상속할 어트리뷰트가 없을 것 같은데 상속으로 표현하는게 좋을지의 여부도 잘 모르겠다...

<br/>


![2차본_2](https://user-images.githubusercontent.com/31160622/102178697-373d5300-3ee9-11eb-8acd-afff004efb32.PNG)

: 상속을 제외한 상태로 구성을 해보았다. 위의 저녀석과 밑의 녀석 중 뭐가 나을까... 지금 생각하였을 때는 각각의 관계는 상속으로 표현할 수 있는 관계가 맞고 상속 시켜주는 어트리뷰트가 현재 없다하더라도 미래에 어떻게 될지 모르고 관계를 표현할 때에도 조금 더 좋다고 판단하여 현재는 상속을 이용하여 표현한 녀석을 선택.

또 한가지 의문점은 생성(has)의 관계에서는 회원과 설문은 일 대 다 관계인 것 같으나 투표(vote)의 관계에서 생각하면 회원과

<br/>


### 추가사항!

: 문제점을 발견! 회원이 설문을 만드는 데는 일대다 관계가 맞으나 회원이 설문을 투표하는 데에는 다대다 관계야! 

-> 투표를 위한 녀석을 따로 만들어주고 다대다 관계를 풀어줄 수 있어야해!!

![최종클다](https://user-images.githubusercontent.com/31160622/102217070-6a023e00-3f1f-11eb-8976-aab6b8d922e6.png)

<br/>



#### 위의 Diagram 을 바탕으로 Attribute 를 추가한 class diagram
![class_Digram](https://user-images.githubusercontent.com/31160622/102184972-aa4bc700-3ef3-11eb-89c3-6f1ba7ed97e9.png)


<br/>


#### 현재까지 최종수정 본
![final_](https://user-images.githubusercontent.com/31160622/102294254-3c071300-3f8c-11eb-84df-af75a1116314.png)

<br/>



**위의 결과물에 대해서 확신이 들지 않으므로 리뷰시간 후 피드백을 바탕으로 수정할 것!!**

<br/>



#### Database Architecture

: 오늘까지 들은 피드백을 바탕으로 E-R Diagram 최종 그릴 것

  ( 상속이 남아있다면 JPA 상속 매핑 방법 중 Single Table 방법 사용. MappedSuperclass, Single table, Joined table, Table per class 등 여러 방법이 있으나 그 중 가장 성능상에서 이점을 보이는 것은 Single table이며 default 옵션이기도 하기에 선택)

<br/>



#### UI Design

: 전체적인 디자인은 일반적인 웹페이지 게시판의 형태를 띄고 있습니다. 

* 처음 접속화면

![ui1](https://user-images.githubusercontent.com/31160622/102196091-c3a83f80-3f02-11eb-95ad-eb2e1c6d31d7.PNG)

: 간단한 어플리케이션을 소개하는 문구를 메인으로 위와 같은 디자인을 생각하고 있습니다. 

<br/>


* 설문등록화면

![ui2](https://user-images.githubusercontent.com/31160622/102196149-d91d6980-3f02-11eb-9fc0-817bca218045.PNG)

: 객관식, 주관식을 선택해서 질문을 추가할 수 있으며 이를 바탕으로 등록

<br/>


* 설문목록 화면

![ui3](https://user-images.githubusercontent.com/31160622/102196162-db7fc380-3f02-11eb-9de6-f29bb4f89f67.PNG)

: 현재까지 등록된 설문 목록들을 볼 수 있으며 설문을 참여하지 않았을 경우 참여가, 참여하였을 경우 결과가 화면에 띄어집니다.

  또한 원하는 내용을 바탕으로 검색을 진행할 수 있습니다.
  
<br/>


* 메인화면 상단의 메뉴 (로그인 하였을 경우)

![ui5](https://user-images.githubusercontent.com/31160622/102196180-e0dd0e00-3f02-11eb-9e27-e094cae2e3ec.PNG)

: 위의 그림처럼 로그아웃과 내설문목록을 확인할 수 있습니다.

<br/>


* 메인화면 상단의 메뉴 (로그인 하지 않았을 경우)

![ui4](https://user-images.githubusercontent.com/31160622/102196175-de7ab400-3f02-11eb-95d6-11f448f2a159.PNG)

: 위의 그림처럼 로그인과 회원가입을 확인할 수 있습니다.

<br/>


* 회원가입

![ui6](https://user-images.githubusercontent.com/31160622/102196191-e5a1c200-3f02-11eb-818e-965ac095c4a8.PNG)

: 회원가입에 필요한 사항을 입력한 후 간단하게 username 중복검사만 거친 후 회원가입을 진행할 수 있습니다.

<br/>



* 로그인

![ui7](https://user-images.githubusercontent.com/31160622/102196206-e9cddf80-3f02-11eb-9610-c13b6bfb3765.PNG)

: 로그인화면입니다!
