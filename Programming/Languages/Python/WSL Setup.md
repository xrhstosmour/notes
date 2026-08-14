#python #wsl #poetry #venv #vscode

Building a specific Python version from source on WSL (Ubuntu), when the distro's packaged version isn't the one needed:

1. Install the [WSL extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) in VS Code.
2. Inside WSL:
```
sudo apt update && sudo apt upgrade
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libsqlite3-dev libreadline-dev libffi-dev curl libbz2-dev
wget https://www.python.org/ftp/python/<version>/Python-<version>.tgz
tar -xzf Python-<version>.tgz
cd Python-<version>
./configure --enable-optimizations
make -j 2
sudo make install
```
3. Alias it in `~/.bashrc` (the exact build usually installs alongside the distro's default Python, not over it):
```
alias python='/usr/local/bin/python<version>'
```
4. Clean up the build artifacts: `rm -rf Python-<version> Python-<version>.tgz`
5. Install pip and a REPL: `sudo apt install python3-pip ipython3`
6. Install [Poetry](https://python-poetry.org/docs/#installation) for dependency management, then configure it to keep the virtualenv inside the project folder (easier for editors/WSL to find):
```
poetry config virtualenvs.in-project true
```
7. From Windows, `wsl --shutdown` and reopen the project folder in WSL for VS Code to pick up the new interpreter.
8. Whitelist `bash.exe` and `wsl.exe` in antivirus/firewall software, they otherwise sometimes get flagged when VS Code shells out through them.
9. Install linting/formatting tools: `pip install black flake8 poetry poetryup`, see [[Code Analysis]] for the fuller static/dynamic analysis toolchain.
