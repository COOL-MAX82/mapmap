Build instructions
==================

Build on GNU/Linux
------------------

Install the dependencies.

Build it:

```
qmake mapmap.pro
make
```

Alternatively:

```
./scripts/build.sh
```

### Ubuntu

NOTE: Tested on 13.10, 14.04, 15.04 and 16.04

Install basic development tools fot Qt projects, plus liblo for OSC support:

```
sudo apt-get install -y \
      liblo-dev liblo-tools \
      qttools5-dev-tools \
      qtmultimedia5-dev \
      libqt5opengl5-dev \ 
      qtwebengine5-dev \
      libqt5multimedia5-plugins \
      qt5-default
```

Install GStreamer 1.0 libraries and plugins:

```
sudo apt-get install -y \
      libgstreamer1.0-dev \
      libgstreamer-plugins-base1.0-dev \
      gstreamer1.0-plugins-bad \
      gstreamer1.0-libav \
      gstreamer1.0-vaapi \
      gstreamer1.0-plugins-base \
      gstreamer1.0-plugins-base-apps \
      gstreamer1.0-plugins-good \
      gstreamer1.0-plugins-ugly \
      gstreamer1.0-x \
      gstreamer1.0-tools
```

Install extra packages if you want to build the documentation:

```
sudo apt-get install -y \
      doxygen \
      graphviz \
      rst2pdf \
      markdown
```

### Arch Linux

Install basic development tools fot Qt projects, GStreamer 1.0 and liblo for OSC support:

```
sudo pacman -S qt5-tools qt5-multimedia qt5-webengine liblo gstreamer
```

Install GStreamer 1.0 libraries and plugins::

```
sudo pacman -S gst-libav \
               gstreamer-vaapi \
               gst-plugins-bad \
               gst-plugins-base \
               gst-plugins-base-libs \
               gst-plugins-good \
               gst-plugins-ugly
```

Build on Mac OS X
-----------------

NOTE: This has been tested on OS X 10.11 (El Capitan).

Install tools and dependencies:

1) Install the Apple Developer Tools
  - You need to register with a credit card in the Apple Store in order to download it (no need to pay, but Apple requires your credit card number).
2) Install Qt5
  - You can get the open source version from http://www.qt.io/download-open-source/
  - Run the installer and choose the default location (which should be ~/Qt).
  - Latest tested version: 5.5.1=
3) Install liblo
  - Use the following guide: http://macappstore.org/liblo/
  - OR compile from the tar.gz - it should install it to /usr/local
4) Install the GStreamer framework. You need the runtime and devel packages to be installed:
  - https://gstreamer.freedesktop.org/data/pkg/osx/1.6.0/gstreamer-1.0-1.6.0-x86_64.pkg
  - https://gstreamer.freedesktop.org/data/pkg/osx/1.6.0/gstreamer-1.0-devel-1.6.0-x86_64.pkg
  - http://gstreamer.freedesktop.org/data/pkg/osx/1.6.0/gstreamer-1.0-1.6.0-x86_64-packages.dmg

Do this:

```
./scripts/build.sh
```

It will create a .app and a .dmg.

DMGVERSION.txt should be created automatically with "1" as its contents. Update to "2", and so on, if needed.

### Troubleshooting

#### GStreamer header not found

If you have a compilation error saying that file ```<gst/gst.h>``` cannot be found: make sure your GStreamer.framework folder is installed and is _not_ read-protected.

#### Corrupted OSC port

If the appearance of the window of the OSC port number in the preferences seem corrupted, you might want to reset MapMap's preferences:

```
rm -f ~/Library/Preferences/info.mapmap.MapMap.plist
```

To print debugging informations, launch it from the Terminal app like this::

```
GSTPLUGIN_PATH=/Library/Frameworks/GStreamer.framework/Libraries GST_DEBUG=2 /Applications/MapMap.app/Contents/MacOS/MapMap
```

Build on Windows
----------------

Download gstreamer-x86 runtime& devel 
 - https://gstreamer.freedesktop.org/data/pkg/windows/1.10.2/gstreamer-1.0-x86-1.10.2.msi
 - https://gstreamer.freedesktop.org/data/pkg/windows/1.10.2/gstreamer-1.0-devel-x86-1.10.2.msi

Then:
- Choose complete option during installation process wizard
- Build Mapmap with Qt Creator (qmake, build release)
- Add the bin directory of your Qt installation (e.g. e.g. C:\Qt\Qt5.6.0\5.6\mingw49_32\bin) to the PATH variable
- Open Windows console then run the following command: ```windeployqt --release --no-system-d3d-compiler <path-to-app-binary>```

Copy the followings DLL into the target folder together with Mapmap.exe:
```
libffi-6.dll libgobject-2.0-0.dll libgstbase-1.0-0.dll libgsttag-1.0-0.dll liborc-0.4-0.dll 
libglib-2.0-0.dll libgstapp-1.0-0.dll libgstpbutils-1.0-0.dll libgstvideo-1.0-0.dll libz.dll 
libgmodule-2.0-0.dll libgstaudio-1.0-0.dll libgstreamer-1.0-0.dll libintl-8.dll
```

Copy all DLL files of the Gstreamer's bin folder (e.g. C:\gstreamer\1.0\x86\bin) into a new folder named 'lib' in the target folder together with mapmap.exe

Copy all DLL files of the Gstreamer's plugin folder (e.g. C:\gstreamer\1.0\x86\lib\gstreamer-1.0) into a new folder named 'plugins' in parallel of lib folder

Remove lib\libopenh264.dll, lib\libSoundTouch-0.dll, lib\libtag.dll

Run Mapamp.exe

Editing translations
--------------------
You might need to update the files:
  
```
cd src/mapmap
lupdate mapmap.pro 
```

Then, do this:

```  
lrelease mapmap.pro
```
