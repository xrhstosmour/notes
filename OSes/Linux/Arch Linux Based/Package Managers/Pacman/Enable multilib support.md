#arch-linux #multilib-support #package-manager
1. ```sudo nvim /etc/pacman.conf```
2. Uncomment the following lines:
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```
3. ```pacman -Syu```