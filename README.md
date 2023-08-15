# monicar2
# 1. Tool install on Jetson Termius, pc에서 SSH로 JETSON에 접속하기 위하여 Termius 사용
# 1-1. SSH에서 Wifi 연결하기
# 실행해야할 명령

     $ sudo nmcli device wifi list
  
     $ sudo nmcli device wifi connect <ssid_name> password <password>
  
     $ ifconfig
