OSX Ports
---------

How to use
----------

    cd ${HOME}
    git clone git@github.com:TrickPlay/osx-ports.git .ports
    cd .ports
    portindex

This will set up MacPorts to know about newer versions of various packages that will give you a better TrickPlay experience.  It'll also create a placeholder package for TrickPlay's dependencies so all the right versions of all the packages can be installed with one easy command:

    sudo port install trickplay-deps

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
