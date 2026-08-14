#vmware #virtualization #ubuntu #docker

Setting up a disposable Linux VM in VMware Workstation/Player for testing:

1. New VM → point at an Ubuntu Server ISO → let the guided install run.
2. Create a non-root user during install, avoid enabling the root account directly.
3. After boot, set a static IP if the VM needs a stable address for SSH access, via netplan (`/etc/netplan/*.yaml`) on modern Ubuntu.
4. Install [[Install open VM tools for Linux|open-vm-tools]] for better host/guest integration (clipboard, resizing).
5. Install Docker inside the VM to use it as a disposable container test bed:
```
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
```
6. Quick smoke test, run a FastAPI container and confirm it's reachable from the host:
```
docker run -d -p 8000:8000 <fastapi_image>
curl http://<vm_ip>:8000
```
