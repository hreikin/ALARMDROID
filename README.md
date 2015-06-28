ALARMDROID
==========
This repo contains PKGBUILDS and other needed files for Odroid U3 Arch Linux related packages that i use for my new ALARM U3 image.

To install simply build the package with the _PKGBUILD_ and _makepkg -s_ and then install the resulting _pkg.tar.xz_ file with pacman.

How To Manually Build/Install
-----------------------------
Change directory to where you want to clone the repo :
```
$ cd git
```
Then clone the repo :
```
$ git clone https://github.com/hreikin/ALARMDROID.git
```
Then change directory into the file you wish to install, for example _xbmc-odroid_ :
```
$ cd xbmc-odroid
```
Then take a look at the _PKGBUILD_ to check everything is ok with nano before running _makepkg -s_ :
```
$ nano PKGBUILD
$ makepkg -s
```
Once _makepkg_ finishes it will create a _pkg.tar.xz_ file which can be installed with pacman like so :
```
$ sudo pacman -U xbmc-odroid-20140901.867305b-1-armv7h.pkg.tar.xz
```
Once you have all the files installed you need to edit your _/etc/xorg.conf_ mine has :
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

Install From My Repo
--------------------
Alternatively you can install my successful builds which are hosted in a repo for quick installation. Simply edit your _/etc/pacman.conf_ and add these few lines to the bottom of the file :
```
[odroidu]
SigLevel = Never
Server = http://oph.mdrjr.net/hreikin/repo
```
Then update pacman and install the desired packages in the usual manner, like so :
```
sudo pacman -Syu
```
```
sudo pacman -S xbmc-odroid
```
