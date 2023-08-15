# monicar2
# 1. Tool install on Jetson Termius, pc에서 SSH로 JETSON에 접속하기 위하여 Termius 사용
# 1-1. SSH에서 Wifi 연결하기
# 실행해야할 명령

     sudo nmcli device wifi list
  
     sudo nmcli device wifi connect <ssid_name> password <password>
  
     ifconfig

     
# ![Screenshot from 2023-08-15 02-44-43](https://github.com/jetsonmom/monicar2/assets/92077615/f6f05745-972c-4d5d-a091-34e1b623bcce)

      

# ![Screenshot from 2023-08-15 02-17-35](https://github.com/jetsonmom/monicar2/assets/92077615/a17e7c40-b7e1-4431-80ac-01dbb1986fbc)

# 연결을 해제할 때
     sudo nmcli device disconnect wlan0

  #   1.2 Cooling Fan

  # 4선 PWM 쿨링팬은 아래 작업을 해야 동작합니다. 즉 PWM 신호에 출력을 주어야 동작하는 것입니다. CPU 사용에 따라 쿨링팬 속도를 자동으로 조정하는 utility를 설치하는게 좋습니다.

    cd Downloads
    git clone https://github.com/jetsonworld/jetson-fan-ctl.git
    cd jetson-fan-ctl

    sudo sh install.sh


# 1.3  jtop 
   # ![Screenshot from 2023-08-15 08-59-14](https://github.com/jetsonmom/monicar2/assets/92077615/03c0d151-ac7c-4663-81cc-b9af53ba8abb)

 sudo apt install python3-pip
 
 sudo -H pip3 install -U jetson-stats
 
# 1.4   I2 C 장치 연결 확인   

     i2cdetect -y -r 1
  
#  ![Screenshot from 2023-08-15 04-02-59](https://github.com/jetsonmom/monicar2/assets/92077615/33d4a7f4-0217-42b6-b02d-5b6d38002882)



# 2. ROS Foxy 설치

#  2.1 ROS Foxy 설치
      cd ~/Downloads

      git clone https://github.com/zeta0707/installROS2.git

      cd installROS2

      ./install-ros2.sh
