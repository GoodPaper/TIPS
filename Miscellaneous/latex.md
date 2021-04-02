# Latex

#### Curly bracket 다음에 여러 줄의 수식을 입력하는 경우
* \begin{eqation} 수식을 사용한다.
```
\begin{equation}
  D_{it} =
    \begin{cases}
      1 & \text{if bank $i$ issues ABs at time $t$}\\
      2 & \text{if bank $i$ issues CBs at time $t$}\\
      0 & \text{otherwise}
    \end{cases}       
\end{equation}
```
* Reference
  * https://tex.stackexchange.com/questions/337351/multiple-lines-one-side-of-equation-with-a-curly-bracket/337352
  * https://atom.io/packages/language-pfm

#### Ubuntu에서 pandoc 설치
* https://pandoc.org/installing.html#linux
```bash
$ sudo apt-get install pandoc
```
