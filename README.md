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
