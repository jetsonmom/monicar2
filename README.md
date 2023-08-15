# monicar2
# 1. Tool install on Jetson Termius, pc에서 SSH로 JETSON에 접속하기 위하여 Termius 사용
# 1-1.   SSH에서 Wifi 연결하기
# 실행해야할 명령

     sudo nmcli device wifi list
  
     sudo nmcli device wifi connect <ssid_name> password <password>
  
     ifconfig

     
# ![Screenshot from 2023-08-15 02-44-43](https://github.com/jetsonmom/monicar2/assets/92077615/f6f05745-972c-4d5d-a091-34e1b623bcce)

      

# ![Screenshot from 2023-08-15 02-17-35](https://github.com/jetsonmom/monicar2/assets/92077615/a17e7c40-b7e1-4431-80ac-01dbb1986fbc)

# 연결을 해제할 때
     sudo nmcli device disconnect wlan0

  #   1.2    Cooling Fan

  # 4선 PWM 쿨링팬은 아래 작업을 해야 동작합니다. 즉 PWM 신호에 출력을 주어야 동작하는 것입니다. CPU 사용에 따라 쿨링팬 속도를 자동으로 조정하는 utility를 설치하는게 좋습니다.

    cd Downloads
    git clone https://github.com/jetsonworld/jetson-fan-ctl.git
    cd jetson-fan-ctl

    sudo sh install.sh

#  
# 1.3    jtop 
   # ![Screenshot from 2023-08-15 08-59-14](https://github.com/jetsonmom/monicar2/assets/92077615/03c0d151-ac7c-4663-81cc-b9af53ba8abb)

 sudo apt install python3-pip
 
 sudo -H pip3 install -U jetson-stats
 
# 1.4    I2 C 장치 연결 확인   

     i2cdetect -y -r 1
  
#  ![Screenshot from 2023-08-15 04-02-59](https://github.com/jetsonmom/monicar2/assets/92077615/33d4a7f4-0217-42b6-b02d-5b6d38002882)



# 2.    ROS Foxy 설치

#  2.1    ROS Foxy 설치
      cd ~/Downloads

      git clone https://github.com/zeta0707/installROS2.git

      cd installROS2
      
      ./install-ros2.sh   #ROS를 install하기 위해서는 internet access가 필요합니다.

# jetson@nano:~/Downloads/installROS2$ ls
# install-ros2.sh  README.md  ros2_turtlesim.png
# jetson@nano:~/Downloads$ ls
# installROS2
# jetson@nano:~/Downloads$ 
#   ![Screenshot from 2023-08-15 04-45-58](https://github.com/jetsonmom/monicar2/assets/92077615/215c2cc6-c3a1-4644-b9ec-b151fca1aa01)


#   2.2 .bashrc 수정

     gedit ~/.bashrc 
     
# 또는 편리한 에디터로 .bashrc 열기 
# 파일 제일 아래에 다음과 같은 내용 입력 
     export ROS_DOMAIN_ID=105 
     alias cba="colcon build --symlink-install" 
     alias cbp="colcon build --packages-select" 
     alias cca="rm -rf ~/ros2_ws/install ~/ros2_ws/build" 
     source /opt/ros/foxy/setup.bash source ~/ros2_ws/install/setup.bash 
     
# 에디터 종료 후 터미널 업데이트 

     $ source ~/.bashrc
     
#   2.3 ros2 workspace 설치

# 아래 명령어를 사용하여 clean을 한 번 하면 cba가 문제없이 실행됩니다.

     jetson@nano:~/ros2_ws$ cca
     jetson@nano:~/ros2_ws$ cba

#   2.4 ROS 동작 확인(Option)   

# 터미널 #1
     jetson@nano:~/ros2_ws$ ros2 run demo_nodes_cpp talker
# ![Screenshot from 2023-08-15 06-46-54](https://github.com/jetsonmom/monicar2/assets/92077615/6cdc27be-0e9b-42a2-b453-eed5411d9265) 

# 터미널 #2
     jetson@nano:~/ros2_ws$ ros2 run demo_nodes_py listener
# ![Screenshot from 2023-08-15 06-47-12](https://github.com/jetsonmom/monicar2/assets/92077615/c66b7f7c-748e-4dcc-881b-f8c7985f4be6)

#     3장, udev rule, monicar2 install

#  1. ROS navitation package install on Jetson
#  아래 과정이 Jetson에 navigation2, slam등을 설치하는 과정입니다. 

   sudo apt update
   sudo apt install -y ros-foxy-cartographer-ros ros-foxy-nav2-map-server

#   topic을 확인하기 위해서는 USB2Serial을 사용할 권한을 추가해주어야합니다. dialout에 본인을 추가하여 dialout을 사용하도록 허가합니다. 아래 명령에서 jetson은 user id 입니다.
    
     sudo usermod -aG dialout jetson

#   monicar2 install
#   jessicar2 code를 다운로드하고 빌드해주십시오.    

     cd ros2_ws/
     cd src
     jetson@nano:~/ros2_ws/src$ git clone https://github.com/orocapangyo/monicar2.git
     cd ..
     jetson@nano:~/ros2_ws$ cba
     
#   2. ROS navitation package install on PC

#   아래 과정이 Jetson에 navigation2, amcl등을 설치하는 과정입니다.

     $ cd ~/Downloads
     $ git clone https://github.com/zeta0707/installROS2.git
     $ cd installROS2
     $ ./install-ros2.sh
     $ sudo apt install -y ros-foxy-cartographer-ros ros-foxy-nav2-map-server

#   topic을 확인하기 위해서는 USB2Serial을 사용할 권한을 추가해주어야합니다. dialout에 본인을 추가하여 dialout을 사용하도록 허가합니다. 아래 명령에서 jetson은 user id 입니다.

     sudo usermod -aG dialout jetson

#     **monicar2 install**

# 아래 명령을 따라 jessicar2 code를 다운로드하고 빌드해주십시오.
     $ sudo apt update

     zeta@changwhan-ASUS:~$ cd ros2_ws/
     zeta@changwhan-ASUS:~/ros2_ws$ cd src
     zeta@changwhan-ASUS:~/ros2_ws/src$ git clone https://github.com/orocapangyo/monicar2.git
     zeta@changwhan-ASUS:~/ros2_ws/src$ cd ..

#전체 빌드
     zeta@changwhan-ASUS:~/ros2_ws$ cba
