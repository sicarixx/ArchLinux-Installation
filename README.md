# ArchLinux Installation
## Instrucciones
### 1- Descarga de ArchLinux
Necesitas descargar una ISO de ArchLinux
```bash
wget https://geo.mirror.pkgbuild.com/iso/2023.03.01/archlinux-2023.03.01-x86_64.iso
```
o revisa el siguiente enlace para otros mirrors [Arch Linux Mirrors](https://archlinux.org/download/#download-mirrors)
### 2- Máquinas Virtuales (Opcional)
Si no lo quieres instalar en tu maquina real, necesitarás una maquina virtual, revisa estos enlaces [VirtualBox](https://www.virtualbox.org/wiki/Downloads) or [VMWare](https://www.vmware.com/products/workstation-player.html)
### 3- Documentación
A modo de recomendación, te invito a leer la documentación sobre la instalación de ArchLinux que tienen en su [Wiki](https://wiki.archlinux.org/title/Installation_guide) ya que, este tipo de instalación se realiza solamente por consola y no porque yo lo haga de una forma significa que a ti te va a funcionar de la misma manera. Esta documentación es solo una guía para que se te haga un poco mas fácil y llevadero el proceso de migrar a una distibución tan poderosa como lo es ArchLinux.
### 4- Instalacion en VBox
1. Cargar teclado en español latino loadkeys `la-latin1`
2. Listar discos `lsblk`
3. Crear particiones con `cfdisk`
4. Formatear particion 1 con `mkfs.ext4 /sda1`
5. Formatear swap con `mkswap /dev/sda2`
6. Activar Swap `swapon /dev/sda2`
7. Montar sistema de ficheros `mount /dev/sda1 /mnt`
8. Instalamos linux `pacstrap /mnt base linux linux-firmware`
9. Generamos el archivo Fstab `genfstab -U /mnt >> /mnt/etc/fstab`
10. Cambiamos a la raiz del nuevo sistema `arch-chroot /mnt`
11. Definimos la zona horaria `ln -sf /usr/share/zoneinfo/America/Santiago /etc/localtime`
12. Generamos el adjtime `hwclock --systohc`
13. Editar el archivo `locale.gen` y le agregamos `es_CL.UTF-8 UTF-8`
14. Ejecutamos `locale-gen`
15. Creamos el archivo locale.conf `echo "LANG=es_ES.UTF-8" >> /etc/locale.conf`
16. Definimos la distribucion de teclado `echo "KEYMAP=es" >> /etc/vconsole.conf`
17. Creamos el nombre del equipo `echo "nombredelequipo" >> /etc/hostname`
18. Editamos el archivos hosts `nano /etc/hosts`
```bash
127.0.0.1 localhost
::1       localhost
127.0.0.1 nombredelequipo.localhost nombredelequipo
```
19. Instalamos `nano`, `wpa_supplicant`, `pulseaudio` y `networkmanager`
20. Habilitamos el demonio de networkmanager `systemctl enable NetworkManager`
21. Habilitamos el demonio de wpa_supplicant `systemctl enable wpa_supplicant.service`
22. Instalamos git `pacman -S git --needed base-devel`
23. Activamos PARU y sus paquetes AUR `git clone https://aur.archlinux.org/paru-bin`
24. Creamos la contraseña del administrador `passwd`
25. Creamos el usuario local `useradd -m nombredeusuario`
26. Le agregamos la contraseña al usuario `passwd nombredeusuario`
27. Agregamos el usuario al grupo wheel `usermod -aG wheel nombredeusuario`
28. Instalamos sudo `pacman -S sudo` y editamos el archivo sudoers `nano /etc/sudoers`
29. Debemos instalar grub `pacman -S grub`
30. Instalamos grub en la particion principal `grub-install /dev/sda`
31. Configuramos el grub `grub-mkconfig -o /boot/grub/grub.cfg`
