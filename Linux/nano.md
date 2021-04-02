# nano

#### Nano에서 여러 줄을 삭제하려면?
왜 찾아 보았는가?
*  Cron script를 Editing 하기 위해 crontab -e 를 하면 Default editor가 nano인데, nano 사용법을 잘 몰랐고, 여러줄을 한번에 삭제하는 방법을 몰라서 찾아봄.
* https://askubuntu.com/questions/154431/how-do-i-delete-multiple-lines-in-nano-without-affecting-the-clipboard
##### 방법
1. <kbd>Ctrl</kbd> * <kbd>Shift</kbd> * <kbd>6</kbd> : 블럭 설정 시작
2. 방향 키로 블럭 지정
3. <kbd>Ctrl</kbd> * <kbd>K</kbd> : 블럭 삭제 ( Cut 인지 Delete ?? )
