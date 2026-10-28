# Fedora 44 Post-Configuraciòn

Guía de configuración y puesta a punto de Fedora después de una instalación limpia.

---

## Optimización de DNF

### Configuración inicial

Editar la configuración de DNF:

```bash
sudo nano /etc/dnf/dnf.conf
```

Añadir:

```ini
fastestmirror=true
max_parallel_downloads=10
deltarpm=true
```

---

## Actualización del sistema

Actualizar el sistema antes de comenzar con la instalación de paquetes:

```bash
sudo dnf update && sudo dnf upgrade -y
```

---

## Paquetes multimedia

Instalar codecs, reproductores, herramientas de compresión y utilidades multimedia:

```bash
sudo dnf install -y xz bzip2 unrar p7zip lbzip2 arj lzma lzop cpio webp-pixbuf-loader unar file-roller xine-lib-extras xine-lib-extras-freeworld gstreamer1-plugins-base-tools ffmpeg libdvdread libdvdnav lsdvd gstreamer1-vaapi libva-utils ImageMagick
```

### GStreamer

Instalar los plugins y codecs adicionales:

```bash
sudo dnf install -y gstreamer1-plugins-{bad-*,good-*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel
```

### Utilidades

```bash
sudo dnf install tilix cmatrix btop htop fastfetch vlc qbittorrent obs-studio kdenlive mousepad eog evince gparted gnome-tweaks mixxx -y
```

Instalando Extension Manager
```bash
sudo dnf copr enable vaniiiiii/extension-manager
sudo dnf install extension-manager
```

---

## Códecs Kdenlive

Añadir los repositorios RPM Fusion

```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

Cambiar ffmpeg

```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
```

Instalar los códecs extra

```bash
sudo dnf install x264 x264-libs libavcodec-freeworld
```

Comprobar

  - Cierra y abre Kdenlive (si no reconoce los códecs, reinicia la sesión).
  - Importa un MP4.
  - Exporta con el perfil MP4 - H264/AAC.


## Activar Flatpak

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

---

## VirtualBox

### Repositorio de Oracle

Descargar el repositorio:

```bash
sudo wget https://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -P /etc/yum.repos.d/
```

### Dependencias

Instalar las dependencias necesarias:

```bash
sudo dnf install -y kernel-devel kernel-headers dkms elfutils-libelf-devel make gcc
```

### Instalación

Instalar VirtualBox:

```bash
sudo dnf install -y VirtualBox-7.2
```

### Grupo `vboxusers`

Añadir el usuario actual al grupo:

```bash
sudo usermod -aG vboxusers $USER
```

---

## ZSH Terminal

Instalar ZSH y las dependencias necesarias:

```bash
sudo dnf install -y git zsh util-linux-user
```

### Oh My Zsh

Clonar el repositorio:

```bash
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```

Crear la configuración:

```bash
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

Crear una copia de seguridad:

```bash
cp ~/.zshrc ~/.zshrc.orig
```

### Shell predeterminado

Cambiar el shell del usuario a ZSH:

```bash
sudo chsh -s /bin/zsh nombre-de-usuario
```

Cerrar y volver a abrir la terminal.

---

## Powerlevel10k

### Instalación

Clonar Powerlevel10k:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k
```

### Configuración

Añadir Powerlevel10k a `.zshrc`:

```bash
echo 'source ~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc
```

Reiniciar ZSH:

```bash
exec zsh
```

Al iniciar aparecerá el asistente de configuración de Powerlevel10k.

---

## ZSH para Root

Para utilizar ZSH con la cuenta `root`, repetir los mismos pasos de instalación de ZSH, Oh My Zsh y Powerlevel10k desde la cuenta de root.

La configuración de `root` es independiente de la configuración del usuario normal.

---

## Temas e iconos

### Bibata Cursor

Habilitar el repositorio:

```bash
sudo dnf copr enable peterwu/rendezvous
```

Instalar los cursores:

```bash
sudo dnf install -y bibata-cursor-themes
```

Instalar Iconos Papirus

```bash
sudo dnf install -y papirus-icon-theme
```

### Layan GTK Theme

Instalar las dependencias:

```bash
sudo dnf install -y gtk-murrine-engine gtk2-engines
```

Clonar el repositorio:

```bash
git clone https://github.com/vinceliuice/Layan-gtk-theme.git
```

Entrar en el directorio:

```bash
cd Layan-gtk-theme
```

Ejecutar el instalador:

```bash
./install.sh
```

## Reinicio

Reiniciar el sistema para aplicar los cambios:

```bash
sudo reboot
```

---

Listo
