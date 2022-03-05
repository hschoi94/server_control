# server_control
openmediavault가 설치된 debian에서 vscode을 이용하여 코드작성 후, 다른 서버에 코드를 전달하거나 환경을 전달하여 실행기능

## debian에서 사용할 vscode 설정

As per: https://stackoverflow.com/questions/60507713/vscode-remote-ssh-connection-failed

On the OMV server, 

set:
AllowTcpForwarding yes

in /etc/ssh/sshd_config

then 

restart the ssh service:
service sshd restart

delete the vs folder

rm -rf .vscode-server/

## 다른 서버 설정
 - Wake On Lan: 작업이 있을 시 켜져야 함.
 - docker: 실행할 코드에서 활용할 환경구성
 ```
 wakeonlan $MAC_ADDR 
 ```
 port number 지정
 ```
 -p $PORT_NUM
 ```

## docker에서 환경 구성 뒤, 실행
### --entrypoint 옵션

--entrypoint 옵션은 Dockerfile의 ENTRYPOINT 설정을 덮어쓰기 위해서 사용합니다.

예를 들어, python:3.8-alpine 이미지로 부터 python --version을 실행하고 싶다면 다음과 같이 커맨드를 실행하면 됩니다.

```
docker run --entrypoint python python:3.8-alpine --version
```

volume을 지정하고 실행할 환경에서 실행할 수 있도록 코드를 작성하여 실행
```
docker run -v volume_path:path
```
코드 실행 끝에 컨테이너가 종료될 수 있도록 함.
```
exit
```
컨테이너 사용후, 부가적인 것을 제거.
```
docker run --rm -it wernight/funbox nyancat
```