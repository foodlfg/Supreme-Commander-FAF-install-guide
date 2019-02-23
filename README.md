# Supreme-Commander-FAF-install-guide
Supreme Commander FAF install guide on Ubuntu
18.04 LTS, 18.10


It works!
So if you have problems running the game/client on Ubuntu 18.04, follow the steps below.
The wiki is outdated but still useful.
https://wiki.faforever.com/index.php?title=Setting_Up_FAF_Linux


## System properties
- **Ubuntu 18.04 LTS, 18.10**

_test1@comp1:~$ uname -a_

    Linux comp1 4.15.0-20-generic #21-Ubuntu SMP Tue Apr 24 06:16:15 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

- **Wine**, custom downloaded by Lutris or PlayOnLinux (see below)

  - Wine v3.10, v3.16, v4.0 - are tested and they work
  - System default Wine v3.0 cannot run the game

- **Graphics info**

_test1@comp1:~$ glxinfo | grep 'version'_

    server glx version string: 1.4
    client glx version string: 1.4
    GLX version: 1.4
        Max core profile version: 4.5
        Max compat profile version: 3.0
        Max GLES1 profile version: 1.1
        Max GLES[23] profile version: 3.1
    OpenGL core profile version string: 4.5 (Core Profile) Mesa 18.0.0-rc5
    OpenGL core profile shading language version string: 4.50
    OpenGL version string: 3.0 Mesa 18.0.0-rc5
    OpenGL shading language version string: 1.30
    OpenGL ES profile version string: OpenGL ES 3.1 Mesa 18.0.0-rc5
    OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.10

test1@comp1:~$ glxinfo | grep 'Extended renderer info' -A 30
[code]Extended renderer info (GLX_MESA_query_renderer):
    Vendor: X.Org (0x1002)
    Device: Radeon RX 560 Series (POLARIS11 / DRM 3.23.0 / 4.15.0-20-generic, LLVM 6.0.0) (0x67ff)
    Version: 18.0.0
    Accelerated: yes
    Video memory: 4062MB
    Unified memory: no
    Preferred profile: core (0x1)
    Max core profile version: 4.5
    Max compat profile version: 3.0
    Max GLES1 profile version: 1.1
    Max GLES[23] profile version: 3.1
Memory info (GL_ATI_meminfo):
    VBO free memory - total: 4062 MB, largest block: 4062 MB
    VBO free aux. memory - total: 4092 MB, largest block: 4092 MB
    Texture free memory - total: 4062 MB, largest block: 4062 MB
    Texture free aux. memory - total: 4092 MB, largest block: 4092 MB
    Renderbuffer free memory - total: 4062 MB, largest block: 4062 MB
    Renderbuffer free aux. memory - total: 4092 MB, largest block: 4092 MB
Memory info (GL_NVX_gpu_memory_info):
    Dedicated video memory: 4062 MB
    Total available memory: 8156 MB
    Currently available dedicated video memory: 4062 MB
OpenGL vendor string: X.Org
OpenGL renderer string: Radeon RX 560 Series (POLARIS11 / DRM 3.23.0 / 4.15.0-20-generic, LLVM 6.0.0)
OpenGL core profile version string: 4.5 (Core Profile) Mesa 18.0.0-rc5
OpenGL core profile shading language version string: 4.50
OpenGL core profile context flags: (none)
OpenGL core profile profile mask: core profile
OpenGL core profile extensions:
    GL_AMD_conservative_depth, GL_AMD_draw_buffers_blend, [/code]


[b][size=150]Installing the game[/size][/b]
[b]0.0[/b]
Install Lutris or PlayOnLinux that can install Windows Steam and can download the Wine version that can be seen above. Steam can install the game and the necessary libraries.
https://lutris.net/downloads/
If you are a terminal/Wine ninja and you are ok with compiling Wine v3.10 for the system (system default Wine 3.0 is no good) then don't install Lutris or PlayOnLinux, just Wine should be enough.


