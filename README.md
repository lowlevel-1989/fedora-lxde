- https://wiki.archlinux.org/title/General_recommendations
- https://github.com/formatcom/mio
- https://github.com/formatcom/vimrc
- https://trac.ffmpeg.org/wiki/HWAccelIntro
- https://trac.ffmpeg.org/wiki/Hardware/VAAPI
- https://trac.ffmpeg.org/wiki/Hardware/QuickSync

### Desactivar auto interfaz grafica (Importante, por si dañas la interfaz o el sistema y esto evite que se quede congelado)
~~~
$ sudo systemctl disable lxdm.service
~~~

### Ver fuentes para el modo texto
~~~
$ ls /lib/kbd/consolefonts/ -1 | grep gz | cat
~~~

### Cambiar la fuente a tu gusto
~~~
$ sudo cp vconsole.conf /etc/vconsole.conf
~~~

### Por si la quieres cambiar de una forma no permanente
~~~
$ setfont solar24x32
~~~

### Actualizar S.O
~~~
$ sudo dnf upgrade
$ reboot
~~~

### Levantar manualmente la interfaz grafica lxde (listen tcp opcional)
~~~
$ xinit /usr/bin/lxsession -- /usr/bin/X :0 vt1 -listen tcp
~~~

### Configurar teclado ( Disable bloq Fn )
~~~
$ localectl
$ localectl list-x11-keymap-layouts | cat
$ localectl list-x11-keymap-models | cat
$ localectl list-x11-keymap-options | cat
$ sudo localectl set-x11-keymap es asus_laptop '' compose:lwin
~~~

### Configurar panel
~~~
$ cp panel ~/.config/lxpanel/LXDE/panels/panel
$ lxpanelctl restart
~~~

### Control de brillo
~~~
$ sudo dnf install brightnessctl
~~~

### Capturar pantalla
~~~
$ sudo dnf install xfce4-screenshooter
~~~

### Agregar Shortcuts
~~~
$ cp lxde-rc.xml .config/openbox/lxde-rc.xml
$ openbox --restart
~~~

### Instalar cliente bluetooth
~~~
$ sudo dnf install blueman
~~~

### Instalar Thunar como navegador de archivos
~~~
$ sudo dnf instasll thunar
~~~

### Instalar Gestor de apariencia
~~~
$ sudo dnf install lxappearance
~~~

### Buscar iconos para el tema
~~~
$ dnf search icon-theme
~~~

### Instalar los iconos que te gusten :3 ejemplo
~~~
$ sudo dnf install breeze-icon-theme
~~~

### Buscar temas para OpenBox
~~~
$ dnf search openbox-theme
~~~

### Instalar un Tema para OpenBox
~~~
$ sudo dnf install openbox-theme-mistral-thin
~~~


### Crear usuario (opcional)
~~~
$ sudo adduser lowlevel
$ sudo passwd lowlevel
~~~

### Agregarlo como usuario con privilegios (opcional)
~~~
$ sudo usermod -aG wheel lowlevel
~~~

### Configurar la aparencia y aplicaciones por defecto si gustas (opcional)
 - Aplicaciones por defecto se configuran desde aqui:
~~~
	- Preferences -> Default applications for LXSession
~~~
 - Cambiar Iconos del sistema y muchas cosas mas:
~~~
	- Preferences -> Customize Look and Feel
~~~
 - Cambiar apariencia de las ventanas:
~~~
	- Preferences -> OpenBox Configuration Manager
~~~

### Eliminar screensaver, normalmente trae mas problemas que beneficios
~~~
$ sudo dnf remove $(rpm -qa | grep xscreensaver)
~~~

### Instalar OpenVPN (opcional)
~~~
$ sudo dnf install openvpn
~~~

### Instalar Git
~~~
$ sudo dnf install git
~~~

### Configurar Git
~~~
$ git config --global user.email "vinicio.valbuena89@gmail.com"
$ git config --global user.name "Vinicio Valbuena"
~~~

### Aqui odiamos el gnome password box, Asi que lo desactivamos
~~~
$ git config --global core.askpass ''
~~~

### Buscar video y buscar controlador en internet
~~~
$ lspci | grep -E "VGA|3D"
~~~

### Instalar driver intel para soporte VA API
~~~
$ sudo dnf install intel-media-driver
~~~

### Buscar controlador nvidia
- https://www.nvidia.com/Download/Find.aspx?lang=en-us

