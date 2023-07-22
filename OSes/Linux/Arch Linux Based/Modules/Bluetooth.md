#arch-linux #modules #bluetooth
1. ```pacman -S --needed bluez bluez-utils blueman```
2. ```sudo nvim /etc/bluetooth/main.conf```
3. Uncomment the following line: 
```
AutoEnable=true
```
4. ```sudo systemctl start bluetooth && sudo systemctl enable bluetooth```