[b]0.1[/b]
Install Steam windows version (I've bought the game on Steam)
It gave me an error when downloading the game (it's a new Steam-Wine compatibility bug):
Editing the Steam config file solved it:
https://www.reddit.com/r/wine_gaming/comments/8r0gh6/steam_in_winedevel_content_servers_unreachable/e0riqd9/
Short version:
Install Linux Steam, download a random game (ex: Doki Doki Literature Club!), then find the Steam config file called: config.vdf
Then you copypasta the line beginning with [i]"CS"[/i] from the linux Steam config file to the Windows Steam config file.
Location of the Steam config files:
Linux: ~/.steam/steam/config/config.vdf
Windows: "your wine prefix directory"/drive_c/Program Files/Steam/config/config.vdf

[b]0.2[/b]
Install Supreme Commander Forged Alliance using Steam
It installs it to: 
/home/test1/.local/share/lutris/runners/winesteam/prefix64/drive_c/Program Files (x86)/Steam/steamapps/common/Supreme Commander Forged Alliance/bin/SupremeCommander.exe

Game.perfs:
/home/test1/.local/share/lutris/runners/winesteam/prefix64/drive_c/users/test1/Local Settings/Application Data/Gas Powered Games/Supreme Commander Forged Alliance/Game.prefs

[b]0.3[/b]
Test the base game. At launch, Steam installs the necessary directx dlls. If you don't use Steam, then you should follow the wiki.
https://wiki.faforever.com/index.php?title=Setting_Up_FAF_Linux#Install_using_the_retail_ISO


[b][size=150]Setting up the system[/size][/b]
[b]1.0[/b]
FaF Client v0.18.0 (currently the latest)
https://github.com/FAForever/client/releases/tag/0.18.0
in ~/Games/fafclient/client-0.18.0

Uid v4.0.5 (currently the latest)
https://github.com/FAForever/uid/releases/tag/v4.0.5
in /usr/local/bin/
with sudo chmod +x /usr/local/bin/faf-uid

[b]1.1[/b]
Adding the release version file
test1@comp1:~/Games/fafclient$ echo "0.18.0" > client-0.18.0/res/RELEASE-VERSION


[b]1.2 [/b]
Installing packages from the Ubuntu repository. It's not a blind copy-paste from the wiki, I've updated this with packages that are needed to run the client v0.18.0 (thanks Wesmania)
test1@comp1:~/Games/fafclient$ sudo apt-get install python3-idna python3-semantic-version python3-pyqt5 python3-pyqt5.qtwebengine python3-pyqt5.qtmultimedia python3-jsonschema python3-jinja2 xdelta3

[code]Reading package lists... Done
Building dependency tree       
Reading state information... Done
python3-idna is already the newest version (2.6-1).
The following additional packages will be installed:
  libminizip1 libqt5designer5 libqt5help5 libqt5multimedia5
  libqt5multimediawidgets5 libqt5opengl5 libqt5quickwidgets5 libqt5sql5
  libqt5sql5-sqlite libqt5test5 libqt5webengine-data libqt5webengine5
  libqt5webenginecore5 libqt5webenginewidgets5 libqt5xml5 libre2-4
  python3-pyqt5.qtwebchannel python3-sip
Suggested packages:
  python-jinja2-doc python3-pyqt5-dbg python-semantic-version-doc
The following NEW packages will be installed:
  libminizip1 libqt5designer5 libqt5help5 libqt5multimedia5
  libqt5multimediawidgets5 libqt5opengl5 libqt5quickwidgets5 libqt5sql5
  libqt5sql5-sqlite libqt5test5 libqt5webengine-data libqt5webengine5
  libqt5webenginecore5 libqt5webenginewidgets5 libqt5xml5 libre2-4
  python3-jinja2 python3-pyqt5 python3-pyqt5.qtmultimedia
  python3-pyqt5.qtwebchannel python3-pyqt5.qtwebengine
  python3-semantic-version python3-sip
0 upgraded, 23 newly installed, 0 to remove and 4 not upgraded.
Need to get 40,3 MB of archives.
After this operation, 162 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-semantic-version all 2.3.1-1 [7.860 B]
Get:2 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libminizip1 amd64 1.1-8build1 [20,2 kB]
Get:3 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 libqt5xml5 amd64 5.9.5+dfsg-0ubuntu1 [99,6 kB]
Get:4 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5designer5 amd64 5.9.5-0ubuntu1 [2.761 kB]
Get:5 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 libqt5sql5 amd64 5.9.5+dfsg-0ubuntu1 [115 kB]
Get:6 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5help5 amd64 5.9.5-0ubuntu1 [133 kB]
Get:7 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5multimedia5 amd64 5.9.5-0ubuntu1 [293 kB]
Get:8 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 libqt5opengl5 amd64 5.9.5+dfsg-0ubuntu1 [132 kB]
Get:9 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5multimediawidgets5 amd64 5.9.5-0ubuntu1 [36,6 kB]
Get:10 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5quickwidgets5 amd64 5.9.5-0ubuntu1 [35,7 kB]
Get:11 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 libqt5sql5-sqlite amd64 5.9.5+dfsg-0ubuntu1 [40,2 kB]
Get:12 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 libqt5test5 amd64 5.9.5+dfsg-0ubuntu1 [98,1 kB]
Get:13 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5webengine-data all 5.9.5+dfsg-0ubuntu2 [5.132 kB]
Get:14 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libre2-4 amd64 20180201+dfsg-2 [185 kB]
Get:15 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5webenginecore5 amd64 5.9.5+dfsg-0ubuntu2 [28,3 MB]
Get:16 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5webengine5 amd64 5.9.5+dfsg-0ubuntu2 [165 kB]
Get:17 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 libqt5webenginewidgets5 amd64 5.9.5+dfsg-0ubuntu2 [131 kB]
Get:18 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 python3-jinja2 all 2.10-1 [95,2 kB]
Get:19 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-sip amd64 4.19.7+dfsg-1 [75,2 kB]
Get:20 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-pyqt5 amd64 5.10.1+dfsg-1ubuntu2 [2.268 kB]
Get:21 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-pyqt5.qtmultimedia amd64 5.10.1+dfsg-1ubuntu2 [141 kB]
Get:22 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-pyqt5.qtwebchannel amd64 5.10.1+dfsg-1ubuntu2 [13,9 kB]
Get:23 http://hu.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-pyqt5.qtwebengine amd64 5.10.1+dfsg-1ubuntu2 [77,6 kB]
Fetched 40,3 MB in 1s (29,3 MB/s)                     
Selecting previously unselected package python3-semantic-version.
(Reading database ... 195159 files and directories currently installed.)
Preparing to unpack .../00-python3-semantic-version_2.3.1-1_all.deb ...
Unpacking python3-semantic-version (2.3.1-1) ...
Selecting previously unselected package libminizip1:amd64.
Preparing to unpack .../01-libminizip1_1.1-8build1_amd64.deb ...
Unpacking libminizip1:amd64 (1.1-8build1) ...
Selecting previously unselected package libqt5xml5:amd64.
Preparing to unpack .../02-libqt5xml5_5.9.5+dfsg-0ubuntu1_amd64.deb ...
Unpacking libqt5xml5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Selecting previously unselected package libqt5designer5:amd64.
Preparing to unpack .../03-libqt5designer5_5.9.5-0ubuntu1_amd64.deb ...
Unpacking libqt5designer5:amd64 (5.9.5-0ubuntu1) ...
Selecting previously unselected package libqt5sql5:amd64.
Preparing to unpack .../04-libqt5sql5_5.9.5+dfsg-0ubuntu1_amd64.deb ...
Unpacking libqt5sql5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Selecting previously unselected package libqt5help5:amd64.
Preparing to unpack .../05-libqt5help5_5.9.5-0ubuntu1_amd64.deb ...
Unpacking libqt5help5:amd64 (5.9.5-0ubuntu1) ...
Selecting previously unselected package libqt5multimedia5:amd64.
Preparing to unpack .../06-libqt5multimedia5_5.9.5-0ubuntu1_amd64.deb ...
Unpacking libqt5multimedia5:amd64 (5.9.5-0ubuntu1) ...
Selecting previously unselected package libqt5opengl5:amd64.
Preparing to unpack .../07-libqt5opengl5_5.9.5+dfsg-0ubuntu1_amd64.deb ...
Unpacking libqt5opengl5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Selecting previously unselected package libqt5multimediawidgets5:amd64.
Preparing to unpack .../08-libqt5multimediawidgets5_5.9.5-0ubuntu1_amd64.deb ...
Unpacking libqt5multimediawidgets5:amd64 (5.9.5-0ubuntu1) ...
Selecting previously unselected package libqt5quickwidgets5:amd64.
Preparing to unpack .../09-libqt5quickwidgets5_5.9.5-0ubuntu1_amd64.deb ...
Unpacking libqt5quickwidgets5:amd64 (5.9.5-0ubuntu1) ...
Selecting previously unselected package libqt5sql5-sqlite:amd64.
Preparing to unpack .../10-libqt5sql5-sqlite_5.9.5+dfsg-0ubuntu1_amd64.deb ...
Unpacking libqt5sql5-sqlite:amd64 (5.9.5+dfsg-0ubuntu1) ...
Selecting previously unselected package libqt5test5:amd64.
Preparing to unpack .../11-libqt5test5_5.9.5+dfsg-0ubuntu1_amd64.deb ...
Unpacking libqt5test5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Selecting previously unselected package libqt5webengine-data.
Preparing to unpack .../12-libqt5webengine-data_5.9.5+dfsg-0ubuntu2_all.deb ...
Unpacking libqt5webengine-data (5.9.5+dfsg-0ubuntu2) ...
Selecting previously unselected package libre2-4:amd64.
Preparing to unpack .../13-libre2-4_20180201+dfsg-2_amd64.deb ...
Unpacking libre2-4:amd64 (20180201+dfsg-2) ...
Selecting previously unselected package libqt5webenginecore5:amd64.
Preparing to unpack .../14-libqt5webenginecore5_5.9.5+dfsg-0ubuntu2_amd64.deb ...
Unpacking libqt5webenginecore5:amd64 (5.9.5+dfsg-0ubuntu2) ...
Selecting previously unselected package libqt5webengine5:amd64.
Preparing to unpack .../15-libqt5webengine5_5.9.5+dfsg-0ubuntu2_amd64.deb ...
Unpacking libqt5webengine5:amd64 (5.9.5+dfsg-0ubuntu2) ...
Selecting previously unselected package libqt5webenginewidgets5:amd64.
Preparing to unpack .../16-libqt5webenginewidgets5_5.9.5+dfsg-0ubuntu2_amd64.deb ...
Unpacking libqt5webenginewidgets5:amd64 (5.9.5+dfsg-0ubuntu2) ...
Selecting previously unselected package python3-jinja2.
Preparing to unpack .../17-python3-jinja2_2.10-1_all.deb ...
Unpacking python3-jinja2 (2.10-1) ...
Selecting previously unselected package python3-sip.
Preparing to unpack .../18-python3-sip_4.19.7+dfsg-1_amd64.deb ...
Unpacking python3-sip (4.19.7+dfsg-1) ...
Selecting previously unselected package python3-pyqt5.
Preparing to unpack .../19-python3-pyqt5_5.10.1+dfsg-1ubuntu2_amd64.deb ...
Unpacking python3-pyqt5 (5.10.1+dfsg-1ubuntu2) ...
Selecting previously unselected package python3-pyqt5.qtmultimedia.
Preparing to unpack .../20-python3-pyqt5.qtmultimedia_5.10.1+dfsg-1ubuntu2_amd64.deb ...
Unpacking python3-pyqt5.qtmultimedia (5.10.1+dfsg-1ubuntu2) ...
Selecting previously unselected package python3-pyqt5.qtwebchannel.
Preparing to unpack .../21-python3-pyqt5.qtwebchannel_5.10.1+dfsg-1ubuntu2_amd64.deb ...
Unpacking python3-pyqt5.qtwebchannel (5.10.1+dfsg-1ubuntu2) ...
Selecting previously unselected package python3-pyqt5.qtwebengine.
Preparing to unpack .../22-python3-pyqt5.qtwebengine_5.10.1+dfsg-1ubuntu2_amd64.deb ...
Unpacking python3-pyqt5.qtwebengine (5.10.1+dfsg-1ubuntu2) ...
Setting up libminizip1:amd64 (1.1-8build1) ...
Setting up python3-semantic-version (2.3.1-1) ...
Setting up libqt5quickwidgets5:amd64 (5.9.5-0ubuntu1) ...
Setting up libqt5webengine-data (5.9.5+dfsg-0ubuntu2) ...
Setting up libqt5test5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Setting up libqt5opengl5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Setting up libqt5multimedia5:amd64 (5.9.5-0ubuntu1) ...
Setting up libre2-4:amd64 (20180201+dfsg-2) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Setting up libqt5xml5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Setting up python3-jinja2 (2.10-1) ...
Setting up libqt5sql5:amd64 (5.9.5+dfsg-0ubuntu1) ...
Setting up python3-sip (4.19.7+dfsg-1) ...
Setting up libqt5webenginecore5:amd64 (5.9.5+dfsg-0ubuntu2) ...
Setting up libqt5designer5:amd64 (5.9.5-0ubuntu1) ...
Setting up libqt5multimediawidgets5:amd64 (5.9.5-0ubuntu1) ...
Setting up libqt5webenginewidgets5:amd64 (5.9.5+dfsg-0ubuntu2) ...
Setting up libqt5webengine5:amd64 (5.9.5+dfsg-0ubuntu2) ...
Setting up libqt5help5:amd64 (5.9.5-0ubuntu1) ...
Setting up libqt5sql5-sqlite:amd64 (5.9.5+dfsg-0ubuntu1) ...
Setting up python3-pyqt5 (5.10.1+dfsg-1ubuntu2) ...
Setting up python3-pyqt5.qtwebchannel (5.10.1+dfsg-1ubuntu2) ...
Setting up python3-pyqt5.qtmultimedia (5.10.1+dfsg-1ubuntu2) ...
Setting up python3-pyqt5.qtwebengine (5.10.1+dfsg-1ubuntu2) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
(first, i forgot to list python3-jsonschema when i installed these... X))
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  python3-jsonschema
0 upgraded, 1 newly installed, 0 to remove and 4 not upgraded.
Need to get 31,2 kB of archives.
After this operation, 175 kB of additional disk space will be used.
Get:1 http://hu.archive.ubuntu.com/ubuntu bionic/main amd64 python3-jsonschema all 2.6.0-2 [31,2 kB]
Fetched 31,2 kB in 0s (162 kB/s)              
Selecting previously unselected package python3-jsonschema.
(Reading database ... 195460 files and directories currently installed.)
Preparing to unpack .../python3-jsonschema_2.6.0-2_all.deb ...
Unpacking python3-jsonschema (2.6.0-2) ...
Setting up python3-jsonschema (2.6.0-2) ...
update-alternatives: using /usr/bin/python3-jsonschema to provide /usr/bin/jsonschema (jsonschema) in auto mode[/code]

[b]1.3[/b]
Run the client. It works for me at this point.
test1@comp1:~/Games/fafclient$ python3 client-0.18.0/src/__main__.py
[code]Gtk-Message: 20:39:46.489: Failed to load module "canberra-gtk-module"
[27892:27922:0707/203948.898161:ERROR:nss_ocsp.cc(591)] No URLRequestContext for NSS HTTP handler. host: s2.symcb.com
[27892:27922:0707/203948.898185:ERROR:nss_ocsp.cc(591)] No URLRequestContext for NSS HTTP handler. host: s2.symcb.com
[27892:27922:0707/203948.898202:ERROR:nss_ocsp.cc(591)] No URLRequestContext for NSS HTTP handler. host: s1.symcb.com
[27892:27922:0707/203948.899179:ERROR:nss_ocsp.cc(591)] No URLRequestContext for NSS HTTP handler. host: s2.symcb.com
[27892:27922:0707/203948.899196:ERROR:nss_ocsp.cc(591)] No URLRequestContext for NSS HTTP handler. host: s2.symcb.com
[27892:27922:0707/203948.899217:ERROR:nss_ocsp.cc(591)] No URLRequestContext for NSS HTTP handler. host: s1.symcb.com[/code]



[b][size=150]Setting up the FaF Client[/size][/b]
[b]2.0[/b]
Setting up the client
Options -> Settings -> Game Path, for me it's:
/home/test1/.local/share/lutris/runners/winesteam/prefix64/drive_c/Program Files (x86)/Steam/steamapps/common/Supreme Commander Forged Alliance

[b]2.1[/b]
Modifying FA Lobby.ini to use the correct Wine version etc
/home/test1/.config/ForgedAllianceForever/FA Lobby.ini
Added:
[i][wine]
exe=/home/test1/.local/share/lutris/runners/wine/3.10-x86_64/bin/wine
prefix=/home/test1/.local/share/lutris/runners/winesteam/prefix64[/i]



[size=150][b]Launch games from the client[/b][/size]
At this point it will work.



[size=150][b]Issues with the game, mods, maps[/b][/size]
- If you experience mouse cursor flickering, disable vsync in the game settings/video
- If the downloaded mods or maps don't show up in the lobby or you're automatically kicked out from lobbies that use mods:
you need to create links for the game to be able to find downloaded mods and maps.
details are here: http://forums.faforever.com/viewtopic.php?f=2&t=4507&start=560#p168893
- If you have no sound when the game window is not active (not focused, minimized), then enable "Emulate a virtual desktop" option with winecfg, its under the Graphics tab. The resolution is your native resolution (you have to set this too).


[i]edited
- typos
- solution for cursor flickering
- xdelta3 install, see more here: https://forums.faforever.com/viewtopic.php?f=2&t=4507&start=550#p168646
- the game cannot use downloaded mods and maps
- explanation how to fix the Windows Steam error when it fails downloading the game
- fixed issue, no audio when the game window is not active
[/i]
