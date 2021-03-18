# 함수

### 함수의 인자로 넘길 수 있는 데이터가 가변적인 경우 -> Asterisks을 사용한다. 튜플로 인식된다.
```python
def foo(first, second, third, *therest):
    print("First: %s" % first)
    print("Second: %s" % second)
    print("Third: %s" % third)
    print("And all the rest... %s" % list(therest))
    print(type(therest))
```
```bash
First: 1
Second: 2
Third: 3
And all the rest... [4, 5]
<class 'tuple'>
```

### 참조
* https://www.learnpython.org/en/Multiple_Function_Arguments
* https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters
