# Racket Portable


## Introduction


## How to Create Portable Installer
I was looking for a portable installer for Racket  when I came across this article: [Portable Racket for Windows Users](https://www.wisdomandwonder.com/link/5656/portable-racket-for-windows-users).

It provides us with a template for creating a portable installer in the portableapps.com standard. Then I decided to clone the original repository (which uses Mercurial) for my own use. 


## Instructions
I wrote a step by step routine considering that I'll create aportable installer for Racket version 7.7 32 bits. Adjust instructions according to your environment and version you downloaded.

### 1. Requirements
1.1. Clone this repository in your C: drive. I'd recommend you to create a sub folder. For instance, I cloned the project to `C:\Users\plica\convert_to_portable\`. It means, my git repository will be at `C:\Users\plica\convert_to_portable\racket-portable`.

1.2. Install PortableApps.com Platform. You can get it [here](https://portableapps.com/download). I recommend you install it in your pendrive or external hard disc.

1.3. Install NSIS Portable, PortableApps.com Launcher and PortableApps.com Installer .  Use PortableApps.com Platform to install (you could download them directly and manually install them, but it will be much more work IMHO).

1.4. Download the Racket Installer. You can get the most  recent  one from (here)[https://download.racket-lang.org/). You can download both 32 and 64 bits versions. 32 bits version has the advantage of working in both systems.

1.5. Install Racket into the App/Racket subdirectory of the cloned repositpry. In my example, I would Install Racket in  `C:\Users\plica\convert_to_portable\racket-portable\App\Racket`.

1.6. Move Racket uninstaller to aonther folder (for instance, to C:). You will need it later in order to uninstall the non-portable version of Racket you just installed in step 1.5.

### 2. Generate Portable Installer

2.1. Using regedit search for ***Racket***. If you've installed a 32 bits version you will find something like `Racket-i386-7.7`. For a 64 bits version you will see something like  `Racket-x86_64-7.7`.

2.2. Open file `App\AppInfo\appinfo.ini` (in my example, it is at `C:\Users\plica\convert_to_portable\racket-portable\App\AppInfo\appinfo.ini`) and edit fields **PackageVersion** and **DisplayVersion** so they will have the current version of Racket.
Note: PackageVersion and DisplayVersion fields require 4 and 3 digits, respectivelly. So, in our example, as Racket version is 7.7, we will have
```python
[Version]
PackageVersion=7.7.0.0
DisplayVersion=7.7.0
```

2.3. Open file `App\AppInfo\Launcher\RacketPortable.ini` (in my example, it is at `C:\Users\plica\convert_to_portable\racket-portable\App\AppInfo\Launcher\RacketPortable.ini`) and edit fields of sections `[RegistryKeys]` and `[RegistryValueWrite]` with the value you found on step 2.1 (`Racket-i386-7.7` in my case).
You will have something like that:
```python
[RegistryKeys]
-=HKCU\Software\Racket-i386-7.7

[RegistryValueWrite]
HKCU\Software\Racket-i386-7.7\=REG_SZ:%PAL:AppDir%\Racket
```

2.4. Run PortableApps.com Launcher and select the root of the cloned project. In my example, it is `C:\Users\plica\convert_to_portable\racket-portable`. Click Go. I recommend that in the last screen you mark both __Test Launcher__ and __view log file__. You should be able to start DrRacket. In case it doesn't happen then you should take a look at the log file.

2.5. Run PortableApps.com Installer and select the root of the cloned project. In my example, it is `C:\Users\plica\convert_to_portable\racket-portable`. Click Go. I recommend that in the last screen you mark both __Test Installer__ and __view log file__.
If everything went right you will have your portable version of Racket installer. It will be named something like RacketPortable_<version>.paf.exe (in my example, it will be named RacketPortable_7.7.0.paf.exe).
You can find the installer at the same level as the folder you cloned (racket-portable). In my case, executable will be located at `C:\Users\plica\convert_to_portable\`.

2.6. Do you remember were you put the uninstaller we moved from Racket folder in step 1.6? Now move it back to its original folder (in my example, it is `C:\Users\plica\convert_to_portable\racket-portable\App\Racket`).
After that you can run it to remove the Racket we installed in step 1.5.

2.7. Enjoy your portable Racket installer.


## Acknowledgements
I would like to thank [Wisdom And Wonder](https://www.wisdomandwonder.com/). He is the author of the template I use to generate the portable version of Racket. All kudos go to him.
