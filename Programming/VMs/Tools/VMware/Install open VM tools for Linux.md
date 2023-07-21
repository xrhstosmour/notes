#vmware #open-vm-tools #linux

  1. Install the following packages:
	  1. ```open-vm-tools```
	  2. ```xf86-input-vmmouse```
	  3. ```xf86-video-vmware```
	  4. ```gtkmm```
  2. ```sudo echo needs_root_rights=yes >>/etc/X11/Xwrapper.config```
  3. ```sudo systemctl enable vmtoolsd && sudo systemctl start vmtoolsd```