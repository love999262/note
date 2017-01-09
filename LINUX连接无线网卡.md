iw连接无线网卡：

iw wlan0 scan 扫描

iw wlan0 link 检测是否连上

ip link show wlan0

ip link set wlan0 up

wpa_supplicant -B -i wlp3s0 -c<(wpa_passphrase "无线用户名" "无线密码")
