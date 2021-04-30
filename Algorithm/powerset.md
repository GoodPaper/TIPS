# Powerset, 멱집합

#### Definition
주어진 집합에서 나올수 있는 모든 부분 집합들로 구성된 집합이다. 공집합도 포함한다. 영어로는 Powerset 이라고 부른다.

#### Example
```python
import itertools

func = itertools.combinations

def powerset( x ):

  w = set()
  for s in range( len( x ) + 1 ):
    a = func( x, s )
    w.update( set( a ) )
  return sorted( w )

print( powerset( [ 1, 2, 3 ] ) ) # [(), (1,), (1, 2), (1, 2, 3), (1, 3), (2,), (2, 3), (3,)]
print( powerset( '17' ) ) # [(), ('1',), ('1', '7'), ('7',)]
print( powerset( '011' ) ) # [(), ('0',), ('0', '1'), ('0', '1', '1'), ('1',), ('1', '1')]

# 응용. 순서가 의미가 있는 Permutations를 사용하면...
func = itertools.permutations
print( powerset( [ 1, 2, 3 ] ) ) # [(), (1,), (1, 2), (1, 2, 3), (1, 3), (1, 3, 2), (2,), (2, 1), (2, 1, 3), (2, 3), (2, 3, 1), (3,), (3, 1), (3, 1, 2), (3, 2), (3, 2, 1)]
print( powerset( '17' ) ) # [(), ('1',), ('1', '7'), ('7',), ('7', '1')]
print( powerset( '011' ) ) # [(), ('0',), ('0', '1'), ('0', '1', '1'), ('1',), ('1', '0'), ('1', '0', '1'), ('1', '1'), ('1', '1', '0')]
```

#### Reference
* https://stackoverflow.com/questions/1482308/how-to-get-all-subsets-of-a-set-powerset
* https://ict-nroo.tistory.com/51
