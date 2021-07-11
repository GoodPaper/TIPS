# function, method

### args, kwargs
* https://www.learnpython.org/en/Multiple_Function_Arguments
* https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters
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

### decorator
Sort of method wrapper
* http://abh0518.net/tok/?p=604
```python
import time

def how_long_does_it_take( func ):

    def wrapper( *args, **kwargs ):

        a = time.time()
        b = func( *args, **kwargs )
        return b, time.time() - a

    return wrappe

@how_long_does_it_take
def dummy():

    time.sleep( 3.0 )
    return 1


if __name__ == '__main__':

    rest, elapsed = dummy()
    print( rest, elapsed )
```