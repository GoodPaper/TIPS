# Interleaving string.
* 2개의 문자열을 특정 순서대로 조합해서 주어진 문자열을 만들 수 있는지 확인하는 문제
* 입출력 예제는 아래와 같음.
```
# Case 1
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true

# Case 2
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false

# Case 3
Input: s1 = "", s2 = "", s3 = ""
Output: true
```
## 제약 사항
  * 0 <= s1, s2의 길이 <= 100
  * 0 <= s3 <= 200
  * s1, s2, s3는 전부 소문자로 구성

## 답변
```python
def func( s1: str, s2: str, s3: str ) -> bool:

    
```