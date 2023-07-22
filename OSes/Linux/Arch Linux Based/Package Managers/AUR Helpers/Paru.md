#arch-linux #aur #package-manager
1. ```sudo pacman -S --needed base-devel```
2. ```git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si && cd .. && sudo rm -rf paru```
3. ```paru -S --needed rustup && rustup default stable```
4. Enable colors in paru:
	1. ```sudo nvim /etc/pacman.conf```
	2. Uncomment the Color line.
5. Skip preview:
	1. ```sudo nvim /etc/paru.conf```
	2. Add ```SkipReview``` keyword

## Commands
* Remove a package without its dependencies: ```paru -Rdd <package>```
* Remove a package and its dependencies: ```paru -Rsc <package>```
* Update all the packages installed: ```paru -Syu```
* List all installed packages: ```paru -Q```
* Remove all orphan packages: `paru -Rsn $(paru -Qdtq)`