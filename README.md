### Desactivar auto interfaz grafica
~~~
$ sudo systemctl disable lxdm.service
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
$ git clone https://github.com/formatcom/v4l2loopback
$ make
$ sudo make install
$ sudo depmod -a
~~~

### V4L2 UTILS
~~~
$ sudo dnf install v4l-utils
$ v4l2-ctl --list-devices
$ v4l2-ctl -d /dev/video3 --all
$ v4l2-ctl -d /dev/video3 --list-formats-ext
~~~

