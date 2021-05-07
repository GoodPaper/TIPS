# uWSGI

### What is this?
WSGI. Web Service Gateway Interface. 웹 어플리케이션의 인터페이스.<br/>
보통 uWSGI는 NginX, Apache와 같이 사용하고는 하는데... 그럼 NginX, Apache가 있어야 무조건 외부와 통신할 수 있는 것 아니냐? 그건 아니다. uWSGI만으로도 서비스는 가능하다.<br/>
NginX와 같은 HTTP Server를 사용하는 이유는, Load balancing, Static resource 접근 제어 등, 여러 좋은 기능을 HTTP 서버가 제공하기 때문이지, 무조건 이거랑 붙여서 사용해야만 한다는 것은 아님.

### Options
옵션(로그, 프로세스 개수 등...)이 매우 많으니, 직접 문서를 확인하고 필요한 것을 가져다 사용할 것.
  * https://uwsgi-docs.readthedocs.io/en/latest/Options.html

### Register to systemd
Emperor를 이용해서 등록할 수 있다. Service 파일을 만들어야 한다.( /etc/systemd/system/OOO.uwsgi.service )
* http://uwsgi-docs.readthedocs.io/en/latest/Systemd.html
반드시 Emperor를 사용해야 하는 것은 아니다. 공식 문서에도 Single application 별로 등록할 수 있다고 나와 있다. Service 스크립트 만들고 등록만 하면 됨.( 당연히 NginX도 systemd로 돌고 있어야 외부에서 접속이 가능함.)
* https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-16-04

### Emperor? ( Multi applications deployment )
* http://uwsgi-docs.readthedocs.io/en/latest/Emperor.html

### Configure with NginX
* http://uwsgi-docs.readthedocs.io/en/latest/Nginx.html

### websocket 구현체와 연결할 때, Multi process를 사용하면 안되는 이유는? ( TODO )
(Flask - SocketIO 패키지를 사용했을 때만 해당되는지는 모르겠으나...) uWSGI 실행 옵션에 Process를 여러개 띄우는 것을 설정하면, Web socket이 Connection 되지 않는다.

실험 결과, 실제로 전부 Connection 시도 하자마자, disconnect가 되어 버리고, 여기에 제기된 이슈도 동일한 상황으로 발생된 것으로 생각된다.

그럼 왜 Multi process로 구동하면 Web socket 기능이 사용될 수 없는 것인가...?
* Flask - SocketIO Extension 문제인가?
* uWSGI - Flask 문제인가?
* Web socket 동작성에 기반하여, Multi process로의 연결이 불가능한 것인가...?

### ETC
* [inetd, xinetd를 이용하여 on demand로 network 프로세스를 시작하는 것을 적용하는 방법](https://uwsgi-docs.readthedocs.io/en/latest/Options.html)
