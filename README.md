# DevHack
개발중 가끔 필요한 각종 짧은 예제 및 꿀팁 레포 입니다.


## 리눅스

 
- 노트북 덮개(뚜껑, 커버) 닫아도 안꺼지게 하기
  - /etc/systemd/logind.conf
  - #HandleLidSwitch=suspend
    - lock      : 모니터만 끄기
    - poweroff  : 전원 끄기
    - hibernate : 최대 절전모드
    - ignore    : 아무것도 안함
  - systemctl restart systemd-login.service



