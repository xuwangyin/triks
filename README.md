triks
=====
## System Management
[dotfiles](http://dotfiles.github.com/)
## zsh
### tips, tricks and examples for the zsh
    aptitude search zsh
    sudo aptitude install zsh-lovers
    man zsh-lovers
    
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