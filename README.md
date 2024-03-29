# Manjaro install steps and history

## Steps
### Installs

| --- | --- |
| Flatpak | `$ sudo pacman -S flatpak` |

- `$ sudo pacman -S flatpak` (Flatpak)
- `$ flatpak install flathub io.atom.Atom` (Atom)
- `$ sudo pacman -S git` (Git)
- `$ sudo pacman -S redshift` (Redshift)

### Configure
#### Fix slow internet
<details>
  <ol>
    <li>Open KDE Connections Manager</li>
    <li>Change the MTU of your wired connection from 'automatic' to '1492' (bytes)</li>
    <li>Configure repos to local mirrors</li>
    <code>$ sudo pacman-mirrors -g</code>
    <li>Reboot</li>
</details>

### Installs
- `$ sudo pacman -S snapd` (Snap)
- `$ flatpak install flathub net.pcsx2.PCSX2` (PCSX2)
- `$ sudo pacman -S bluez bluez-plugins bluez-utils` (Bluetooth Applications)

### Configure
#### PS3 Controller -  Connect via USB
<details>
  <ol>
    <li>`$ systemctl start bluetooth.service`</li>
    <li>Plug in controller via USB</li>
    <li>Check xpad is installed and up-to-date `$ sudo pacman -S xpad` ***NECESSARY?***</li>
  </ol>
</details>

#### PS3 Controller - Add steam support via USB
1. navigate to /etc/udev/rules.d
2. edit or create the following file `/etc/udev/rules.d/99-dualshock-3.rules` with the following contents:

```
# DualShock 3 controller, Bluetooth
KERNEL=="hidraw*", KERNELS=="*054C:0268*", MODE="0660", TAG+="uaccess"

# DualShock 3 controller, USB
KERNEL=="hidraw*", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="0268", MODE="0660", TAG+="uaccess"\
```

3. add user to input group `$ sudo usermod -aG input $USER`

### Installs (GUI-driven)
#### Propriety NVIDIA graphics drivers
1. Manjaro system settings -> Manjaro -> Hardware Configuration -> Auto Install Propriety Drivers

### Installs
- `$ flatpak install flathub com.spotify.Client` (Spotify)
- `$ flatpak install flathub tv.kodi.Kodi` (Kodi)

### Configure
#### 4TB hard-drive - Mount at boot
1. Add the following lines to `/etc/fstab`

```
# 4TB media/game drive
UUID="8A03-C390"                          /mnt/sda2     exfat   nofail,noatime,rw,user,uid=1000,gid=1000,dmask=022,fmask=133,windows_names,auto,umask=000,exec 0 0
```

2. Reboot

#### 4TH hard-drive - Add as steam library location
_NOTE: the following is a work-around for steam spitting out the error: New Steam library folder must be on a filesystem mounted with execute permissions_

1. In steam, create a new library at `~/SteamLibrary`
2. Navigate to `~/SteamLibrary` and delete the folder `steamapps`
3. On the 4TB hard-drive, create a folder called `Steam-Linux`
4. On the 4TB hard-drive, create a folder called **inside** the folder `Steam-Linux` called `steamapps`
(result should be this: `/mnt/sda2/Steam-Linux/steamapps`)
5. In a terminal
  1. `$ cd ~/SteamLibrary`
  2. `$ ln -s /mnt/sda2/Steam-Linux/steamapps steamapps`
6. You should now have a symbolic link from `~/SteamLibrary/steamapps` on your home folder to `/mnt/sda2/Steam-Linux/steamapps` on your hard-drive

Sources - [Steam Forums](https://steamcommunity.com/app/221410/discussions/0/666827316152433246/#c624076027916587866)

#### Git - Add credentials
##### Add email
`$ git config --global user.email "[github web operations email]"`
##### Add name
`$ git config --global user.name "DrTexxOfficial"`

#### Git - Use SSH
[Original Guide](https://help.github.com/en/articles/connecting-to-github-with-ssh)
1. `$ sudo pacman -S xclip`
1. `$ xclip -sel clip < ~/.ssh/id_rsa.pub`

### AUR Installs
- `$ ?????????????????????` Install xboxdrv via AUR (2019/06/27)

### Installs
- `$ sudo pacman -S wine` (WINE)
- `$ sudo pacman -S wine_gecko` (wine_gecko)
- `$ sudo pacman -S winetricks` (winetricks)
- `$ sudo pacman -S cmake` (CMake)

### ???
#### Build PCSX2 from source
Dependencies:
lib32-bzip2
lib32-libjpeg
lib32-glew
lib32-nvidia-cg-toolkit
lib32-portaudio
lib32-sdl
lib32-soundtouch
sparsehash

(nevermind gave up and used AUR instead)

### AUR Installs
- `$ ????????????????` Install pcsx2-git via AUR

### Installs
- `$ sudo pacman -S bluez-plugins` (bluez-plugins to enable PS3 controller support via bluetooth hopefully)

## Helpful commands
### Hard-drives
<details>
  <summary>List hard-drive information and mount points</summary>
  <code>lsblk</code>
</details>
<details>
  <summary>How to get UUID of hard-drives</summary>
  <code>sudo blkid</code>
</details>
<details>
  <summary>Change hard-drives mounted at boot</summary>
  Edit <code>/etc/fstab</code>
</details>
