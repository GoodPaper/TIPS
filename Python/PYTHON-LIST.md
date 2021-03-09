# 리스트

### slice 방법
start : stop(혹은 end) : step 형태로 사용한다.
유념해야 할 것은... end는 end부터 포함하지 않겠다는 의미이지, end가 포함되는 것까지를 의미하는 것이 아니다.
```pythonregexp
a[start:end] # start부터 end-1까지의 item
a[start:]    # start부터 리스트 끝까지 item
a[:end]      # 처음부터 end-1까지의 item
a[:]         # 리스트의 모든 item
a[-1]        # 맨 뒤의 item
a[-2:]       # 맨 뒤에서부터 item2개
a[:-n]       # 맨 뒤의 item n개 빼고 전부
```

### 기존 리스트에 아이템 **1**개 아이템 추가 -> append()
```pythonregexp
>>> A = [1, 2]
>>> A.append(3)
>>> A.append(4)
>>> A

[1, 2, 3, 4]
```

### 기존 리스트에 다른 리스트를 덧붙이는 경우 -> extend()
```pythonregexp
>>> A.extend([5, 6, 7])
>>> A.extend((8, 9))
>>> A

[1, 2, 3, 4, 5, 6, 7, 8, 9]

>>> A.extend(range(11, 14))
>>> A

[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
```

### 리스트를 튜플로 변경하고 싶으면? -> tuple()
```pythonregexp
>>> A = tuple(["A", "B"])
>>> A

('A', 'B')
```

### 리스트에 있는 중복된 아이템을 제거하려면? -> set() 사용
```pythonregexp
>>> t = [1, 2, 3, 1, 2, 5, 6, 7, 8]
>>> t
[1, 2, 3, 1, 2, 5, 6, 7, 8]

>>> list(set(t))
[1, 2, 3, 5, 6, 7, 8]
```

### 기타
* list와 tuple의 차이: mutable, hash

### 참조
* http://hashcode.co.kr/questions/74/%ED%8C%8C%EC%9D%B4%EC%8D%AC-slice-notation-%EC%93%B0%EB%8A%94%EA%B1%B0%EC%A2%80-%EC%95%8C%EB%A0%A4%EC%A3%BC%EC%84%B8%EC%9A%94
* https://stackoverflow.com/questions/20196159/how-to-append-multiple-values-to-a-list-in-python
* https://stackoverflow.com/questions/7961363/removing-duplicates-in-lists
* https://stackoverflow.com/questions/2643850/what-is-a-good-way-to-do-countif-in-python
