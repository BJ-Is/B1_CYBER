### 1.Préparation de la machine
### 🌞 Exécution du script autoconfig.sh
```bash
[rock-bji@music ~]$ sudo /opt/autoconfig.sh music.tp3.b3
22:17:17 [INFO] Le script d'autoconfiguration a démarré
22:17:17 [INFO] Le script a bien été lancé en root.
22:17:17 [INFO] Vérification de l'état de SELinux...
22:17:17 [INFO] Vérification de l'état du firewall
22:17:17 [INFO] Service de firewalling firewalld est activé.
22:17:17 [INFO] Vérification du port SSH
22:17:17 [INFO] Le service SSH ne tourne pas sur le port 22/TCP. Port actuel : 33672.
22:17:17 [INFO] La machine s'appelle déjà music.tp3.b3.
22:17:17 [INFO] Vérification de l'utilisateur rock-bji...
22:17:17 [INFO] L'utilisateur rock-bji est déjà dans le groupe wheel.
22:17:17 [INFO] Le script d'autoconfiguration s'est correctement déroulé.
[rock-bji@vbox ~]$
```
### 🌞 Création du dossier pour héberger les fichiers de musique
```bash
[rock-bji@music ~]$ sudo mkdir -p /srv/music
```
### 🌞 Déposer des fichiers son dans le dossier
```bash
$ scp "/c/Users/jerem/Downloads/hope.mp3" rock-bji@192.168.20.17:/srv/music/
rock-bji@192.168.20.17's password:
hope.mp3                                      100% 2660KB  26.1MB/s   00:00

$ scp "/c/Users/jerem/Downloads/son_espoir.mp3" rock-bji@192.168.20.17:/srv/music/
rock-bji@192.168.20.17's password:
son_espoir.mp3                                100% 2660KB  22.6MB/s   00:00

$ scp "C:\Users\jerem\Downloads\dawnofchange.mp3" rock-bji@192.168.20.17:/srv/music/
rock-bji@192.168.20.17's password:
C:\Users\jerem\Downloads\dawnofchange.mp3     100% 2764KB  21.1MB/s   00:00

```
### 2. Installation du service de streaming
### 🌞 Ajouter les dépôts nécessaires pour installer Jellyfin
```bash
[rock-bji@music ~]$ sudo dnf install --nogpgcheck https://mirrors.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-$(rpm -E %rhel).noarch.rpm -y
sudo dnf config-manager --set-enabled crb
[sudo] password for rock-bji:
Last metadata expiration check: 0:56:40 ago on Sat 18 Jan 2025 02:10:09 PM CET.
rpmfusion-nonfree-release-9.noarch.rpm       18 kB/s |  10 kB     00:00
Dependencies resolved.
============================================================================
 Package                      Arch      Version       Repository       Size
============================================================================
Installing:
 rpmfusion-nonfree-release    noarch    9-1           @commandline     10 k
Installing dependencies:
 epel-release                 noarch    9-7.el9       extras           19 k
 rpmfusion-free-release       noarch    9-1           extras          9.2 k

Transaction Summary
============================================================================
Install  3 Packages

Total size: 38 k
Total download size: 28 k
Installed size: 34 k
Downloading Packages:
(1/2): rpmfusion-free-release-9-1.noarch.rp  46 kB/s | 9.2 kB     00:00
(2/2): epel-release-9-7.el9.noarch.rpm       87 kB/s |  19 kB     00:00
----------------------------------------------------------------------------
Total                                        59 kB/s |  28 kB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                    1/1
  Installing       : epel-release-9-7.el9.noarch                        1/3
  Running scriptlet: epel-release-9-7.el9.noarch                        1/3
Many EPEL packages require the CodeReady Builder (CRB) repository.
It is recommended that you run /usr/bin/crb enable to enable the CRB repository.

  Installing       : rpmfusion-free-release-9-1.noarch                  2/3
  Installing       : rpmfusion-nonfree-release-9-1.noarch               3/3
  Running scriptlet: rpmfusion-nonfree-release-9-1.noarch               3/3
  Verifying        : epel-release-9-7.el9.noarch                        1/3
  Verifying        : rpmfusion-free-release-9-1.noarch                  2/3
  Verifying        : rpmfusion-nonfree-release-9-1.noarch               3/3

Installed:
  epel-release-9-7.el9.noarch            rpmfusion-free-release-9-1.noarch
  rpmfusion-nonfree-release-9-1.noarch

Complete!
```
### 🌞 Installer le paquet jellyfin
```bash
[rock-bji@music ~]$ sudo dnf install jellyfin -y
Extra Packages for Enterprise Linux 9 - x86  12 MB/s |  23 MB     00:01

Extra Packages for Enterprise Linux 9 openh 3.2 kB/s | 2.5 kB     00:00
Rocky Linux 9 - BaseOS                       11 kB/s | 4.1 kB     00:00
Rocky Linux 9 - AppStream                    11 kB/s | 4.5 kB     00:00
Rocky Linux 9 - CRB                         4.2 MB/s | 2.5 MB     00:00
RPM Fusion for EL 9 - Free - Updates        522 kB/s | 220 kB     00:00
RPM Fusion for EL 9 - Nonfree - Updates     189 kB/s |  91 kB     00:00
Dependencies resolved.
============================================================================
 Package             Arch   Version            Repository              Size
============================================================================
Installing:
 jellyfin            x86_64 10.8.13-1.el9      rpmfusion-free-updates 9.3 k
Installing dependencies:
 SDL2                x86_64 2.26.0-1.el9       appstream              683 k
 alsa-lib            x86_64 1.2.12-1.el9       appstream              504 k
 aspnetcore-runtime-6.0
                     x86_64 6.0.36-1.el9_5     appstream              6.9 M
 at                  x86_64 3.1.23-11.el9      baseos                  60 k
 cairo               x86_64 1.17.4-7.el9       appstream              659 k
 cairo-gobject       x86_64 1.17.4-7.el9       appstream               18 k
 dotnet-host         x86_64 9.0.1-1.el9_5      appstream              213 k
 dotnet-hostfxr-6.0  x86_64 6.0.36-1.el9_5     appstream              163 k
 dotnet-runtime-6.0  x86_64 6.0.36-1.el9_5     appstream               23 M
 ffmpeg              x86_64 5.1.6-2.el9        rpmfusion-free-updates 1.7 M
 ffmpeg-libs         x86_64 5.1.6-2.el9        rpmfusion-free-updates 7.8 M
 fftw-libs-double    x86_64 3.3.8-12.el9.0.1   appstream              906 k
 flac-libs           x86_64 1.3.3-10.el9_2.1   appstream              217 k
 fontconfig          x86_64 2.14.0-2.el9_1     appstream              274 k
 freetype            x86_64 2.10.4-9.el9       baseos                 387 k
 fribidi             x86_64 1.0.10-6.el9.2     appstream               84 k
 gdk-pixbuf2         x86_64 2.42.6-4.el9_4     appstream              466 k
 graphite2           x86_64 1.3.14-9.el9       baseos                  94 k
 gsm                 x86_64 1.0.19-6.el9       appstream               33 k
 harfbuzz            x86_64 2.7.4-10.el9       baseos                 623 k
 highway             x86_64 1.2.0-2.el9        epel                    35 k
 intel-mediasdk      x86_64 21.3.5-1.el9       epel                   2.6 M
 jack-audio-connection-kit
                     x86_64 1.9.21-1.el9       epel                   522 k
 jellyfin-firewalld  noarch 10.8.13-1.el9      rpmfusion-free-updates  17 k
 jellyfin-server     x86_64 10.8.13-1.el9      rpmfusion-free-updates 9.7 M
 jellyfin-web        noarch 10.8.13-1.el9      rpmfusion-free-updates  40 M
 ladspa              x86_64 1.13-28.el9        crb                     47 k
 lame-libs           x86_64 3.100-12.el9       appstream              332 k
 libX11              x86_64 1.7.0-9.el9        appstream              650 k
 libX11-common       noarch 1.7.0-9.el9        appstream              151 k
 libX11-xcb          x86_64 1.7.0-9.el9        appstream               10 k
 libXau              x86_64 1.0.9-8.el9        appstream               30 k
 libXext             x86_64 1.3.4-8.el9        appstream               39 k
 libXfixes           x86_64 5.0.3-16.el9       appstream               19 k
 libXft              x86_64 2.3.3-8.el9        appstream               61 k
 libXrender          x86_64 0.9.10-16.el9      appstream               27 k
 libXxf86vm          x86_64 1.1.4-18.el9       appstream               18 k
 libaom              x86_64 3.9.0-1.el9        epel                   1.8 M
 libass              x86_64 0.17.1-1.el9       epel                   116 k
 libasyncns          x86_64 0.8-22.el9         appstream               29 k
 libavdevice         x86_64 5.1.6-2.el9        rpmfusion-free-updates  70 k
 libbluray           x86_64 1.3.4-1.el9        epel                   171 k
 libcdio             x86_64 2.1.0-6.el9        appstream              244 k
 libcdio-paranoia    x86_64 10.2+2.0.1-6.el9   appstream               85 k
 libdatrie           x86_64 0.2.13-4.el9       appstream               32 k
 libdav1d            x86_64 1.5.0-2.el9        epel                   601 k
 libdecor            x86_64 0.1.1-1.el9        appstream               42 k
 libdrm              x86_64 2.4.121-1.el9      appstream              158 k
 libglvnd            x86_64 1:1.3.4-1.el9      appstream              133 k
 libglvnd-glx        x86_64 1:1.3.4-1.el9      appstream              140 k
 libicu              x86_64 67.1-9.el9         baseos                 9.6 M
 libjpeg-turbo       x86_64 2.0.90-7.el9       appstream              174 k
 libjxl              x86_64 0.7.0-1.el9        epel                   957 k
 libmodplug          x86_64 1:0.8.9.0-13.el9   epel                   171 k
 libmysofa           x86_64 1.2.1-1.el9        epel                    42 k
 libogg              x86_64 2:1.3.4-6.el9      appstream               32 k
 libopenmpt          x86_64 0.7.13-1.el9       epel                   686 k
 libpciaccess        x86_64 0.16-7.el9         baseos                  26 k
 libpng              x86_64 2:1.6.37-12.el9    baseos                 116 k
 librsvg2            x86_64 2.50.7-3.el9       appstream              2.8 M
 libsamplerate       x86_64 0.1.9-10.el9       appstream              1.3 M
 libshaderc          x86_64 2024.0-1.el9       appstream              1.0 M
 libsndfile          x86_64 1.0.31-8.el9_5.2   appstream              206 k
 libthai             x86_64 0.1.28-8.el9       appstream              208 k
 libtheora           x86_64 1:1.1.1-31.el9     appstream              163 k
 libudfread          x86_64 1.1.2-2.el9        epel                    33 k
 libv4l              x86_64 1.20.0-5.el9       appstream              198 k
 libva               x86_64 2.20.0-1.el9       appstream              105 k
 libvdpau            x86_64 1.5-1.el9          appstream               16 k
 libvmaf             x86_64 2.3.0-2.el9        epel                   177 k
 libvorbis           x86_64 1:1.3.7-5.el9      appstream              192 k
 libvpx              x86_64 1.9.0-8.el9_5      appstream              1.1 M
 libwayland-client   x86_64 1.21.0-1.el9       appstream               33 k
 libwayland-cursor   x86_64 1.21.0-1.el9       appstream               18 k
 libxcb              x86_64 1.13.1-9.el9       appstream              224 k
 libxshmfence        x86_64 1.3-10.el9         appstream               12 k
 lilv-libs           x86_64 0.24.14-3.el9      epel                    58 k
 llvm-libs           x86_64 18.1.8-3.el9       appstream               26 M
 lttng-ust           x86_64 2.12.0-6.el9       appstream              282 k
 lv2                 x86_64 1.18.8-4.el9       epel                    90 k
 mesa-filesystem     x86_64 24.1.2-3.el9       appstream               10 k
 mesa-libGL          x86_64 24.1.2-3.el9       appstream              169 k
 mesa-libglapi       x86_64 24.1.2-3.el9       appstream               44 k
 mpg123-libs         x86_64 1.32.9-1.el9_5     appstream              349 k
 ocl-icd             x86_64 2.2.13-4.el9       appstream               51 k
 openal-soft         x86_64 1.19.1-16.el9      appstream              533 k
 opencore-amr        x86_64 0.1.6-3.el9        epel                   172 k
 openjpeg2           x86_64 2.4.0-7.el9        appstream              162 k
 opus                x86_64 1.3.1-10.el9       appstream              199 k
 pango               x86_64 1.48.7-3.el9       appstream              297 k
 pixman              x86_64 0.40.0-6.el9_3     appstream              269 k
 pulseaudio-libs     x86_64 15.0-2.el9         appstream              666 k
 rubberband          x86_64 3.1.3-2.el9        epel                   365 k
 serd                x86_64 0.30.12-2.el9      epel                    61 k
 shared-mime-info    x86_64 2.1-5.el9          baseos                 372 k
 sord                x86_64 0.16.10-2.el9      epel                    46 k
 soxr                x86_64 0.1.3-11.el9       epel                    82 k
 speex               x86_64 1.2.0-11.el9       appstream               67 k
 spirv-tools-libs    x86_64 2024.2-1.el9       appstream              1.4 M
 sratom              x86_64 0.6.10-2.el9       epel                    26 k
 srt-libs            x86_64 1.4.4-1.el9        epel                   291 k
 svt-av1-libs        x86_64 0.9.0-1.el9        epel                   1.7 M
 vamp-plugin-sdk     x86_64 2.9.0-4.el9        epel                   171 k
 vapoursynth-libs    x86_64 57-1.el9           epel                   503 k
 vid.stab            x86_64 1.1.0-14.20201110gitf9166e9.el9
                                               epel                    49 k
 vo-amrwbenc         x86_64 0.1.3-18.el9       epel                    75 k
 x264-libs           x86_64 0.163-6.20210613git5db6aa6.el9
                                               rpmfusion-free-updates 682 k
 x265-libs           x86_64 3.5-5.el9          rpmfusion-free-updates 1.3 M
 xml-common          noarch 0.6.3-58.el9       appstream               31 k
 xvidcore            x86_64 1.3.7-9.el9        epel                   252 k
 zimg                x86_64 3.0.5-1.el9        epel                   275 k
 zvbi                x86_64 0.2.35-15.el9      epel                   413 k
Installing weak dependencies:
 jxl-pixbuf-loader   x86_64 0.7.0-1.el9        epel                    53 k
 mesa-dri-drivers    x86_64 24.1.2-3.el9       appstream              8.8 M
 vmaf-models         noarch 2.3.0-2.el9        epel                   227 k

Transaction Summary
============================================================================
Install  116 Packages

Total download size: 168 M
Installed size: 507 M
Downloading Packages:
Rocky Linux 9 - CR1268% [===========================================================================================================================================================================================================(1/116): highway-1.2.0-2.el9.x86_64.rpm     241 kB/s |  35 kB     00:00
(2/116): jxl-pixbuf-loader-0.7.0-1.el9.x86_ 805 kB/s |  53 kB     00:00
(3/116): jack-audio-connection-kit-1.9.21-1 1.2 MB/s | 522 kB     00:00
(4/116): libass-0.17.1-1.el9.x86_64.rpm     1.7 MB/s | 116 kB     00:00
(5/116): libbluray-1.3.4-1.el9.x86_64.rpm   1.2 MB/s | 171 kB     00:00
(6/116): libdav1d-1.5.0-2.el9.x86_64.rpm    2.9 MB/s | 601 kB     00:00
(7/116): libjxl-0.7.0-1.el9.x86_64.rpm      3.3 MB/s | 957 kB     00:00
(8/116): libaom-3.9.0-1.el9.x86_64.rpm      1.8 MB/s | 1.8 MB     00:01
(9/116): libmodplug-0.8.9.0-13.el9.x86_64.r 1.4 MB/s | 171 kB     00:00
(10/116): libmysofa-1.2.1-1.el9.x86_64.rpm  777 kB/s |  42 kB     00:00
(11/116): libudfread-1.1.2-2.el9.x86_64.rpm 566 kB/s |  33 kB     00:00
(12/116): intel-mediasdk-21.3.5-1.el9.x86_6 1.8 MB/s | 2.6 MB     00:01
(13/116): libvmaf-2.3.0-2.el9.x86_64.rpm    1.9 MB/s | 177 kB     00:00
(14/116): lilv-libs-0.24.14-3.el9.x86_64.rp 1.1 MB/s |  58 kB     00:00
(15/116): libopenmpt-0.7.13-1.el9.x86_64.rp 3.3 MB/s | 686 kB     00:00
(16/116): lv2-1.18.8-4.el9.x86_64.rpm       1.2 MB/s |  90 kB     00:00
(17/116): opencore-amr-0.1.6-3.el9.x86_64.r 1.8 MB/s | 172 kB     00:00
(18/116): sord-0.16.10-2.el9.x86_64.rpm     704 kB/s |  46 kB     00:00
(19/116): rubberband-3.1.3-2.el9.x86_64.rpm 2.2 MB/s | 365 kB     00:00
(20/116): serd-0.30.12-2.el9.x86_64.rpm     473 kB/s |  61 kB     00:00
(21/116): soxr-0.1.3-11.el9.x86_64.rpm      490 kB/s |  82 kB     00:00
(22/116): sratom-0.6.10-2.el9.x86_64.rpm    162 kB/s |  26 kB     00:00
(23/116): srt-libs-1.4.4-1.el9.x86_64.rpm   1.6 MB/s | 291 kB     00:00
(24/116): vamp-plugin-sdk-2.9.0-4.el9.x86_6 975 kB/s | 171 kB     00:00
(25/116): vapoursynth-libs-57-1.el9.x86_64. 2.5 MB/s | 503 kB     00:00
(26/116): vid.stab-1.1.0-14.20201110gitf916 975 kB/s |  49 kB     00:00
(27/116): vmaf-models-2.3.0-2.el9.noarch.rp 2.1 MB/s | 227 kB     00:00
(28/116): vo-amrwbenc-0.1.3-18.el9.x86_64.r 791 kB/s |  75 kB     00:00
(29/116): zimg-3.0.5-1.el9.x86_64.rpm       2.0 MB/s | 275 kB     00:00
(30/116): xvidcore-1.3.7-9.el9.x86_64.rpm   1.6 MB/s | 252 kB     00:00
(31/116): svt-av1-libs-0.9.0-1.el9.x86_64.r 2.6 MB/s | 1.7 MB     00:00
(32/116): zvbi-0.2.35-15.el9.x86_64.rpm     2.2 MB/s | 413 kB     00:00
(33/116): graphite2-1.3.14-9.el9.x86_64.rpm 677 kB/s |  94 kB     00:00
(34/116): at-3.1.23-11.el9.x86_64.rpm       425 kB/s |  60 kB     00:00
(35/116): libpciaccess-0.16-7.el9.x86_64.rp 325 kB/s |  26 kB     00:00
(36/116): harfbuzz-2.7.4-10.el9.x86_64.rpm  1.6 MB/s | 623 kB     00:00
(37/116): libpng-1.6.37-12.el9.x86_64.rpm   2.5 MB/s | 116 kB     00:00
(38/116): freetype-2.10.4-9.el9.x86_64.rpm  4.5 MB/s | 387 kB     00:00
(39/116): shared-mime-info-2.1-5.el9.x86_64 4.7 MB/s | 372 kB     00:00
(40/116): fribidi-1.0.10-6.el9.2.x86_64.rpm 375 kB/s |  84 kB     00:00
(41/116): SDL2-2.26.0-1.el9.x86_64.rpm      1.4 MB/s | 683 kB     00:00
(42/116): fontconfig-2.14.0-2.el9_1.x86_64. 1.6 MB/s | 274 kB     00:00
(43/116): libasyncns-0.8-22.el9.x86_64.rpm  346 kB/s |  29 kB     00:00
(44/116): libxshmfence-1.3-10.el9.x86_64.rp 201 kB/s |  12 kB     00:00
(45/116): libXfixes-5.0.3-16.el9.x86_64.rpm 376 kB/s |  19 kB     00:00
(46/116): libogg-1.3.4-6.el9.x86_64.rpm     478 kB/s |  32 kB     00:00
(47/116): libX11-common-1.7.0-9.el9.noarch. 1.1 MB/s | 151 kB     00:00
(48/116): libicu-67.1-9.el9.x86_64.rpm      7.0 MB/s | 9.6 MB     00:01
(49/116): libsamplerate-0.1.9-10.el9.x86_64 1.5 MB/s | 1.3 MB     00:00
(50/116): libva-2.20.0-1.el9.x86_64.rpm     462 kB/s | 105 kB     00:00
(51/116): speex-1.2.0-11.el9.x86_64.rpm     742 kB/s |  67 kB     00:00
(52/116): libXau-1.0.9-8.el9.x86_64.rpm     872 kB/s |  30 kB     00:00
(53/116): gsm-1.0.19-6.el9.x86_64.rpm       504 kB/s |  33 kB     00:00
(54/116): libdecor-0.1.1-1.el9.x86_64.rpm   786 kB/s |  42 kB     00:00
(55/116): mesa-libglapi-24.1.2-3.el9.x86_64 1.1 MB/s |  44 kB     00:00
(56/116): libxcb-1.13.1-9.el9.x86_64.rpm    2.0 MB/s | 224 kB     00:00
(57/116): mesa-filesystem-24.1.2-3.el9.x86_ 191 kB/s |  10 kB     00:00
(58/116): mesa-libGL-24.1.2-3.el9.x86_64.rp 1.6 MB/s | 169 kB     00:00
(59/116): libvdpau-1.5-1.el9.x86_64.rpm     227 kB/s |  16 kB     00:00
(60/116): libXrender-0.9.10-16.el9.x86_64.r 589 kB/s |  27 kB     00:00
(61/116): flac-libs-1.3.3-10.el9_2.1.x86_64 1.2 MB/s | 217 kB     00:00
(62/116): libdrm-2.4.121-1.el9.x86_64.rpm   1.9 MB/s | 158 kB     00:00
(63/116): libsndfile-1.0.31-8.el9_5.2.x86_6 2.3 MB/s | 206 kB     00:00
(64/116): mpg123-libs-1.32.9-1.el9_5.x86_64 2.1 MB/s | 349 kB     00:00
(65/116): libjpeg-turbo-2.0.90-7.el9.x86_64 2.3 MB/s | 174 kB     00:00
(66/116): libXft-2.3.3-8.el9.x86_64.rpm     910 kB/s |  61 kB     00:00
(67/116): libXext-1.3.4-8.el9.x86_64.rpm    787 kB/s |  39 kB     00:00
(68/116): libdatrie-0.2.13-4.el9.x86_64.rpm 528 kB/s |  32 kB     00:00
(69/116): libvorbis-1.3.7-5.el9.x86_64.rpm  1.6 MB/s | 192 kB     00:00
(70/116): libglvnd-glx-1.3.4-1.el9.x86_64.r 1.4 MB/s | 140 kB     00:00
(71/116): libglvnd-1.3.4-1.el9.x86_64.rpm   1.1 MB/s | 133 kB     00:00
(72/116): libtheora-1.1.1-31.el9.x86_64.rpm 1.3 MB/s | 163 kB     00:00
(73/116): libcdio-2.1.0-6.el9.x86_64.rpm    1.8 MB/s | 244 kB     00:00
(74/116): librsvg2-2.50.7-3.el9.x86_64.rpm  2.4 MB/s | 2.8 MB     00:01
(75/116): libvpx-1.9.0-8.el9_5.x86_64.rpm   2.1 MB/s | 1.1 MB     00:00
(76/116): alsa-lib-1.2.12-1.el9.x86_64.rpm  2.1 MB/s | 504 kB     00:00
(77/116): libthai-0.1.28-8.el9.x86_64.rpm   1.9 MB/s | 208 kB     00:00
(78/116): mesa-dri-drivers-24.1.2-3.el9.x86 2.4 MB/s | 8.8 MB     00:03
(79/116): lame-libs-3.100-12.el9.x86_64.rpm 2.1 MB/s | 332 kB     00:00
(80/116): libXxf86vm-1.1.4-18.el9.x86_64.rp 358 kB/s |  18 kB     00:00
(81/116): opus-1.3.1-10.el9.x86_64.rpm      1.3 MB/s | 199 kB     00:00
(82/116): openal-soft-1.19.1-16.el9.x86_64. 2.0 MB/s | 533 kB     00:00
(83/116): openjpeg2-2.4.0-7.el9.x86_64.rpm  1.5 MB/s | 162 kB     00:00
(84/116): ocl-icd-2.2.13-4.el9.x86_64.rpm   1.0 MB/s |  51 kB     00:00
(85/116): libwayland-cursor-1.21.0-1.el9.x8 311 kB/s |  18 kB     00:00
(86/116): libwayland-client-1.21.0-1.el9.x8 503 kB/s |  33 kB     00:00
(87/116): pixman-0.40.0-6.el9_3.x86_64.rpm  1.9 MB/s | 269 kB     00:00
(88/116): xml-common-0.6.3-58.el9.noarch.rp 682 kB/s |  31 kB     00:00
(89/116): pulseaudio-libs-15.0-2.el9.x86_64 2.0 MB/s | 666 kB     00:00
(90/116): spirv-tools-libs-2024.2-1.el9.x86 2.3 MB/s | 1.4 MB     00:00
(91/116): dotnet-hostfxr-6.0-6.0.36-1.el9_5 1.5 MB/s | 163 kB     00:00
(92/116): aspnetcore-runtime-6.0-6.0.36-1.e 2.4 MB/s | 6.9 MB     00:02
(93/116): pango-1.48.7-3.el9.x86_64.rpm     1.9 MB/s | 297 kB     00:00
(94/116): fftw-libs-double-3.3.8-12.el9.0.1 2.3 MB/s | 906 kB     00:00
(95/116): cairo-gobject-1.17.4-7.el9.x86_64 322 kB/s |  18 kB     00:00
(96/116): cairo-1.17.4-7.el9.x86_64.rpm     2.2 MB/s | 659 kB     00:00
(97/116): libX11-xcb-1.7.0-9.el9.x86_64.rpm 233 kB/s |  10 kB     00:00
(98/116): libX11-1.7.0-9.el9.x86_64.rpm     2.2 MB/s | 650 kB     00:00
(99/116): libcdio-paranoia-10.2+2.0.1-6.el9 1.1 MB/s |  85 kB     00:00
(100/116): lttng-ust-2.12.0-6.el9.x86_64.rp 1.8 MB/s | 282 kB     00:00
(101/116): gdk-pixbuf2-2.42.6-4.el9_4.x86_6 2.3 MB/s | 466 kB     00:00
(102/116): llvm-libs-18.1.8-3.el9.x86_64.rp 2.4 MB/s |  26 MB     00:10
(103/116): libv4l-1.20.0-5.el9.x86_64.rpm   853 kB/s | 198 kB     00:00
(104/116): dotnet-host-9.0.1-1.el9_5.x86_64 1.5 MB/s | 213 kB     00:00
(105/116): libshaderc-2024.0-1.el9.x86_64.r 2.3 MB/s | 1.0 MB     00:00
(106/116): ladspa-1.13-28.el9.x86_64.rpm    173 kB/s |  47 kB     00:00
(107/116): ffmpeg-5.1.6-2.el9.x86_64.rpm    1.7 MB/s | 1.7 MB     00:01
(108/116): jellyfin-10.8.13-1.el9.x86_64.rp 178 kB/s | 9.3 kB     00:00
(109/116): jellyfin-firewalld-10.8.13-1.el9 261 kB/s |  17 kB     00:00
(110/116): ffmpeg-libs-5.1.6-2.el9.x86_64.r 3.6 MB/s | 7.8 MB     00:02
(111/116): jellyfin-server-10.8.13-1.el9.x8 5.3 MB/s | 9.7 MB     00:01
(112/116): libavdevice-5.1.6-2.el9.x86_64.r 707 kB/s |  70 kB     00:00
(113/116): x264-libs-0.163-6.20210613git5db 4.2 MB/s | 682 kB     00:00
(114/116): x265-libs-3.5-5.el9.x86_64.rpm   4.0 MB/s | 1.3 MB     00:00
(115/116): dotnet-runtime-6.0-6.0.36-1.el9_ 2.3 MB/s |  23 MB     00:10
(116/116): jellyfin-web-10.8.13-1.el9.noarc  12 MB/s |  40 MB     00:03
----------------------------------------------------------------------------
Total                                       7.8 MB/s | 168 MB     00:21
Extra Packages for Enterprise Linux 9 - x86 1.1 MB/s | 1.6 kB     00:00
Importing GPG key 0x3228467C:
 Userid     : "Fedora (epel9) <epel@fedoraproject.org>"
 Fingerprint: FF8A D134 4597 106E CE81 3B91 8A38 72BF 3228 467C
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-9
Key imported successfully
RPM Fusion for EL 9 - Free - Updates        428 kB/s | 1.7 kB     00:00
Importing GPG key 0x296458F3:
 Userid     : "RPM Fusion free repository for EL (9) <rpmfusion-gpg-key-el9-free@rpmfusion.org>"
 Fingerprint: EDC0 0FE7 418C 9DF7 EF49 91A4 7403 EA33 2964 58F3
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-el-9
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Running scriptlet: jellyfin-server-10.8.13-1.el9.x86_64               1/1
  Preparing        :                                                    1/1
  Installing       : libpng-2:1.6.37-12.el9.x86_64                    1/116
  Installing       : libogg-2:1.3.4-6.el9.x86_64                      2/116
  Installing       : libvorbis-1:1.3.7-5.el9.x86_64                   3/116
  Installing       : libwayland-client-1.21.0-1.el9.x86_64            4/116
  Installing       : opus-1.3.1-10.el9.x86_64                         5/116
  Installing       : fribidi-1.0.10-6.el9.2.x86_64                    6/116
  Installing       : serd-0.30.12-2.el9.x86_64                        7/116
  Installing       : libvmaf-2.3.0-2.el9.x86_64                       8/116
  Installing       : sord-0.16.10-2.el9.x86_64                        9/116
  Installing       : libX11-xcb-1.7.0-9.el9.x86_64                   10/116
  Installing       : pixman-0.40.0-6.el9_3.x86_64                    11/116
  Installing       : ocl-icd-2.2.13-4.el9.x86_64                     12/116
  Installing       : alsa-lib-1.2.12-1.el9.x86_64                    13/116
  Installing       : libjpeg-turbo-2.0.90-7.el9.x86_64               14/116
  Installing       : mesa-filesystem-24.1.2-3.el9.x86_64             15/116
  Installing       : gsm-1.0.19-6.el9.x86_64                         16/116
  Installing       : shared-mime-info-2.1-5.el9.x86_64               17/116
  Running scriptlet: shared-mime-info-2.1-5.el9.x86_64               17/116
  Installing       : gdk-pixbuf2-2.42.6-4.el9_4.x86_64               18/116
  Installing       : zimg-3.0.5-1.el9.x86_64                         19/116
  Installing       : vapoursynth-libs-57-1.el9.x86_64                20/116
  Installing       : libv4l-1.20.0-5.el9.x86_64                      21/116
  Installing       : x264-libs-0.163-6.20210613git5db6aa6.el9.x86    22/116
  Installing       : sratom-0.6.10-2.el9.x86_64                      23/116
  Installing       : lilv-libs-0.24.14-3.el9.x86_64                  24/116
  Installing       : vmaf-models-2.3.0-2.el9.noarch                  25/116
  Installing       : libwayland-cursor-1.21.0-1.el9.x86_64           26/116
  Installing       : flac-libs-1.3.3-10.el9_2.1.x86_64               27/116
  Installing       : libsndfile-1.0.31-8.el9_5.2.x86_64              28/116
  Installing       : libsamplerate-0.1.9-10.el9.x86_64               29/116
  Running scriptlet: jack-audio-connection-kit-1.9.21-1.el9.x86_6    30/116
  Installing       : jack-audio-connection-kit-1.9.21-1.el9.x86_6    30/116
  Installing       : libtheora-1:1.1.1-31.el9.x86_64                 31/116
  Installing       : zvbi-0.2.35-15.el9.x86_64                       32/116
  Running scriptlet: zvbi-0.2.35-15.el9.x86_64                       32/116
  Installing       : x265-libs-3.5-5.el9.x86_64                      33/116
  Installing       : jellyfin-firewalld-10.8.13-1.el9.noarch         34/116
  Running scriptlet: jellyfin-firewalld-10.8.13-1.el9.noarch         34/116
  Installing       : ladspa-1.13-28.el9.x86_64                       35/116
  Installing       : dotnet-host-9.0.1-1.el9_5.x86_64                36/116
  Installing       : dotnet-hostfxr-6.0-6.0.36-1.el9_5.x86_64        37/116
  Installing       : lttng-ust-2.12.0-6.el9.x86_64                   38/116
  Installing       : fftw-libs-double-3.3.8-12.el9.0.1.x86_64        39/116
  Running scriptlet: xml-common-0.6.3-58.el9.noarch                  40/116
  Installing       : xml-common-0.6.3-58.el9.noarch                  40/116
  Installing       : spirv-tools-libs-2024.2-1.el9.x86_64            41/116
  Installing       : libshaderc-2024.0-1.el9.x86_64                  42/116
  Installing       : openjpeg2-2.4.0-7.el9.x86_64                    43/116
  Installing       : openal-soft-1.19.1-16.el9.x86_64                44/116
  Installing       : lame-libs-3.100-12.el9.x86_64                   45/116
  Installing       : libvpx-1.9.0-8.el9_5.x86_64                     46/116
  Installing       : libcdio-2.1.0-6.el9.x86_64                      47/116
  Installing       : libcdio-paranoia-10.2+2.0.1-6.el9.x86_64        48/116
  Installing       : libglvnd-1:1.3.4-1.el9.x86_64                   49/116
  Installing       : libdatrie-0.2.13-4.el9.x86_64                   50/116
  Installing       : libthai-0.1.28-8.el9.x86_64                     51/116
  Installing       : mpg123-libs-1.32.9-1.el9_5.x86_64               52/116
  Installing       : libopenmpt-0.7.13-1.el9.x86_64                  53/116
  Installing       : libXau-1.0.9-8.el9.x86_64                       54/116
  Installing       : libxcb-1.13.1-9.el9.x86_64                      55/116
  Installing       : speex-1.2.0-11.el9.x86_64                       56/116
  Installing       : llvm-libs-18.1.8-3.el9.x86_64                   57/116
  Installing       : libX11-common-1.7.0-9.el9.noarch                58/116
  Installing       : libX11-1.7.0-9.el9.x86_64                       59/116
  Installing       : libXext-1.3.4-8.el9.x86_64                      60/116
  Installing       : libXrender-0.9.10-16.el9.x86_64                 61/116
  Installing       : libXfixes-5.0.3-16.el9.x86_64                   62/116
  Installing       : libvdpau-1.5-1.el9.x86_64                       63/116
  Installing       : libXxf86vm-1.1.4-18.el9.x86_64                  64/116
  Installing       : libxshmfence-1.3-10.el9.x86_64                  65/116
  Installing       : libasyncns-0.8-22.el9.x86_64                    66/116
  Installing       : pulseaudio-libs-15.0-2.el9.x86_64               67/116
  Installing       : libicu-67.1-9.el9.x86_64                        68/116
  Installing       : dotnet-runtime-6.0-6.0.36-1.el9_5.x86_64        69/116
  Installing       : aspnetcore-runtime-6.0-6.0.36-1.el9_5.x86_64    70/116
  Installing       : libpciaccess-0.16-7.el9.x86_64                  71/116
  Installing       : libdrm-2.4.121-1.el9.x86_64                     72/116
  Installing       : mesa-libglapi-24.1.2-3.el9.x86_64               73/116
  Installing       : mesa-dri-drivers-24.1.2-3.el9.x86_64            74/116
  Installing       : libglvnd-glx-1:1.3.4-1.el9.x86_64               75/116
  Installing       : mesa-libGL-24.1.2-3.el9.x86_64                  76/116
  Installing       : libva-2.20.0-1.el9.x86_64                       77/116
  Installing       : intel-mediasdk-21.3.5-1.el9.x86_64              78/116
  Installing       : at-3.1.23-11.el9.x86_64                         79/116
  Running scriptlet: at-3.1.23-11.el9.x86_64                         79/116
Created symlink /etc/systemd/system/multi-user.target.wants/atd.service → /usr/lib/systemd/system/atd.service.

  Installing       : graphite2-1.3.14-9.el9.x86_64                   80/116
  Installing       : freetype-2.10.4-9.el9.x86_64                    81/116
  Installing       : harfbuzz-2.7.4-10.el9.x86_64                    82/116
  Installing       : fontconfig-2.14.0-2.el9_1.x86_64                83/116
  Running scriptlet: fontconfig-2.14.0-2.el9_1.x86_64                83/116
  Installing       : cairo-1.17.4-7.el9.x86_64                       84/116
  Installing       : cairo-gobject-1.17.4-7.el9.x86_64               85/116
  Installing       : libass-0.17.1-1.el9.x86_64                      86/116
  Installing       : libXft-2.3.3-8.el9.x86_64                       87/116
  Installing       : pango-1.48.7-3.el9.x86_64                       88/116
  Installing       : libdecor-0.1.1-1.el9.x86_64                     89/116
  Installing       : SDL2-2.26.0-1.el9.x86_64                        90/116
  Installing       : librsvg2-2.50.7-3.el9.x86_64                    91/116
  Installing       : xvidcore-1.3.7-9.el9.x86_64                     92/116
  Installing       : vo-amrwbenc-0.1.3-18.el9.x86_64                 93/116
  Installing       : vid.stab-1.1.0-14.20201110gitf9166e9.el9.x86    94/116
  Installing       : vamp-plugin-sdk-2.9.0-4.el9.x86_64              95/116
  Installing       : svt-av1-libs-0.9.0-1.el9.x86_64                 96/116
  Installing       : srt-libs-1.4.4-1.el9.x86_64                     97/116
  Installing       : soxr-0.1.3-11.el9.x86_64                        98/116
  Installing       : opencore-amr-0.1.6-3.el9.x86_64                 99/116
  Installing       : lv2-1.18.8-4.el9.x86_64                        100/116
  Installing       : rubberband-3.1.3-2.el9.x86_64                  101/116
  Installing       : libudfread-1.1.2-2.el9.x86_64                  102/116
  Installing       : libbluray-1.3.4-1.el9.x86_64                   103/116
  Installing       : libmysofa-1.2.1-1.el9.x86_64                   104/116
  Installing       : libmodplug-1:0.8.9.0-13.el9.x86_64             105/116
  Installing       : libdav1d-1.5.0-2.el9.x86_64                    106/116
  Installing       : highway-1.2.0-2.el9.x86_64                     107/116
  Installing       : jxl-pixbuf-loader-0.7.0-1.el9.x86_64           108/116
  Installing       : libjxl-0.7.0-1.el9.x86_64                      109/116
  Installing       : libaom-3.9.0-1.el9.x86_64                      110/116
  Installing       : ffmpeg-libs-5.1.6-2.el9.x86_64                 111/116
  Installing       : libavdevice-5.1.6-2.el9.x86_64                 112/116
  Installing       : ffmpeg-5.1.6-2.el9.x86_64                      113/116
  Running scriptlet: jellyfin-server-10.8.13-1.el9.x86_64           114/116
  Installing       : jellyfin-server-10.8.13-1.el9.x86_64           114/116
  Running scriptlet: jellyfin-server-10.8.13-1.el9.x86_64           114/116
  Installing       : jellyfin-web-10.8.13-1.el9.noarch              115/116
  Installing       : jellyfin-10.8.13-1.el9.x86_64                  116/116
  Running scriptlet: fontconfig-2.14.0-2.el9_1.x86_64               116/116
  Running scriptlet: jellyfin-server-10.8.13-1.el9.x86_64           116/116
  Running scriptlet: jellyfin-10.8.13-1.el9.x86_64                  116/116
  Verifying        : highway-1.2.0-2.el9.x86_64                       1/116
  Verifying        : intel-mediasdk-21.3.5-1.el9.x86_64               2/116
  Verifying        : jack-audio-connection-kit-1.9.21-1.el9.x86_6     3/116
  Verifying        : jxl-pixbuf-loader-0.7.0-1.el9.x86_64             4/116
  Verifying        : libaom-3.9.0-1.el9.x86_64                        5/116
  Verifying        : libass-0.17.1-1.el9.x86_64                       6/116
  Verifying        : libbluray-1.3.4-1.el9.x86_64                     7/116
  Verifying        : libdav1d-1.5.0-2.el9.x86_64                      8/116
  Verifying        : libjxl-0.7.0-1.el9.x86_64                        9/116
  Verifying        : libmodplug-1:0.8.9.0-13.el9.x86_64              10/116
  Verifying        : libmysofa-1.2.1-1.el9.x86_64                    11/116
  Verifying        : libopenmpt-0.7.13-1.el9.x86_64                  12/116
  Verifying        : libudfread-1.1.2-2.el9.x86_64                   13/116
  Verifying        : libvmaf-2.3.0-2.el9.x86_64                      14/116
  Verifying        : lilv-libs-0.24.14-3.el9.x86_64                  15/116
  Verifying        : lv2-1.18.8-4.el9.x86_64                         16/116
  Verifying        : opencore-amr-0.1.6-3.el9.x86_64                 17/116
  Verifying        : rubberband-3.1.3-2.el9.x86_64                   18/116
  Verifying        : serd-0.30.12-2.el9.x86_64                       19/116
  Verifying        : sord-0.16.10-2.el9.x86_64                       20/116
  Verifying        : soxr-0.1.3-11.el9.x86_64                        21/116
  Verifying        : sratom-0.6.10-2.el9.x86_64                      22/116
  Verifying        : srt-libs-1.4.4-1.el9.x86_64                     23/116
  Verifying        : svt-av1-libs-0.9.0-1.el9.x86_64                 24/116
  Verifying        : vamp-plugin-sdk-2.9.0-4.el9.x86_64              25/116
  Verifying        : vapoursynth-libs-57-1.el9.x86_64                26/116
  Verifying        : vid.stab-1.1.0-14.20201110gitf9166e9.el9.x86    27/116
  Verifying        : vmaf-models-2.3.0-2.el9.noarch                  28/116
  Verifying        : vo-amrwbenc-0.1.3-18.el9.x86_64                 29/116
  Verifying        : xvidcore-1.3.7-9.el9.x86_64                     30/116
  Verifying        : zimg-3.0.5-1.el9.x86_64                         31/116
  Verifying        : zvbi-0.2.35-15.el9.x86_64                       32/116
  Verifying        : harfbuzz-2.7.4-10.el9.x86_64                    33/116
  Verifying        : graphite2-1.3.14-9.el9.x86_64                   34/116
  Verifying        : at-3.1.23-11.el9.x86_64                         35/116
  Verifying        : libpciaccess-0.16-7.el9.x86_64                  36/116
  Verifying        : libicu-67.1-9.el9.x86_64                        37/116
  Verifying        : freetype-2.10.4-9.el9.x86_64                    38/116
  Verifying        : libpng-2:1.6.37-12.el9.x86_64                   39/116
  Verifying        : shared-mime-info-2.1-5.el9.x86_64               40/116
  Verifying        : SDL2-2.26.0-1.el9.x86_64                        41/116
  Verifying        : fribidi-1.0.10-6.el9.2.x86_64                   42/116
  Verifying        : fontconfig-2.14.0-2.el9_1.x86_64                43/116
  Verifying        : libasyncns-0.8-22.el9.x86_64                    44/116
  Verifying        : libsamplerate-0.1.9-10.el9.x86_64               45/116
  Verifying        : libxshmfence-1.3-10.el9.x86_64                  46/116
  Verifying        : libXfixes-5.0.3-16.el9.x86_64                   47/116
  Verifying        : libogg-2:1.3.4-6.el9.x86_64                     48/116
  Verifying        : libX11-common-1.7.0-9.el9.noarch                49/116
  Verifying        : llvm-libs-18.1.8-3.el9.x86_64                   50/116
  Verifying        : libva-2.20.0-1.el9.x86_64                       51/116
  Verifying        : speex-1.2.0-11.el9.x86_64                       52/116
  Verifying        : gsm-1.0.19-6.el9.x86_64                         53/116
  Verifying        : libXau-1.0.9-8.el9.x86_64                       54/116
  Verifying        : libdecor-0.1.1-1.el9.x86_64                     55/116
  Verifying        : libxcb-1.13.1-9.el9.x86_64                      56/116
  Verifying        : mesa-libglapi-24.1.2-3.el9.x86_64               57/116
  Verifying        : mesa-libGL-24.1.2-3.el9.x86_64                  58/116
  Verifying        : mesa-filesystem-24.1.2-3.el9.x86_64             59/116
  Verifying        : mesa-dri-drivers-24.1.2-3.el9.x86_64            60/116
  Verifying        : libvdpau-1.5-1.el9.x86_64                       61/116
  Verifying        : libXrender-0.9.10-16.el9.x86_64                 62/116
  Verifying        : flac-libs-1.3.3-10.el9_2.1.x86_64               63/116
  Verifying        : libdrm-2.4.121-1.el9.x86_64                     64/116
  Verifying        : libsndfile-1.0.31-8.el9_5.2.x86_64              65/116
  Verifying        : mpg123-libs-1.32.9-1.el9_5.x86_64               66/116
  Verifying        : libjpeg-turbo-2.0.90-7.el9.x86_64               67/116
  Verifying        : libXft-2.3.3-8.el9.x86_64                       68/116
  Verifying        : libXext-1.3.4-8.el9.x86_64                      69/116
  Verifying        : libdatrie-0.2.13-4.el9.x86_64                   70/116
  Verifying        : libvorbis-1:1.3.7-5.el9.x86_64                  71/116
  Verifying        : libglvnd-glx-1:1.3.4-1.el9.x86_64               72/116
  Verifying        : libglvnd-1:1.3.4-1.el9.x86_64                   73/116
  Verifying        : libtheora-1:1.1.1-31.el9.x86_64                 74/116
  Verifying        : libcdio-2.1.0-6.el9.x86_64                      75/116
  Verifying        : librsvg2-2.50.7-3.el9.x86_64                    76/116
  Verifying        : libvpx-1.9.0-8.el9_5.x86_64                     77/116
  Verifying        : alsa-lib-1.2.12-1.el9.x86_64                    78/116
  Verifying        : libthai-0.1.28-8.el9.x86_64                     79/116
  Verifying        : lame-libs-3.100-12.el9.x86_64                   80/116
  Verifying        : libXxf86vm-1.1.4-18.el9.x86_64                  81/116
  Verifying        : openal-soft-1.19.1-16.el9.x86_64                82/116
  Verifying        : opus-1.3.1-10.el9.x86_64                        83/116
  Verifying        : openjpeg2-2.4.0-7.el9.x86_64                    84/116
  Verifying        : ocl-icd-2.2.13-4.el9.x86_64                     85/116
  Verifying        : libwayland-cursor-1.21.0-1.el9.x86_64           86/116
  Verifying        : libwayland-client-1.21.0-1.el9.x86_64           87/116
  Verifying        : pixman-0.40.0-6.el9_3.x86_64                    88/116
  Verifying        : spirv-tools-libs-2024.2-1.el9.x86_64            89/116
  Verifying        : xml-common-0.6.3-58.el9.noarch                  90/116
  Verifying        : pulseaudio-libs-15.0-2.el9.x86_64               91/116
  Verifying        : dotnet-runtime-6.0-6.0.36-1.el9_5.x86_64        92/116
  Verifying        : dotnet-hostfxr-6.0-6.0.36-1.el9_5.x86_64        93/116
  Verifying        : aspnetcore-runtime-6.0-6.0.36-1.el9_5.x86_64    94/116
  Verifying        : pango-1.48.7-3.el9.x86_64                       95/116
  Verifying        : fftw-libs-double-3.3.8-12.el9.0.1.x86_64        96/116
  Verifying        : cairo-gobject-1.17.4-7.el9.x86_64               97/116
  Verifying        : cairo-1.17.4-7.el9.x86_64                       98/116
  Verifying        : libX11-xcb-1.7.0-9.el9.x86_64                   99/116
  Verifying        : libX11-1.7.0-9.el9.x86_64                      100/116
  Verifying        : libcdio-paranoia-10.2+2.0.1-6.el9.x86_64       101/116
  Verifying        : lttng-ust-2.12.0-6.el9.x86_64                  102/116
  Verifying        : gdk-pixbuf2-2.42.6-4.el9_4.x86_64              103/116
  Verifying        : libv4l-1.20.0-5.el9.x86_64                     104/116
  Verifying        : libshaderc-2024.0-1.el9.x86_64                 105/116
  Verifying        : dotnet-host-9.0.1-1.el9_5.x86_64               106/116
  Verifying        : ladspa-1.13-28.el9.x86_64                      107/116
  Verifying        : ffmpeg-5.1.6-2.el9.x86_64                      108/116
  Verifying        : ffmpeg-libs-5.1.6-2.el9.x86_64                 109/116
  Verifying        : jellyfin-10.8.13-1.el9.x86_64                  110/116
  Verifying        : jellyfin-firewalld-10.8.13-1.el9.noarch        111/116
  Verifying        : jellyfin-server-10.8.13-1.el9.x86_64           112/116
  Verifying        : jellyfin-web-10.8.13-1.el9.noarch              113/116
  Verifying        : libavdevice-5.1.6-2.el9.x86_64                 114/116
  Verifying        : x264-libs-0.163-6.20210613git5db6aa6.el9.x86   115/116
  Verifying        : x265-libs-3.5-5.el9.x86_64                     116/116

Installed:
  SDL2-2.26.0-1.el9.x86_64
  alsa-lib-1.2.12-1.el9.x86_64
  aspnetcore-runtime-6.0-6.0.36-1.el9_5.x86_64
  at-3.1.23-11.el9.x86_64
  cairo-1.17.4-7.el9.x86_64
  cairo-gobject-1.17.4-7.el9.x86_64
  dotnet-host-9.0.1-1.el9_5.x86_64
  dotnet-hostfxr-6.0-6.0.36-1.el9_5.x86_64
  dotnet-runtime-6.0-6.0.36-1.el9_5.x86_64
  ffmpeg-5.1.6-2.el9.x86_64
  ffmpeg-libs-5.1.6-2.el9.x86_64
  fftw-libs-double-3.3.8-12.el9.0.1.x86_64
  flac-libs-1.3.3-10.el9_2.1.x86_64
  fontconfig-2.14.0-2.el9_1.x86_64
  freetype-2.10.4-9.el9.x86_64
  fribidi-1.0.10-6.el9.2.x86_64
  gdk-pixbuf2-2.42.6-4.el9_4.x86_64
  graphite2-1.3.14-9.el9.x86_64
  gsm-1.0.19-6.el9.x86_64
  harfbuzz-2.7.4-10.el9.x86_64
  highway-1.2.0-2.el9.x86_64
  intel-mediasdk-21.3.5-1.el9.x86_64
  jack-audio-connection-kit-1.9.21-1.el9.x86_64
  jellyfin-10.8.13-1.el9.x86_64
  jellyfin-firewalld-10.8.13-1.el9.noarch
  jellyfin-server-10.8.13-1.el9.x86_64
  jellyfin-web-10.8.13-1.el9.noarch
  jxl-pixbuf-loader-0.7.0-1.el9.x86_64
  ladspa-1.13-28.el9.x86_64
  lame-libs-3.100-12.el9.x86_64
  libX11-1.7.0-9.el9.x86_64
  libX11-common-1.7.0-9.el9.noarch
  libX11-xcb-1.7.0-9.el9.x86_64
  libXau-1.0.9-8.el9.x86_64
  libXext-1.3.4-8.el9.x86_64
  libXfixes-5.0.3-16.el9.x86_64
  libXft-2.3.3-8.el9.x86_64
  libXrender-0.9.10-16.el9.x86_64
  libXxf86vm-1.1.4-18.el9.x86_64
  libaom-3.9.0-1.el9.x86_64
  libass-0.17.1-1.el9.x86_64
  libasyncns-0.8-22.el9.x86_64
  libavdevice-5.1.6-2.el9.x86_64
  libbluray-1.3.4-1.el9.x86_64
  libcdio-2.1.0-6.el9.x86_64
  libcdio-paranoia-10.2+2.0.1-6.el9.x86_64
  libdatrie-0.2.13-4.el9.x86_64
  libdav1d-1.5.0-2.el9.x86_64
  libdecor-0.1.1-1.el9.x86_64
  libdrm-2.4.121-1.el9.x86_64
  libglvnd-1:1.3.4-1.el9.x86_64
  libglvnd-glx-1:1.3.4-1.el9.x86_64
  libicu-67.1-9.el9.x86_64
  libjpeg-turbo-2.0.90-7.el9.x86_64
  libjxl-0.7.0-1.el9.x86_64
  libmodplug-1:0.8.9.0-13.el9.x86_64
  libmysofa-1.2.1-1.el9.x86_64
  libogg-2:1.3.4-6.el9.x86_64
  libopenmpt-0.7.13-1.el9.x86_64
  libpciaccess-0.16-7.el9.x86_64
  libpng-2:1.6.37-12.el9.x86_64
  librsvg2-2.50.7-3.el9.x86_64
  libsamplerate-0.1.9-10.el9.x86_64
  libshaderc-2024.0-1.el9.x86_64
  libsndfile-1.0.31-8.el9_5.2.x86_64
  libthai-0.1.28-8.el9.x86_64
  libtheora-1:1.1.1-31.el9.x86_64
  libudfread-1.1.2-2.el9.x86_64
  libv4l-1.20.0-5.el9.x86_64
  libva-2.20.0-1.el9.x86_64
  libvdpau-1.5-1.el9.x86_64
  libvmaf-2.3.0-2.el9.x86_64
  libvorbis-1:1.3.7-5.el9.x86_64
  libvpx-1.9.0-8.el9_5.x86_64
  libwayland-client-1.21.0-1.el9.x86_64
  libwayland-cursor-1.21.0-1.el9.x86_64
  libxcb-1.13.1-9.el9.x86_64
  libxshmfence-1.3-10.el9.x86_64
  lilv-libs-0.24.14-3.el9.x86_64
  llvm-libs-18.1.8-3.el9.x86_64
  lttng-ust-2.12.0-6.el9.x86_64
  lv2-1.18.8-4.el9.x86_64
  mesa-dri-drivers-24.1.2-3.el9.x86_64
  mesa-filesystem-24.1.2-3.el9.x86_64
  mesa-libGL-24.1.2-3.el9.x86_64
  mesa-libglapi-24.1.2-3.el9.x86_64
  mpg123-libs-1.32.9-1.el9_5.x86_64
  ocl-icd-2.2.13-4.el9.x86_64
  openal-soft-1.19.1-16.el9.x86_64
  opencore-amr-0.1.6-3.el9.x86_64
  openjpeg2-2.4.0-7.el9.x86_64
  opus-1.3.1-10.el9.x86_64
  pango-1.48.7-3.el9.x86_64
  pixman-0.40.0-6.el9_3.x86_64
  pulseaudio-libs-15.0-2.el9.x86_64
  rubberband-3.1.3-2.el9.x86_64
  serd-0.30.12-2.el9.x86_64
  shared-mime-info-2.1-5.el9.x86_64
  sord-0.16.10-2.el9.x86_64
  soxr-0.1.3-11.el9.x86_64
  speex-1.2.0-11.el9.x86_64
  spirv-tools-libs-2024.2-1.el9.x86_64
  sratom-0.6.10-2.el9.x86_64
  srt-libs-1.4.4-1.el9.x86_64
  svt-av1-libs-0.9.0-1.el9.x86_64
  vamp-plugin-sdk-2.9.0-4.el9.x86_64
  vapoursynth-libs-57-1.el9.x86_64
  vid.stab-1.1.0-14.20201110gitf9166e9.el9.x86_64
  vmaf-models-2.3.0-2.el9.noarch
  vo-amrwbenc-0.1.3-18.el9.x86_64
  x264-libs-0.163-6.20210613git5db6aa6.el9.x86_64
  x265-libs-3.5-5.el9.x86_64
  xml-common-0.6.3-58.el9.noarch
  xvidcore-1.3.7-9.el9.x86_64
  zimg-3.0.5-1.el9.x86_64
  zvbi-0.2.35-15.el9.x86_64

Complete!
```
### 🌞 Lancer le service jellyfin
```bash
[rock-bji@music ~]$ sudo systemctl start jellyfin
[sudo] password for rock-bji:
```
### 🌞 Afficher la liste des ports TCP en écoute
```bash
[rock-bji@music ~]$ sudo ss -tuln | grep ':8096'
tcp   LISTEN 0      512          0.0.0.0:8096       0.0.0.0:*
```
### 🌞 Ouvrir le port derrière lequel Jellyfin écoute
```bash
[rock-bji@music ~]$ sudo firewall-cmd --add-port=8096/tcp --permanent
success
[rock-bji@music ~]$ sudo firewall-cmd --reload
success
```
### 🌞 Visiter l'interface Web de Jellyfin
```bash
jerem@hpvictusBJI MINGW64 ~
$ curl -L http://192.168.20.17:8096
<!doctype html><html class="preload"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover"><link rel="manifest" href="64d966784cd77b03a79c.json"><meta name="format-detection" content="telephone=no"><meta name="msapplication-tap-highlight" content="no"><meta http-equiv="X-UA-Compatibility" content="IE=Edge"><meta name="apple-mobile-web-app-capable" content="yes"><meta name="mobile-web-app-capable" content="yes"><meta name="application-name" content="Jellyfin"><meta name="robots" content="noindex, nofollow, noarchive"><meta name="referrer" content="no-referrer"><meta property="og:title" content="Jellyfin"><meta property="og:site_name" content="Jellyfin"><meta property="og:url" content="http://jellyfin.org"><meta property="og:description" content="The Free Software Media System"><meta property="og:type" content="article"><meta id="themeColor" name="theme-color" content="#202020"><link rel="apple-touch-icon" sizes="180x180" href="f5bbb798cb2c65908633.png"><link href="6a2e2e6b4186720e5d4f.png" media="screen and (device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="eb8bef4f19b6ad227f46.png" media="screen and (device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="3fa90c593184d5737eb3.png" media="screen and (device-width: 375px) and (device-height: 667px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="23a72f5d56f82554aeab.png" media="screen and (device-width: 375px) and (device-height: 667px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="d28a57b1e61f9f0dabd9.png" media="screen and (device-width: 414px) and (device-height: 736px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="16fc81178d1aee54f6cc.png" media="screen and (device-width: 414px) and (device-height: 736px) and (-webkit-device-pixel-ratio: 3) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="f94ebf203ea0c91a47c6.png" media="screen and (device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="522fa270807b7b12a9ba.png" media="screen and (device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="0df719b48efcaef953df.png" media="screen and (device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="0b37f660ac0f7f01ab41.png" media="screen and (device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="d0e56683308a17dba86d.png" media="screen and (device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="baafa93a783b76e667ec.png" media="screen and (device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 3) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="379bab68d056910336f9.png" media="screen and (device-width: 768px) and (device-height: 1024px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="d31413d3f03c0873ccbb.png" media="screen and (device-width: 768px) and (device-height: 1024px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="49d14d0eb7bcdf6f2d1b.png" media="screen and (device-width: 834px) and (device-height: 1112px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="bbb3e6d43389ba0d436c.png" media="screen and (device-width: 834px) and (device-height: 1112px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="142d834c201895a46a01.png" media="screen and (device-width: 834px) and (device-height: 1194px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="e62987a12a58b24f383a.png" media="screen and (device-width: 834px) and (device-height: 1194px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link href="3f3fe0fd3a0b637b5030.png" media="screen and (device-width: 1024px) and (device-height: 1366px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)" rel="apple-touch-startup-image"/><link href="a962662957ebbb8eb436.png" media="screen and (device-width: 1024px) and (device-height: 1366px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)" rel="apple-touch-startup-image"/><link rel="shortcut icon" href="bc8d51405ec040305a87.ico"><meta name="msapplication-TileImage" content="39209dd2362c0db7c673.png"><meta name="msapplication-TileColor" content="#333333"><title>Jellyfin</title><style>.backgroundContainer-transparent:not(.withBackdrop),.transparentDocument{background:0 0!important;background-color:transparent!important}.layout-tv .mouseIdle,.layout-tv .mouseIdle a,.layout-tv .mouseIdle button,.layout-tv .mouseIdle input,.layout-tv .mouseIdle label,.layout-tv .mouseIdle select,.layout-tv .mouseIdle textarea,.screensaver-noScroll.mouseIdle,.screensaver-noScroll.mouseIdle a,.screensaver-noScroll.mouseIdle button,.screensaver-noScroll.mouseIdle input,.screensaver-noScroll.mouseIdle label,.screensaver-noScroll.mouseIdle select,.screensaver-noScroll.mouseIdle textarea,.transparentDocument .mouseIdle,.transparentDocument .mouseIdle a,.transparentDocument .mouseIdle button,.transparentDocument .mouseIdle input,.transparentDocument .mouseIdle label,.transparentDocument .mouseIdle select,.transparentDocument .mouseIdle textarea{cursor:none!important}.preload{background-color:#101010}.hide,.mouseIdle .hide-mouse-idle,.mouseIdle-tv .hide-mouse-idle-tv{display:none!important}.mainDrawerHandle{position:fixed;top:0;left:0;bottom:0;z-index:1;width:.8em}@-webkit-keyframes fadein{from{opacity:0}to{opacity:1}}@keyframes fadein{from{opacity:0}to{opacity:1}}.splashLogo{-webkit-animation:fadein .5s;animation:fadein .5s;width:30%;height:30%;background-image:url(assets/img/icon-transparent.png);background-position:center center;background-repeat:no-repeat;background-size:contain;position:fixed;top:50%;left:50%;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%)}@media screen and (min-device-width:992px){.splashLogo{background-image:url(assets/img/banner-light.png)}}</style><script defer="defer" src="main.jellyfin.bundle.js?d0b85f6e4b2ff93c2f0b"></script></head><body><div class="backdropContainer"></div><div class="backgroundContainer"></div><div class="mainDrawer hide"><div class="mainDrawer-scrollContainer scrollContainer focuscontainer-y"></div></div><div class="skinHeader focuscontainer-x"></div><div class="mainAnimatedPages skinBody"><div class="splashLogo"></div></div><div class="mainDrawerHandle"></div></body></html>
jerem@hpvictusBJI MINGW64 ~
```

