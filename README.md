## Create shortcut in start Menu

Create shortcut of desired program in following location:
```shell
%AppData%\Microsoft\Windows\Start Menu\Programs
```
for eg. shortcut of spyder
<img src=./images/shortcut.PNG width=80%>



## Powerline Fonts

Open `powershell` as admin

```shell
git clone https://github.com/powerline/fonts.git
cd fonts
.\install.ps1

```

Alternative: [POWERLEVEL9K](https://github.com/Powerlevel9k/powerlevel9k)



# WSL

### Install the Windows Subsystem for Linux

Open PowerShell as Administrator and run:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```



Install [Windows 10 May 2020 Update](https://www.microsoft.com/en-in/software-download/windows1 0)

Open PowerShell as Administrator and run:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --set-default-version 2
```

**Install Ubuntu 20.04 from Microsoft Store**



### Settings Up Linux

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
sudo pip install numpy scipy astropy matplotlib pandas pyreduce-astro eleanor
sudo pip install ptipython jupyter

# gdown
sudo pip install gdown

# enabling xserver connection
echo -e "\n" >> ~/.bashrc
echo -e "export DISPLAY=$(grep -m 1 nameserver /etc/resolv.conf | awk '{print $2}'):0.0" >> ~/.bashrc

echo -e "\n" >> ~/.zshrc
echo -e "export DISPLAY=$(grep -m 1 nameserver /etc/resolv.conf | awk '{print $2}'):0.0" >> ~/.zshrc

```



## :warning: Optional



 **Removing password for `sudo`**

```shell
echo -e "$(whoami) ALL=(ALL:ALL) NOPASSWD:ALL"
```



**Theming**

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



# Installing Software

### **IDL**

```shell
#Fixing  libXp.so.6
sudo apt install -y libxpm4 imagemagick
sudo ln -s /usr/lib/x86_64-linux-gnu/libXpm.so.4.11.0 \
/usr/lib/x86_64-linux-gnu/libXp.so.6

cd
gdown --id 132FL4KwI7VWdzrw2bVc4vxqeRXuQZaJN
wget http://lifeng.lamost.org/courses/IDL/software/license.dat
sudo mkdir /usr/local/itt      
sudo tar -xvf ./idl71linux.x86.tar.gz --directory /usr/local/itt/
cd /usr/local/itt
sudo /usr/local/itt/install
cd
sudo mv ./license.dat /usr/local/itt/license/
```



**Libraries**

```shell
git clone https://github.com/idl-coyote/coyote
sudo mv ./coyote /usr/local/itt/idl/lib/
```
