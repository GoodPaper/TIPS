# Regular Expression
* https://www.regextester.com/

##### 둥근 괄호( Parenthesis ) 안에 있는 내용
```javascript
\(([^)]+)\)
```
* **(NYSE:ACI)**, EQT Corporation **(EQT-IR)**

##### 중괄호[ Square bracket ] 안에 있는 내용
```javascript
\[([^)]+)\]
```
* **[Nasdaq:LMT]**

##### 특정 단어 뒤 Capital Alphabet
```javscript
symbol \w[A-Z]+\w // symbol 뒤 Capital alphabet

:\s+\w[A-Z]+ // : 뒤 Capital alphabet
```
* (NYSE) under the **symbol EFX**.
* TSX/NYSE/PSE<strong>: MFC</strong> SEHK: 945
