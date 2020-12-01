# Index

1. [WSL](#WSL)
   1. [Installing Windows Subsystem for Linux](#1-installing-windows-subsystem-for-linux)
   2. [Installing X11](#2-installing-x11)
   3. [Setting Up Linux](#3-setting-up-linux)
   4. [Optional](#4-optional-warning)
2. [Installing Software on WSL](#installing-software-on-wsl)
3. [Miscellaneous](#Miscellaneous)



# WSL

### 1. Installing Windows Subsystem for Linux

1. If your **Windows 10 version is less than 2004** then Install  [Windows 10 May 2020 Update](https://www.microsoft.com/en-in/software-download/windows10)

2. Open PowerShell as Administrator and run:

   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```
   then **Restart your PC**
   
3. Download & install Linux kernel update package: https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi  
   then **Restart your PC**

4. Open PowerShell as Administrator and run:

   ```shell
   wsl --set-default-version 2
   ```

5. **Install Ubuntu 20.04 from Microsoft Store**

   <img src=/images/ms_store.png width=80%>
   
6. **(Optional) Installing Theme**

  Open PowerShell as Administrator and run:
```shell
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
scoop install concfg
concfg import https://raw.githubusercontent.com/lukesampson/concfg/master/presets/monokai.json
```

  

### 2. Installing X11	

1. Download and Install [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/)

2. `windows+r`  type  `shell:startup`

3. Create a shortcut there with

    `C:\Program Files\VcXsrv\vcxsrv.exe" :0 -multiwindow -clipboard -wgl -ac`

​		This will autostart  **VcXsrv Windows X Server** on startup

4. Adding rule in firewall

   `windows+r`  type  `wf.msc`

   Add a **New Rule** in **Inbound Rules** => [Instrutions](./firewall_setup.pdf)
   
5. Adding `DISPLAY` variable to you shell profile file.  
   Add the line beloew at the end of your shell profile (`~/.bashrc` for bash-shell or `~/.zshrc` for zsh-shell), so that WSL can connect to X windows system.  
   ```shell
   export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0
   ```

**Or**  
You can use x410, for instructions: [x410 Setup](https://x410.dev/cookbook/wsl/using-x410-with-wsl2/)

### 3. Setting Up Linux

```shell
#Essential
sudo apt install -y xfce4 xfce4-session thunar-archive-plugin dbus-x11 python3-gi-cairo libbz2-dev

#GTK warnings
sudo apt install -y libatk-adaptor libgail-common gtk2-engines-pixbuf gnome-themes-standard

# for theme settings
sudo apt install -y lxappearance

# remove 
sudo apt purge -y xscreensaver gnome-screensaver light-locker i3lock
sudo apt autoremove -y

# oh-my-zsh
#=======================================================================
sudo apt install -y zsh
echo "no" | sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

	# adding plugins
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-completions

	# adding plugins in zshrc
sed -i 's/plugins.*/plugins=(sudo git zsh-autosuggestions zsh-completions zsh-syntax-highlighting)/' ~/.zshrc

chsh -s $(which zsh)
#=======================================================================

# Installing python 3.7.7
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install -y python3.7
wget https://bootstrap.pypa.io/get-pip.py
sudo python3.7 ./get-pip.py
sudo ln -s $(which python3.7) /usr/local/bin/python

# python modules
sudo apt install -y python3.7-tk
sudo pip install numpy scipy astropy matplotlib pandas
sudo pip install ptipython jupyter

# gdown
sudo pip install gdown

# enabling xserver connection
echo -e "\n" >> ~/.bashrc
echo -e "export DISPLAY=$(grep -m 1 nameserver /etc/resolv.conf | awk '{print $2}'):0.0" >> ~/.bashrc

echo -e "\n" >> ~/.zshrc
echo -e "export DISPLAY=$(grep -m 1 nameserver /etc/resolv.conf | awk '{print $2}'):0.0" >> ~/.zshrc

```



## 4. Optional :warning:

- **Powerline Fonts**

  Open `powershell` as admin

  ```shell
  git clone https://github.com/powerline/fonts.git
  cd fonts
  .\install.ps1
  
  ```

  Alternative: [POWERLEVEL9K](https://github.com/Powerlevel9k/powerlevel9k)



-  **Removing password for `sudo`**

  ```shell
  echo -e "$(whoami) ALL=(ALL:ALL) NOPASSWD:ALL"
  ```

  

- **Theming**

  ```shell
  wget https://dllb2.pling.com/api/files/download/j/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6IjE1ODk4ODgwMTAiLCJ1IjpudWxsLCJsdCI6ImRvd25sb2FkIiwicyI6ImIyZWMyNGI4NDJkMTQ1OWI1YWM5ZTViZDU0ZjVmNGQyOWVmNzFjNWRmYzdlNjE0YjljYjI1NmJhYTk2YzYyOTBhZTJlMzY4MTliMGYzNDc1YTQwN2Q3MDJjNTlhZTYyYjdmYmEyM2E4ZjZmMGVlOTg4ZjNkNmZhZGJiOGJiODM5IiwidCI6MTU5MTA5NjQ5NSwic3RmcCI6ImVkZDU0ZjZkZDIyYjcwYjAzZWQ3MTg0OGJkYzAzMDBmIiwic3RpcCI6IjE1MC4xMjkuMTY0LjIxNiJ9.V6Xe0xPZuaGZ3OqvqFFhc5voeGK9JBQ5JwG-iO-cpCw/Mojave-dark-solid.tar.xz
  
  wget https://dllb2.pling.com/api/files/download/j/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6IjE1OTAwNDcxMDciLCJ1IjpudWxsLCJsdCI6ImRvd25sb2FkIiwicyI6IjZhMDNjNGZmYjQzMjcwMTRkY2Q5Y2YyNzZiYmQxODA1MDdhYTc1NjVlZDA0NDhjYmQwYjJjZjdhZTMxNmY3MGQ0NzAwYTkxZTJhZjlmNjBlNjFlOTgzZjc0NjUyYjkzYWQ1ZWU3N2UxNDI3NmU3ZDkyMjc0NmEwNDY5OTU4ZjRlIiwidCI6MTU5MTA5NjY2OCwic3RmcCI6ImVkZDU0ZjZkZDIyYjcwYjAzZWQ3MTg0OGJkYzAzMDBmIiwic3RpcCI6IjE1MC4xMjkuMTY0LjIxNiJ9.aO-tZ8JGVnYtOQrg-G-1vo_I8Pf-APyUGS4hbEpmEE0/03-McMojave-circle-blue.tar.xz
  
  mkdir ~/.icons
  mkdir ~/.themes
  
  tar -xvf ./03-McMojave-circle-blue.tar.xz --directory ~/.icons
  tar -xvf ./Mojave-dark-solid.tar.xz --directory ~/.themes
  
  rm -rf ./03-McMojave-circle-blue.tar.xz ./Mojave-dark-solid.tar.xz
  ```

  After that set theme using `lxappearance`

---



# Installing Software on WSL

- ### **IDL**

  ```shell
  #Fixing  libXp.so.6
  sudo apt install -y libxpm4 imagemagick
  sudo ln -s /usr/lib/x86_64-linux-gnu/libXpm.so.4.11.0 \
  /usr/lib/x86_64-linux-gnu/libXp.so.6
  
  cd
  gdown --id 132FL4KwI7VWdzrw2bVc4vxqeRXuQZaJN
  gdown --id 1HvQAtnpxGbcAe6yqUHc3hFAFgwM0RI9i
  sudo mkdir /usr/local/itt      
  sudo tar -xvf ./idl71linux.x86.tar.gz --directory /usr/local/itt/
  cd /usr/local/itt
  sudo /usr/local/itt/install
  cd
  sudo mv ./license.dat /usr/local/itt/license/
  ```

  **Libraries**

  ```shell
  sudo git clone https://github.com/Dishendramishra/coyote /usr/local/itt/idl/lib/coyote
  sudo git clone https://github.com/Dishendramishra/IDLAstro /usr/local/itt/idl/lib/astron
  sudo wget https://raw.githubusercontent.com/Dishendramishra/idl_tutorial/master/libraries/clear.pro -P /usr/local/itt/idl/lib/
  sudo wget https://raw.githubusercontent.com/Dishendramishra/idl_tutorial/master/libraries/cls.pro -P /usr/local/itt/idl/lib/
  ```

- ### IRAF

  ```shell
  sudo apt install iraf
  ```
  
  Then download file below and `cd` to downloaded location:
  
  https://media.githubusercontent.com/media/Dishendramishra/windows_setup/master/files/iraf-cygwin-files.tar
  
  ```shell
  mkdir iraf_libs
  tar -xvf iraf-cygwin-files.tar --directory ./iraf_libs/
  cd ./iraf_libs/
  sudo mkdir /usr/lib/iraf/extern/tables /usr/lib/iraf/extern/stsdas
  sudo tar -xvf ./stsdas39-src.tar.gz --directory /usr/lib/iraf/extern/stsdas
  sudo tar -xvf ./tables39-src.tar.gz --directory /usr/lib/iraf/extern/tables
  ```
  
  **Running IRAF**
  ```shell
  irafcl
  ```
  
  
- ### Eleanor and Pyreduce

  ```shell
  sudo pip install eleanor pyreduce-astro
  ```

---



# Miscellaneous

- #### **Create shortcut in start Menu**

  Create shortcut of desired program in following location:

  ```powershell
  %AppData%\Microsoft\Windows\Start Menu\Programs
  ```

  for eg. shortcut of spyder
  <img src=./images/shortcut.PNG width=80%>

- #### **Disable Quick Access from Explorer**
  ```
  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer
  ```
  Right-click on an empty space in the right pane, then choose **New → DWORD (32-bit) Value** named **HubMode** value **1**. 
