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

- USB 장치 별칭(별명) 생성 또는 이름 고정
  - lsusb
    - VendorID : Product ID를 확인할 수 있음
    
  - udevadm info -a -n /dev/장치이름 | grep '{serial}' | head -n1
    - serial ID를 확인할 수 있음.
      - 아직 alias에 serial ID 적용해서 성공한 적 없긴 함 ㅎㅎ;;

  - cd /etc/udev/rules.d
  - sudo gedit 99-usb-serial.rules
    - SUBSYSTEM=="tty", ATTRS{idVendor}=="XXXX", ATTRS{idProduct}=="XXXX", ATTRS{serial}=="XXX...X", SYMLINK+="별명"
      - 별명에 짓고싶은 이름 넣으면 됨.

  - sudo udevadm control --reload-rules
    - 위 명령어 입력 후 장치 뺐다가 다시 끼고나서 동작 확인하기


## 라즈베리파이

- 한글 깨짐 관련
  - sudo apt install -y fonts-unfonts-core
    - 여기까지 하면 읽기만 가능
  - sudo apt install ibus-hangul
    - 여기까지 하면 쓰기도 가능

- Conky (실시간 리소스 모니터링 툴) 설치
  - sudo apt-get install conky -y
  - wget -O /home/pi/.conkyrc https://raw.githubusercontent.com/novaspirit/rpi_conky/master/rpi3_conkyrc
  - sudo vim /usr/bin/conky.sh
    <pre>
    <code>
    #!/bin/sh
    (sleep 4s && conky) &
    exit 0
    </code>
    </pre>
  - sudo vim /etc/xdg/autostart/conky.desktop
    <pre>
    <code>
    [Desktop Entry]
    Name=conky.desktop
    Type=Application
    Exec=sh /usr/bin/conky.sh
    Terminal=false
    Comment=system monitoring tool.Categories=uTility;
    </code>
    </pre>
  - sudo reboot

## ROS

- 라즈베리파이에 ROS Melodic 설치중 오류 (gpg: keyserver receive failed: No name)
  <pre>
  <code>
  sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
  </code>
  </pre>
  위의 명령어에서 오류가 발생하면 keyserver를 바꿔서 아래의 명령어를 돌려보자.
  <pre>
  <code>
  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
  </code>
  </pre>
