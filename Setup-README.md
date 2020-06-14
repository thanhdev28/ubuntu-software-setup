# ubuntu-software-setup
## Setup environment and software

### Install vim
```
sudo apt-get update
sudo apt-get install vim
```

### Install cURL:
```
sudo apt-get install curl
```

### Install Git
```
sudo apt-get update
sudo apt-get install git
```
Git configuration
```
git config --global user.name "Nguyễn Mạnh Cường";
git config --global user.email "nguyenmanhcuong03@vccorp.vn";
git config --global alias.st status;
git config --global alias.co checkout;
git config --global alias.br branch;
git config --global alias.cmf "commit --amend --no-edit";
git config --global alias.lol "log --oneline";
```

## Appearance

### Install ZSH and Oh My ZSH
```
sudo apt-get install zsh
sudo apt-get install powerline fonts-powerline
```
Clone **Oh My ZSH** to **home**
```
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```
Copy **Oh My ZSH** template to **~/.zshrc**
```
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
Open file **~/.zshrc** and change theme to **agnoster** (recommend)
```
ZSH_THEME="agnoster"
```
Change default terminal to ZSH
```
chsh -s /bin/zsh
```
Logout to apply change

### Install ZSH plugins

**Highlight syntax**
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git "$HOME/.zsh-syntax-highlighting" --depth 1
echo "source $HOME/.zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> "$HOME/.zshrc"
```

**Auto suggestion**
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
Update file **~/.zshrc**
```
plugins=(... zsh-autosuggestions)
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=035'
```