### Si es NVIDIA descativar nouveau que no es compatible
~~~
$ echo "blacklist nouveau" >> /etc/modprobe.d/nouveau-blacklist.conf
~~~

### Actualizar argumento del kernel
~~~
$ ### Agregar argumento rd.driver.blacklist=nouveau En GRUB_CMDLINE_LINUX
$
$ sudo vim /etc/default/grub
$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
$ sudo dnf remove xorg-x11-drv-nouveau
~~~

### Instalar dependencias para compilar el controlador de NVIDIA
~~~
$ sudo dnf install kernel-devel kernel-headers gcc make dkms acpid libglvnd-glx libglvnd-opengl libglvnd-devel pkgconfig
~~~

### Instalar NVIDIA desde el modo texto, Ejemplo
~~~
$ sudo ./NVIDIA-Linux-x86_64-460.84.run
$ reboot
~~~

### Validar Driver NVIDIA
~~~
$ nvidia-smi
~~~

### Instalar Vulkan
~~~
$ sudo dnf install vulkan mesa-vulkan-drivers vulkan-tools
~~~

### Test Vulkan
~~~
$ vulkaninfo | less
~~~

### Validar Xorg
~~~
$ grep LoadModule /var/log/Xorg.0.log
~~~

### Validar validar validar
~~~
$ cat /proc/driver/nvidia/version
~~~

### Validar opengl
~~~
$ glxinfo
~~~

### Validar zona horaria
~~~
$ timedatectl
~~~

### Ver zona horarias disposibles
~~~
$ timedatectl list-timezones
$ # ó
$ ls /usr/share/zoneinfo
~~~

### Cambiar zona horaria
~~~
$ sudo timedatectl set-timezone Europe/Madrid
~~~

### Configurar V4L2 loopback (opcional)
~~~
$ git clone https://github.com/umlaeute/v4l2loopback
$ make
$ sudo make install
$ sudo depmod -a
~~~

### V4L2 UTILS (opcional)
~~~
$ sudo dnf install v4l-utils
$ v4l2-ctl --list-devices
$ v4l2-ctl -d /dev/video3 --all
$ v4l2-ctl -d /dev/video3 --list-formats-ext
~~~

### Habilitar repositorio Fusion (opcional)
~~~
$ sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
~~~

### Instalar OBS
~~~
$ sudo dnf install obs-studio
~~~

### Instalar Emulador terminal
~~~
$ sudo dnf install xfce4-terminal
~~~

### Instalar Zsh
~~~
$ sudo dnf install zsh
~~~

### Antes de colocar zsh por defecto, validar si esta autorizada
~~~
$ cat /etc/shells
~~~

### Colocar zsh como shell por defecto, para el usuario
~~~
$ sudo usermod --shell $(which zsh) $(id --user --name)
~~~

### Validar si se cambio la shell para tu usuario
~~~
$ cat /etc/passwd
~~~

### Instalar Oh My Zsh
~~~
$ curl -LO https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
$ chmod +x install.sh
~~~

### Configurar el tema de la terminal que gustes (para mi wezm+)
- https://github.com/ohmyzsh/ohmyzsh/wiki/Themes

### Para hacerlo mas seisi, instalar tmux: Terminal MUltipleXer
~~~
$ sudo dnf install tmux
~~~

### Instalar xclip, yo lo usare junto a vim y tmux
~~~
$ sudo dnf install xclip
~~~

### Hacer de vim algo sexy
~~~
$ git clone https://github.com/formatcom/vimrc.git
$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
$ cp vimrc ~/.vimrc
$ vim +PluginInstall +qall
~~~

### Instalar dependencias de YouCompleteMe
~~~
$ sudo dnf install python3-devel
$ sudo dnf install golang                 # soporte go
$ sudo dnf install nodejs                 # soporte nodejs
$ sudo dnf install java-latest-openjdk    # soporte java
~~~
~~~
$ pip install flake8
$ pip install pytest
$ pip install PyHamcrest
~~~

### Instalar YouCompleteMe
~~~
$ cd ~/.vim/bundle/YouCompleteMe
$ python3 run_tests.py
$ python3 install.py --all
~~~

### Instalar Visor de imagen
~~~
$ sudo dnf install nomacs
$ sudo dnf install nomacs-plugins
~~~

### Utilizar mi configuración para nomacs (opcional)
~~~
$ cp -rf Image\ Lounge.conf ~/.config/nomacs
~~~
