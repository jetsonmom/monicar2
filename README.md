# monicar2
# 1. Tool install on Jetson Termius, pc에서 SSH로 JETSON에 접속하기 위하여 Termius 사용
# 1-1. SSH에서 Wifi 연결하기
# 실행해야할 명령

     $ sudo nmcli device wifi list
  
     $ sudo nmcli device wifi connect <ssid_name> password <password>
  
     $ ifconfig

     
# ![Screenshot from 2023-08-15 02-44-43](https://github.com/jetsonmom/monicar2/assets/92077615/f6f05745-972c-4d5d-a091-34e1b623bcce)

      

# ![Screenshot from 2023-08-15 02-17-35](https://github.com/jetsonmom/monicar2/assets/92077615/a17e7c40-b7e1-4431-80ac-01dbb1986fbc)

# 연결을 해제할 때
     $ sudo nmcli device disconnect wlan0
