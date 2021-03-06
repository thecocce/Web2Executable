Web2Executable
==============

Uses node-webkit to generate "native" apps for already existing web apps.

Requires the pyside library and python 2.X to run. If you want to replace the icon in the Windows Exe's, this will do it automatically with the latest code if you have PIL or Pillow installed. I've only tested the code on python 2.7.3-2.7.5, so I can't speak about any lower version, but it should work as long as PySide is supported.

If you have an idea for a feature, please list it [here](https://github.com/jyapayne/Web2Executable/wiki/Feature-Requests).

If you got some value out of using my app, consider donating a dollar to keep me caffeinated :) 

<a href='https://pledgie.com/campaigns/26899'><img alt='Click here to lend your support to: Web2Executable Donations and make a donation at pledgie.com !' src='https://pledgie.com/campaigns/26899.png?skin_name=chrome' border='0' ></a>


Downloads
---------

###CMD

[Windows 7+ Download](http://www.mediafire.com/download/r9rawa9qorlfa79/Web2ExeWin-CMD.zip)

[Mac OS X 10.6+ download](http://www.mediafire.com/download/esyz3z3ij0qrt64/Web2ExeMac-CMD.zip)

[Ubuntu 14.04 download](http://www.mediafire.com/download/vet95whim6g8x55/Web2ExeLinux-CMD.zip)

###GUI

####Mac OS X

[Mac OS X 10.7+ download - v0.1.16b](http://www.mediafire.com/download/92yx388kld2d3vc/Web2ExeMac-v0.1.16b.zip)

You can just put the app where ever you want and double click to run it.

####Windows

[Windows 7+ download - v0.1.16b](http://www.mediafire.com/download/1rzq4h6ncstdws8/Web2ExeWin-v0.1.16b.zip)

Double click the Web2Exe.exe file inside the extracted folder.

####Linux

[Ubuntu 14.04 - v0.1.16b](http://www.mediafire.com/download/8cvyl0d4avtwv49/Web2ExeLinux-v0.1.16b.zip)

Give the executable permissions to execute and then run it:

```
chmod +x web2exe
./web2exe
```

It's probably better for linux users to install the requirements and run the python script as instructed below.


Getting Started
---------------

###GUI 

Install dependencies **PIL or Pillow** for icon and icns exporting.

Initiate submodules:

```
git submodule update --init --recursive
```

Run with:

```
python main.py
```

It's a pretty simple app. Just point it the the directory that your web application lives, customize the options (the two marked with a star are the only ones required) and then choose your export options. The app will export under YOUR_OUTPUT_DIR/YOUR_APP_NAME. 

###Command line interface

Dependencies: configobj (install with pip) and Pillow if you want icon replacement (not necessary)

Run the command_line.py with the --help option to see a list of export options. Optionally, if you don't want to install python, there are builds for Mac and Windows in the command_line_builds folder of this repository.

Example usage (if using the prebuilt binary, replace `python command_line.py` with the exe name):

```
python command_line.py /var/www/html/CargoBlaster/ --main html/index.html --export-to linux-x64 windows mac --width 900 --height 700 --nw-version 0.10.5
```

Features
--------

- Cross platform to Mac, Windows, Linux
- Working media out of the box (sound and video)
- Easy to use and straightforward
- Streamlined workflow from project -> working standalone exe
- Same performance as Google Chrome
- Works with Phaser; should work with other HTML5 game libraries
- Export web applications to all platforms from your current OS
- Ability to specify a node-webkit version to download
- Automatic insertion of icon files into Windows exe's or Mac Apps by filling out the icon fields as necessary
- A command line utility with functionality equivalent to the GUI. Useful for automated builds.

Planned Features
----------------

- Compression options using UPX to minimize the exe size
- Minification of javascript, html, css before zipping


FAQ
---

### How do I include external files?

You must provide support for this yourself using javascript and nodejs. You can get the path of the current executable with `path.dirname( process.execPath );` and then load files relative to that path. 

### When exporting to Linux, I get an error about libudev.so.0

This is an known issue with nw.js/node-webkit. See [here](https://github.com/nwjs/nw.js/wiki/The-solution-of-lacking-libudev.so.0) for information on how to work around this issue.

### How do I use option X?

All of the options for node-webkit are documented in node-webkit's manifest file specification. It is located [here](https://github.com/rogerwang/node-webkit/wiki/Manifest-format).

### What is the downloads folder for and where should I keep it?

The downloads folder is where Web2Exe stores the node-webkit versions in zip or tar format. This location should be chosen as a central location, because Web2Exe will reuse the files to create executables every time the export button is pressed. It will also save time by not having to redownload the node-webkit files over and over.

The Web2Executable/files/downloads folder is a good place to keep your downloads or any place that **isn't your project's directory**.

### Where is the default downloads location and how can I change it back?

For right now, the default location is in Web2Executable/files/downloads (Web2Executable.app/Contents/MacOS/files/downloads for Mac OSX).

This location is stored on a by project basis, so it will load what you have set for a particular project from the package.json file. Right now, the only way to change it back to the default is to open the package.json file with a text editor and remove the download_dir option from it.

### How do I use the icon replacement?

The icon replacement works by filling out the fields "Window Icon", "Exe Icon", or "Mac Icon". If "Window Icon" is filled out and the others aren't, Web2Exe will automatically use this field instead of "Exe Icon" or "Mac Icon" depending on if you export to Mac or Windows.

If you fill "Exe Icon" out, this will be used to replace the icon inside the node-webkit exe from the default compass icon if you export to Windows. Only pngs and jpegs are supported right now.

If you fill out "Mac Icon", this will convert the icon from png or jpeg to icns and copy it into the Mac app folder (or just copy if the icon is already in icns format). Of course, this is only when exporting to Mac.

### Why don't you replace icons for Linux?

Linux executables don't use icons, so there's nothing to replace. If you want to set an icon for when the app is running for Linux, simply fill out the "Window Icon" field.

What's New?
----------------------

v0.1.16b
- Fixed an issue with copying files on windows

v0.1.15b
- Fixed some issues with copying external files

v0.1.12b
- Added new options that were requested and made the window wider to accommodate.

v0.1.11b
- fixed a bug that overwrote the index.html path if it was not in the root directory

v0.1.10b
- added the ability to specify an icon for both mac and windows export applications

v0.1.9b
- made UI more compact for small screens
- fixed Mac issue with not loading! Yay!

v0.1.8b
- added an "Open to export folder" button that makes things a little easier to navigate to.
- attempted to fix Mac OS X issues with crashing

v0.1.7b
- added better download management so there is no redownloading things. Also a bunch of bugs were fixed up.

v0.1.6b

- added the ability to get newer NodeWebkit versions automatically from the changelog of node-webkit. Also fixed compatibility with 0.10.X.

v0.1.4b

- fixed an issue where index.html would be found with absolute path, which would cause a "require not found" error

v0.1.3b

- Added the ability to choose node-webkit versions if 0.9.2 is not what you want*
- Modified the UI slightly for people with smaller monitors
- Added a force-download option to overwrite files

*Note: If you have already downloaded, say, 0.9.2 of webkit, then you select 0.8.5, you will have to select "Force download" in order to update the files properly. I'm not sure how to reliably/efficiently detect and store multiple versions of the node-webkit files.

v0.1.2b

- Fixed an issue with icon copying
- Fixed a bug that overwrote existing package.json files.



Screenshots
-----------

v0.1.13b Mac OS X

![ScreenshotMac2](http://i.imgur.com/JgKfYIm.png)

v0.1.9b Mac OS X

![ScreenshotMac](http://i.imgur.com/Kdd6DcC.png)


License
-------

The MIT License (MIT)

Copyright (c) 2015 SimplyPixelated

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
