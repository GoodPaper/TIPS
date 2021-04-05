# string

#### encode, error
* 왜 찾아보았는가?: 인터넷 문서는 여러 언어로 이루어져있는데, 이를 1개 언어로 Normalize 하려면, HTML Escape, Unicode encoding, decoding 과정이 필요하다. 이 과정에서 찾아봄.
* 여기서는 encoding 보다는 error에 집중한다.
```python
# string.encode( encoding = encoding, errors = errors )
#errors
#  'backslashreplace': 백슬래시 기호로 표시
#  'ignore': 해당 글자 무시
#  'namereplace': 해당 글씨를 정해진 설명으로 변경
#  'strict': 예외 발생
#  'replace': 물음표로 변경
#  'xmlcharrefreplace': xml 기호로 표시

txt = "Aåpl"
print( txt.encode( encoding="ascii", errors = "backslashreplace" ) )
print( txt.encode( encoding="ascii", errors = "ignore" ) )
print( txt.encode( encoding="ascii", errors = "namereplace" ) )
print( txt.encode( encoding="ascii", errors = "replace" ) )
print( txt.encode( encoding="ascii", errors = "xmlcharrefreplace" ) )

b'A\\xe5pl' # backslashreplace
b'Apl' # ignore
b'A\\N{LATIN SMALL LETTER A WITH RING ABOVE}pl' # namereplace
b'A?pl' # replace
b'Aåpl' # xmlcharrefreplace
```
* https://www.w3schools.com/python/ref_string_encode.asp

#### 문자열 안에 있는 punctuation 일괄 제거
* str.maketrans 사용
```bash
maketrans(x, y=None, z=None, /)
    Return a translation table usable for str.translate().

    If there is only one argument, it must be a dictionary mapping Unicode
    ordinals (integers) or characters to Unicode ordinals, strings or None.
    Character keys will be then converted to ordinals.
    If there are two arguments, they must be strings of equal length, and
    in the resulting dictionary, each character in x will be mapped to the
    character at the same position in y. If there is a third argument, it
    must be a string, whose characters will be mapped to None in the result.
```
```python
>>> import string
>>> t = str.maketrans( '', '', string.punctuation ) # 반환되는 t는 dict 이다. key는 Integer
>>> print( 'show-me.the?money!'.translate( t ) )
showmethemoney
```
* https://stackoverflow.com/questions/34293875/how-to-remove-punctuation-marks-from-a-string-in-python-3-x-using-translate/34294398
