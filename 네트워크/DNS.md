# DNS

## Domain Name

IP주소를 사람이 이해하기 쉽게 문자 형식으로 나타낸 것.

도메인 네임을 컴퓨터가 이해할 수 있도록 IP 주소로 변환해주는 시스템이 바로 DNS(Domain Name System)이다.
<br/>
<br/>

+) 주소창에 www.naver.com을 치면 일어나는 일 ...
![image](https://user-images.githubusercontent.com/97162920/174620229-2ee3eaa6-c9e3-424e-99c4-823b8f9ef2ac.png)

## DNS Round-Robin

DNS 서버 구성 방식 중 하나

### Round-Robin

![image](https://user-images.githubusercontent.com/97162920/174620683-bf06cbd5-18c7-4fd6-a7e2-39d2ee497cbc.png)
대표적인 스케줄링 기법

- 선점형 스케줄링
- 우선순위를 두지 않음
- 들어오는 순서대로, 주어진 시간만큼 돌아가면서 실행

DNS를 RR로 구성할 경우 로드밸런서가 필요 없다!

하지만 다음과 같은 단점이 있다.

- 서버의 수만큼 공인 IP의 수가 필요하다
- 균등하게 분산되지 않는다
- 서버가 다운되어도 확인할 수 없다

다음과 같은 방법으로 극복할 수 있다.

- 다중과 구성 방식
- 가중치 편성 방식
- 로드밸런스를 도입한 최소 연결 방식
<br/>

위 내용에 대해 더 자세하게 알고싶다면 - 
[DNS round robin 방식이란? - Problem/Question (fc2.com)](http://dailusia.blog.fc2.com/blog-entry-362.html)

---

## 로드 밸런싱
서비스의 규모가 커지고 이용자 수가 많아지면 기존의 서버로 원활한 서비스를 제공하기 어려워진다.
이때 **scale-up** 혹은 **scale-out** 방식으로 문제를 해결할 수 있다.
- scale-up: 기존 서버의 성능을 UP 시키는 방식
- scale-out: 기존 서버와 동일하거나 낮은 수준의 서버를 증설하는 방식

scale-out 방식을 사용하려 한다면, 로드 밸런싱으로 여러대의 서버에 트래픽을 균등하게 분산해줘야 한다.
![image](https://user-images.githubusercontent.com/97162920/174621324-eefe3bdf-5495-4f2b-9b5c-da22d84653de.png)

### L4 로드밸런서와 L7 로드밸런서 

![image](https://user-images.githubusercontent.com/97162920/174622844-da08064f-68f3-4351-8b23-48b8e01a6fe8.png)

참고블로그
https://tecoble.techcourse.co.kr/post/2021-11-07-load-balancing/
