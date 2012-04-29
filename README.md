triks
=====
## System Management
[dotfiles](http://dotfiles.github.com/)
## zsh
### resources
[holman's zsh](https://github.com/holman/dotfiles)
### tips, tricks and examples for the zsh
    aptitude search zsh
    sudo aptitude install zsh-lovers
    man zsh-lovers
## emacs
### dired search and replace
mark files:
    
    dired-mark-files-regexp(%m)
query replace:

    dired-do-query-replace-regexp(Q)
search:

    dired-do-search
## Ubuntu Server
### ftp server
[ftp server setup guide](https://help.ubuntu.com/10.04/serverguide/ftp-server.html), note the default ftp directory is /srv/ftp.
## New System Setup
### Case-Insensitive Tabbing in Ubuntu Terminal(Bash)
    sudo cp -p /etc/inputrc /etc/inputrc.bak
    sudo su
    echo "set completion-ignore-case on">>  /etc/inputrc
    exit
    
### configure vpn
    Right click on network manager, select "edit connections..."
    Navigate to "VPN" tab, click on "Add", click "Create..." in the new window.
    Fill in the Gateway(ip address of ssh server), username and password, click on "Advanced...".
    Unselect "EAP"，select "Use point-to-point encryption(MPPE)"

### ustb ubuntu source list
    deb ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty main multiverse restricted universe
    deb ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-backports main multiverse restricted universe
    deb ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-proposed main multiverse restricted universe
    deb ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-security main multiverse restricted universe
    deb ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-updates main multiverse restricted universe
    deb-src ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty main multiverse restricted universe
    deb-src ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-backports main multiverse restricted universe
    deb-src ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-proposed main multiverse restricted universe
    deb-src ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-security main multiverse restricted universe
    deb-src ftp://ftp.ustb.edu.cn/pub/ubuntu/ natty-updates main multiverse restricted universe

## Linux Tricks
### Copy To Clipboard
    $ sudo apt-get install xclip
    $ xclip -sel clip < ~/.ssh/id_rsa.pub
### print the strings of printable characters in files(i.e. MS Word)
    strings /usr/lib/libstdc++.so.6 | grep GLIBC

## writing matlab interface for c/c++ programs
[MEX-files Guide](http://www.mathworks.cn/support/tech-notes/1600/1605.html#example1)
### Windows
#### compile and install opencv from source if you have made change to the source, otherwise just install opencv binaries.
[OpenCV Installation Guide](http://opencv.willowgarage.com/wiki/InstallGuide)
#### build our project into a shared library
### program
    #include <vector>
    #include <stack>
    #include "cv.h"
    #include <opencv2/core/core.hpp>
    #include <opencv2/imgproc/imgproc.hpp>
    #include <opencv2/highgui/highgui.hpp>
    #include "mex.h"
    
    using namespace std;
    using namespace cv;
    
    void mexFunction(int nlhs, mxArray *plhs[],
        int nrhs, const mxArray *prhs[]) {
        
      mexPrintf("Hello, world!\n");
    
      Mat origin = imread("demo.jpg");
      imshow("origin", origin);
      waitKey(
    } 
### makefile
    all:
        mex `pkg-config --cflags opencv` testcv.cpp `pkg-config --libs opencv`
### compile
    make
### problem
in the matlab command window (path of testcv should be in the matlab's search path):

    >> testcv

yields: 

    ??? Invalid MEX-file '/home/xuwangyin/matlab/testcv.mexglx': /usr/local/matlabR2010a/bin/glnx86/../../sys/os/glnx86/libstdc++.so.6: version
    `GLIBCXX_3.4.11' not found (required by /usr/local/lib/libopencv_core.so.2.3).

### solution
    $ locate libstdc++
    
yields

       /usr/lib/gcc/i486-linux-gnu/4.2/libstdc++.a
       /usr/lib/gcc/i486-linux-gnu/4.2/libstdc++.so
       /usr/lib/gcc/i686-linux-gnu/4.6/libstdc++.a
       /usr/lib/gcc/i686-linux-gnu/4.6/libstdc++.so
       /usr/lib/i386-linux-gnu/libstdc++.so.6
       /usr/lib/i386-linux-gnu/libstdc++.so.6.0.16
       /usr/lib/ure/lib/libstdc++.so.6
       /usr/local/matlabR2010a/sys/os/glnx86/README.libstdc++
       /usr/local/matlabR2010a/sys/os/glnx86/libstdc++.so.6
       /usr/local/matlabR2010a/sys/os/glnx86/libstdc++.so.6.0.9
       ...
       
if you can't find it, you can just copy one from other machines.  

make sure the new target contains GLIBCXX_3.4.11

    strings /usr/lib/i386-linux-gnu/libstdc++.so.6.0.16| grep GLIBCXX
    
go to the directory contains libstdc++.so.6

    cd $MATLAB/ys/os/glnx86
    
backup the old link

    sudo cp libstdc++.so.6 libstdc++.so.6.disabled
    
make the new link

    sudo ln -sf /usr/lib/i386-linux-gnu/libstdc++.so.6.0.16 libstdc++.so.6