# Bernoulli process( trial )

#### Definition
* 어떤 시도의 결과가 2가지로만 나오는 경우를 Bernoulli process( trial )라고 말한다.
* 보통 성공, 아니면 실패의 케이스로 많이 설명한다. 대표적인 것은 동전 던지기.
  * 동전 무한대로 던지면 동전이 세워지는 경우도 있긴 하겠으나... 이 가능성은 없다고 하자. ㅎㅎ

#### PMF, Probability Mass Function, 확률 질량 함수
* 2개의 경우만 있을 수 있기 때문에, 한가지가 나올 수 있는 경우가 p 라고 한다면, 나머지 한개가 나올 수 있는 경우는 1-p 이다.
  * 확률의 합은 1이니...
* 확률 질량 함수, Probability Mass Function, f(x)는 아래와 같다.
\[
\begin{equation}
  f(x) =
    \begin{cases}
      p & \text{if x = 1}\\
      1-p & \text{if x = 0}\\
    \end{cases}
\end{equation}
\]

#### Expected value, Variance
* 베르누이 확률변수의 기대값
  * $E(X) = 1*p + 0*(1-p) = p$
* 베르누이 확률변수의 분산
  * $V(X) = E(X^2) - {E(X)}^2 = p - p^2 = p(1-p) = pq$

#### Reference
* https://m.blog.naver.com/mykepzzang/220838870172
  * 정말 잘 정리되어 있음.
* https://ko.wikipedia.org/wiki/%EB%B2%A0%EB%A5%B4%EB%88%84%EC%9D%B4_%EA%B3%BC%EC%A0%95