### Customize theme like MacOS
[How To Make Ubuntu Look Like Mac (In 5 Steps) - OMG! Ubuntu!](https://www.omgubuntu.co.uk/2017/03/make-ubuntu-look-like-mac-5-steps) <br>
Install gnome-shell extensions:
```
sudo apt-get install chrome-gnome-shell
```
#### Bonus extensions
[User Themes - GNOME Shell Extensions](https://extensions.gnome.org/extension/19/user-themes/) <br>
[Dynamic Panel Transparency - GNOME Shell Extensions](https://extensions.gnome.org/extension/1011/dynamic-panel-transparency/) <br>
Recommend install **Plank Dock** after install **Dask to Dock** <br>
Install **Plank Preferences** from Ubuntu Software

## Environments

### Install nginx
Detail here: [How To Install Nginx on Ubuntu 18.04 \| DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)
```
sudo apt-get update
sudo apt-get install nginx
sudo ufw app list
sudo ufw allow 'Nginx HTTP'
sudo ufw status
systemctl status nginx
```

### Install PHP
[How to Install PHP (7, 7.2 or 7.3) on Ubuntu – ThisHosting.Rocks](https://thishosting.rocks/install-php-on-ubuntu/) <br>
[Install PHP7.2 NGINX and PHP7.2-FPM on Ubuntu 18.04 · GitHub](https://gist.github.com/teocci/18b7ec498586b8ed455b94028b351b4c)
```
sudo apt-get update
sudo apt-get install php7.2 php7.2-cli php7.2-fpm php7.2-curl php7.2-zip php7.2-gd php7.2-mysql php7.2-mbstring php7.2-xml php7.2-redis
```

### Install Nodejs v10.17.0
```
https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions
```
Choose **Node.js v10.x** instructions section

### Install Composer
[Composer Download](https://getcomposer.org/download/)

If **composer isn't global** then run
```
sudo mv composer.phar /usr/local/bin/composer
```

### Install Yarn, Bower
**Yarn**
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```
```
sudo apt update && sudo apt install yarn
```
If **yarn isn't global**. Update file **~/.zshrc**
```
export PATH="$(yarn global bin):$PATH"
```

**Bower**
```
sudo npm i -g bower
```

## Software

### Install IBus Teni
[GitHub - teni-ime/ibus-teni: Bộ gõ tiếng Việt cho Linux chạy trên IBus](https://github.com/teni-ime/ibus-teni)
```
sudo add-apt-repository ppa:teni-ime/ibus-teni
sudo apt-get update
sudo apt-get install ibus-teni
ibus restart
```
Read mouse events, need for ibus-teni work well (options)
```
sudo usermod -a -G input $USER
```

### Install Telegram Desktop
Recommend install **Telegram Desktop** via **apt-get** to using its with Unikey.
```
sudo add-apt-repository ppa:atareao/telegram

sudo apt-get update

sudo apt-get install telegram
```
After that, reboot to using Unikey in **Telegram Desktop**

### Install Smartgit
[SmartGit Downloads](https://www.syntevo.com/smartgit/download/) <br>
Download and extract tar file.
Navigate to folder  **bin**. run file **smartgit.sh** and **add-menuitem.sh**
```
. ./smartgit.sh
```
```
. ./add-menuitem.sh
```
Re purchase Smartgit (eg: Smartgit v19.1)
```
cd ~/.config/smartgit/19.1 && mv preferences.yml preferences.yml.bak
```

### Install PHPStorm
[Download PhpStorm: Lightning-Smart PHP IDE](https://www.jetbrains.com/phpstorm/download/) <br>
Extract and navigate to folder **bin**. Then run file **phpstorm.sh**
```
. ./phpstorm.sh
```

### Install SublimeText
[Linux Package Manager Repositories – Sublime Text 3 Documentation](https://www.sublimetext.com/docs/3/linux_repositories.html)
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```
```
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```
```
sudo apt-get update
sudo apt-get install sublime-text
```

Install **Packages Control** then install **Splunk Conf File Syntax Highlighting** and **nginx** packages to highlight syntax


### Install OpenVPN
```
sudo apt-get install openvpn network-manager-openvpn network-manager-openvpn-gnome
```

### Install PHP Xdebug
```
sudo apt-get update && sudo apt-get install php-xdebug
```

```
sudo subl /etc/php/7.2/mods-available/xdebug.ini
```
Update **xdebug.ini** with following information
```
xdebug.remote_enable=true
xdebug.remote_host=localhost
xdebug.remote_port=9000
xdebug.remote_handler=dbgp
xdebug.remote_autostart=1
```

### Install Flameshot (screenshot)
[GitHub - lupoDharkael/flameshot: Powerful yet simple to use screenshot software](https://github.com/lupoDharkael/flameshot#installation)
```
sudo apt update && sudo apt install flameshot
```
Set shortcut for **Flamshot** <br>
Open **Settings/Devices/Keyboard** then add shortcut
```
Name: Flameshot shortcut
Command: flameshot gui
Shortcut: Windows + Print Screen
```

### Other software
Skype for Linux <br>
DBeaver for SQL <br>
Redis Desktop Manager <br>
VSCode <br>
Koala
## Bonus information

Change workspace's owner to www-data
```
sudo chown -R www-data:www-data /var/www/
```

Add current user to www-data group
```
sudo adduser $USER www-data
```
Allow www-data group's members can modify workspace
```
sudo chmod -R g+rwx /var/www
```

Logout to apply new membership

### Laravel installer <br>
If **laravel installer isn't global**. Update **.zshrc** file
```
export PATH=~/.composer/vendor/bin:$PATH
```

### Fix wrong auto scale resolution Redis Desktop Manager
[Known Issues - Redis Desktop Manager](http://docs.redisdesktop.com/en/latest/known-issues/) <br>
Find **redis-desktop-manager_rdm.desktop** using
```
locate redis-desktop-manager_rdm.desktop
```
or
```
sudo find / -iname "*redis-desktop*"
```
or **default location**
```
/var/lib/snapd/desktop/applications/redis-desktop-manager_rdm.desktop
```

Open file and add **QT_AUTO_SCREEN_SCALE_FACTOR=0** to **Exec** line
