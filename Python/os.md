# OS

#### 새로 디렉토리 만들때, 하위 디렉토리까지 만드는 방법
* exist_ok 를 True로 설정한다. Default는 False
* 만드려는 디렉토리 path 안에, 이미 File system에 그 디렉토리가 있는 경우, exist_ok = False 이면 Error가 발생한다.
```python
>>> os.makedirs( 'path', exist_ok = True )
>>> help( os.makedirs )
...
makedirs(name, mode=511, exist_ok=False)
    makedirs(name [, mode=0o777][, exist_ok=False])

    Super-mkdir; create a leaf directory and all intermediate ones.  Works like
    mkdir, except that any intermediate path segment (not just the rightmost)
    will be created if it does not exist. If the target directory already
    exists, raise an OSError if exist_ok is False. Otherwise no exception is
    raised.  This is recursive.
```
