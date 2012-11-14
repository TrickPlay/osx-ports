OSX Ports
---------

Pre-requisites
--------------

First, install XCode.  You can get it through the App Store (on the apple menu).
Once XCode is installed, you need to install the XCode command line tools.  To do this, launch XCode, then go to Preferences.  Click the "Downloads" tab, and install command line tools.
Next, install [MacPorts][mp].  Use the PKG version of the MacPorts install.

[mp]: http://www.macports.org/install.php


How to use
----------

Once the prereqs are all installed, you need to fetch our special ports and then install.

    cd ${HOME}
    git clone git@github.com:TrickPlay/osx-ports.git .ports
    cd .ports
    portindex

This will set up MacPorts to know about newer versions of various packages that will give you a better TrickPlay experience.  It'll also create a placeholder package for TrickPlay's dependencies so all the right versions of all the packages can be installed with one easy command:

    sudo port self-update
    sudo port install trickplay-deps +quartz -x11 +no_x11 +no_gnome +ares +ssl

After you've done that, you should then be able to build the trickplay engine from source.  Some day we'll have release versions of the engine installable directly from MacPorts.

    cd "${HOME}/somepath"
    git clone git@git.trickplay.com:tp-master.git trickplay
    cd trickplay
    mkdir build
    CC=clang CXX=clang++ cmake -G Ninja -DTP_WITH_WEBGL=1 -DTP_PROFILING=1 -DCMAKE_BUILD_TYPE=RelMinSize -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -H. -Bbuild
    ninja -C build

What I typically do is create a symlink that'll behave nice.

    mkdir "${HOME}/bin"
    cd "${HOME}/bin"
    ln -s "${HOME}/somepath/trickplay/build/clients/clutter-mediaplayer/trickplay" .

And then, make sure that `${HOME}/bin` is in your `$PATH`
