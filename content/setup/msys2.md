## -*- coding: utf-8 -*-
.. title: msys2

[openFrameworks](http://openframeworks.cc/) | [Documentation table of contents](table_of_contents.md)

msys2
=====

Installing msys2 
----------------

First, install MSYS2 using the [one-click installer](https://msys2.github.io/) or 
directly unzipping the archive from their [repository](http://sourceforge.net/projects/msys2/files/Base/x86_64/)

If you are going to use QtCreator you should install msys2 in the default install folder, c:\msys64

Open a MSYS2 shell and update the system packages :

    pacman --noconfirm  --needed -Sy bash pacman pacman-mirrors msys2-runtime
	
Close the shell and open a new one to update the remaining packages :

    pacman --noconfirm -Su

You are now ready to install openFrameworks.	


Installing openFrameworks
-------------------------

Download and unzip the win_cb version of oF.

Open an MSYS shell and install OF dependencies:

    cd your_oF_directory/scripts/win_cb/msys2
    ./install_dependencies.sh`
	
Open an **MINGW32** shell and compile oF libraries:

	cd your_oF_directory/libs/openFrameworksCompiled/project
    make

You can speed-up compilation using parallel build `make -j4` or the number of cores you want it to use


Setting the PATH variable
-------------------------
On MSYS2, openFrameworks needs the dlls that are provided by MSYS2 package manager `pacman`. The PATH variable tells the system where to look for these dlls. On Windows, the system starts to look into the executable folder, then into the folders defined in system PATH and finally into the folders defined in user PATH.

You can find how to set the PATH in windows here: http://www.computerhope.com/issues/ch000549.htm

You'll need to add your_msys2_directory\mingw32\bin;your_msys2_directory\usr\bin to your PATH, which usually is:

        c:\msys64\mingw32\bin;c:\msys64\usr\bin
        
You can also set the PATH from the command line: open a Windows cmd prompt and set you user PATH

        setx PATH "%PATH%;your_msys2_directory\mingw32\bin;your_msys2_directory\usr\bin;"

If you have administrative privileges, you can directly set the system PATH. All users will benefit of it...

That's all, now go to the your_oF_directory/examples folder, where you will find 
the examples, and have fun! 

Running examples
----------------
Compile the example (for example the 3DPrimitivesExample)

    cd your_oF_directory/examples/3d/3DPrimitivesExample
    make

At this point, `make run` or  double-click on the exe file to launch. 


Makefile
--------

Every example has a Makefile you can configure using the files config.make
and addons.make.

config.make: This file has options to add search paths, libraries, etc., the 
syntax is the usual syntax in makefiles, there's help comments inside the file.

addons.make: if you want to use an addon which is inside the addons folder, just 
add its name in a new line in this file.

QtCreator
---------

With msys2 you can also use QtCreator as an IDE, you can find more information in the corresponding [setup guide](../qtcreator):

FAQ / Common problems
--------------------- 
- "I have a TLSv1_1_client_method missing error" when I double-click the exe ?"

The executable looks for ssleay32.dll and libeay32.dll and it first finds a version that doesn't support TLS v1.1. Often it happens with Intel iCls software. The solution is to move the your_msys2_directory\mingw32\bin path before the conflicting path. If the conflicting path is in the system PATH and you do not have administrative privileges, copy/link ssleay32.dll and libeay32.dll from your_msys2_directory\mingw32\bin to the executable folder.

- "I'm on a corporate network with a proxy. I cannot download packages with pacman."

You may need to set HTTP_PROXY and HTTPS_PROXY environment variables.

    From a DOS/CMD prompt :    
    set http_proxy=http://your_proxy:your_port
    set http_proxy=http://username:password@your_proxy:your_port
    set https_proxy=https://your_proxy:your_port
    set https_proxy=https://username:password@your_proxy:your_port
Don't forget to escape special characters in your password...



 

many thanks!! OFteam

