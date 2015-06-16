ALARMDROID
==========
This repo contains PKGBUILDS and other needed files for Odroid related packages that i may need to use for my new ALARM U3 image, it is still very WIP and PKGREL/PKGVER/ETC may need bumping !

To install simply build the package with the `PKGBUILD` and `makepkg -s` and then install the resulting `pkg.tar.xz` file with pacman. The packages i recommend you install are :
```
odroid-libgl-mali
mesa-noegl
```
You will also need these packages from the official repos (amongst others) :
```
linux-odroid-u2
xf86-video-armsoc-odroid
xf86-video-fbturbo-git
xf86-video-fbdev
mesa-libgl
```
How to Build/Install
--------------------
Change directory to where you want to clone the repo :
```
$ cd git
```
Then clone the repo :
```
$ git clone https://github.com/hreikin/ALARMDROID.git
```
Then change directory into the file you wish to install, for example odroid-libgl-mali :
```
$ cd odroid-libgl-mali
```
Then take a look at the 'PKGBUILD' to check everything is ok with nano before running 'makepkg -s' :
```
$ nano PKGBUILD
$ makepkg -s
```
Once 'makepkg' finishes it will create a 'pkg.tar.xz' file (maybe more than 1!) which can be installed with pacman like so :
```
$ sudo pacman -U odroid-libgl-mali-r4p0-2-armv7h.pkg.tar.xz
```
Once you have all the files installed you need to edit your '/etc/xorg.conf' mine has :
```
# X.Org X server configuration file for xfree86-video-mali

Section "Device"
	Identifier 	"Mali-Fbdev"
	Driver		"armsoc"
	Option		"fbdev"           	"/dev/fb1"
	Option  	"Debug" 		"false"
	Option		"DPMS"			"false"
	Option		"Fimg2DExa"		"false"
	Option		"DRI2"			"true"
	Option		"DRI2_PAGE_FLIP"	"false"
#	Option		"Fimg2DExaSolid"	"false"
#	Option		"Fimg2DExaCopy"		"false"
#	Option		"Fimg2DExaComposite"	"false"
        Option          "SWcursorLCD"           "false"
EndSection

Section "Screen"
	Identifier   "Default Screen"
	Device       "Mali-Fbdev"
	DefaultDepth 24
EndSection

Section "DRI"
	Mode 0666
EndSection
```
