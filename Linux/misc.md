#### 화면에 떠 있는 창의 Process ID를 알고 싶다면?
```bash
# https://askubuntu.com/questions/137875/tell-a-process-pid-by-its-window
$ xprop _NET_WM_PID | sed 's/_NET_WM_PID(CARDINAL) = //' | ps `cat`
```
