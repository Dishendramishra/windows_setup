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

**Install your Linux distribution of choice from Microsoft Store**



### Tuning Up Linux

```shell
#Essential
sudo apt install xfce4-session
sudo apt install thunar-archive-plugin
sudo apt install dbus-x11
sudo apt-get install python3-gi-cairo

#GTK warnings
sudo apt-get install libatk-adaptor libgail-common
sudo apt-get install gtk2-engines-pixbuf
sudo apt install gnome-themes-standard

# oh-my-zsh
#=======================================================================
sudo apt install -y zsh
echo "yes" | sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

	# adding plugins
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-completions

	# adding plugins in zshrc
sed -i 's/plugins.*/plugins=(sudo git zsh-autosuggestions zsh-completions zsh-syntax-highlighting)/' ~/.zshrc
#=======================================================================

# gdown
echo "y" | sudo apt install python3-pip
sudo ln -s $(which pip3) /usr/local/bin/pip
echo "y" | sudo pip install gdown

# python modules
pip install numpy scipy astropy matplotlib pyreduce-astro jupyter pandas
sudo pip install ptipython

#for theme settings
sudo apt install lxappearance
```



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
