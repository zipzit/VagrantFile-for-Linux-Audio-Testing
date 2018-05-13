# -*- mode: ruby -*-
# vi: set ft=ruby :

# Reminder: $ vagrant up
#           $ vagrant destroy

Vagrant.configure("2") do |config|
  # config.vm.box = "kurron/xenial-xubuntu"
  # config.vm.box = 'ubuntu/xenial64'
  config.vm.box = "bstoots/xubuntu-16.04-desktop-amd64"
  # requires https://github.com/sprotheroe/vagrant-disksize plugin installed on the host
  # config.disksize.size = '30GB'

config.vm.provider "virtualbox" do |vb|
  vb.gui = true    ## Display the VirtualBox GUI when booting the machine
  # vb.memory = "4096"
  vb.name = "bstoots-Xub-Dev"
  vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']

  ## from https://github.com/kurron/packer-xubuntu-xenial/blob/master/vagrantfile
  ## See https://www.virtualbox.org/manual/ch08.html for option descriptions
  vb.customize ["modifyvm", :id, "--rtcuseutc", "on"]      ## This option lets the real-time clock (RTC) operate in UTC time.
  vb.customize ["modifyvm", :id, "--hwvirtex", "on"]       ## This enables or disables the use of hardware virtualization extensions (Intel VT-x or AMD-V) in the processor of your host system;
  vb.customize ["modifyvm", :id, "--nestedpaging", "on"]   ## If hardware virtualization is enabled, this additional setting enables or disables the use of the nested paging feature in the processor of your host system;
  vb.customize ["modifyvm", :id, "--vtxvpid", "on"]        ## If hardware virtualization is enabled, for Intel VT-x only, this additional setting enables or disables the use of the tagged TLB (VPID) feature
  vb.customize ["modifyvm", :id, "--largepages", "on"]     ## If hardware virtualization and nested paging are enabled, for Intel VT-x only, an additional performance improvement of up to 5% can be obtained by enabling this setting
  vb.customize ["modifyvm", :id, "--ioapic", "on"]         ## Enabling the I/O APIC is required for 64-bit guest operating systems, reqd if you want to use more than one virtual CPU in a VM.
  vb.customize ["modifyvm", :id, "--acpi", "on"]           ## Should the VM should have ACPI support?
  vb.customize ["modifyvm", :id, "--nictype1", "virtio"]   ## change the network card hardware for better performance
  # vb.customize ["modifyvm", :id, "--groups", "/Special Testing"]    ## Yawn.  Displays details of the VM Groups.  Displays the VB in a different "location" in the VirtualBox GUI display.
  vb.customize ["modifyvm", :id, "--memory", "4096"]       ## This sets the amount of RAM, in MB, that the virtual machine should allocate for itself from the host.
  vb.customize ["modifyvm", :id, "--vram", "128"]          ## This sets the amount of RAM that the virtual graphics card should have.
  vb.customize ["modifyvm", :id, "--cpus", "2"]            ## This sets the number of virtual CPUs for the virtual machine
  vb.customize ["modifyvm", :id, "--audio", "coreaudio"]        ## choices are none|null|dsound|oss|alsa|pulse|oss|pulse|coreaudio]
  vb.customize ["modifyvm", :id, "--audiocontroller", "ac97"]    ## Choices are: ac97|hda|sb16
  vb.customize ["modifyvm", :id, "--audioout", "on"]       ##
  # vb.customize ["controlvm", :id, "--audioout", "on"]       ##
  vb.customize ["modifyvm", :id, "--audioin", "on"]        ##
  ## do we also need     [--audiocodec stac9700|ad1980|stac9221|sb16]  ??
  vb.customize ["modifyvm", :id, "--accelerate3d", "on"]    ## Enable 3D Display Acceleration

end

config.vm.provision "shell", inline: <<-SHELL

  # Update/upgrade/autoremove can cause troubles, primarily with unexpected interacive terminal responses..
  # Better to run them manually after VirtualBox is running...
  #
  # echo -----------------------------------
  # echo UPDATE GRUB
  # echo -----------------------------------
  # # # https://github.com/hashicorp/vagrant/issues/289
  # apt-get -y remove grub-pc
  # apt-get -y install grub-pc
  # grub-install /dev/sda # precaution
  # update-grub
  #
  # echo -----------------------------------
  # echo UPDATE
  # echo -----------------------------------
  # sudo apt-get -y update
  #
  # echo -----------------------------------
  # echo UPGRADE
  # echo -----------------------------------
  #
  # # now start bootstrapping and upgrading your system packages
  # sudo apt-get -y upgrade
  #
  # echo -----------------------------------
  # echo AUTOREMOVE
  # echo -----------------------------------
  # sudo apt-get -y autoremove
  #
  # # Usually if there are kernel updates, you’ll want to reboot the server. So, do that.
  # #
  # # sudo shutdown -r now

  echo -----------------------------------
  echo INSTALL APTITUDE, A DEBIAN PACKAGE MANAGER
  echo -----------------------------------
  sudo apt-get install -y aptitude        # Aptitude = a debian package manager

  # echo -----------------------------------
  # echo INSTALL XUBUNTU DESKTOP
  # echo -----------------------------------
  # sudo aptitude install -y xubuntu-desktop     # Only required if the base image doesn't already include it.

  echo -----------------------------------
  echo INSTALL BUILD ESSENTIALS
  echo -----------------------------------
  sudo apt-get install -y build-essential   # Debian package development tools, g++, gcc, libc6-dev, make
  sudo apt-get install -y nano
  # # sudo apt-get install -y g++ cmake libglu-dev libxi-dev
  #
  #
  # # cd /opt
  # # sudo wget -c http://download.virtualbox.org/virtualbox/5.2.8/VBoxGuestAdditions_5.2.8.iso \
  # #                    -O VBoxGuestAdditions_5.2.8.iso
  # # sudo mount VBoxGuestAdditions_5.2.8.iso -o loop /mnt
  # # cd /mnt
  # # sudo sh VBoxLinuxAdditions.run --nox11
  # # cd /opt
  # # sudo rm *.iso
  # # sudo /etc/init.d/vboxadd setup
  # # sudo chkconfig --add vboxadd
  # # sudo chkconfig vboxadd on

  # echo -----------------------------------
  # echo INSTALL GUEST ADDITIONS
  # echo -----------------------------------
  # # sudo apt-get install -y virtualbox-guest-dkms
  # # Guest additions, per https://askubuntu.com/questions/22743/how-do-i-install-guest-additions-in-a-virtualbox-vm
  # # sudo apt-get install -y virtualbox-guest-additions-iso
  # # sudo apt-get update
  # # sudo apt-get dist-upgrade
  # # sudo apt-get install -y virtualbox-guest-x11
  #
  # # https://askubuntu.com/questions/992395/16-04-guest-on-16-04-host-vboxclient-failed-to-connect-to-the-virtualbox-ker
  # # https://www.vagrantup.com/docs/virtualbox/boxes.html
  # VB_VER=5.2.8
  # sudo wget -q http://download.virtualbox.org/virtualbox/${VB_VER}/VBoxGuestAdditions_${VB_VER}.iso
  # sudo mkdir /media/VBoxGuestAdditions
  # sudo mount -o loop,ro VBoxGuestAdditions_${VB_VER}.iso /media/VBoxGuestAdditions
  # sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
  # # sudo sh /media/xenial/VBOXADDITIONS_5.1.30_118389/autorun.sh.
  # # rm VBoxGuestAdditions_${VB_VER}.iso
  # # sudo umount /media/VBoxGuestAdditions
  # # sudo rmdir /media/VBoxGuestAdditions

  # https://github.com/arnemertz/Xubuntu1604_DevBox/blob/master/provision/provision.sh
  echo -----------------------------------
  echo INSTALL GIT
  echo -----------------------------------
  sudo apt-get -y install git
  sudo apt-get -f install

  echo -----------------------------------
  echo INSTALL ATOM
  echo -----------------------------------
  sudo wget -c https://atom.io/download/deb -O atom-amd64.deb
  dpkg -i atom-amd64.deb
  sudo apt-get -f install

  # Add the repo
  # curl -L https://packagecloud.io/AtomEditor/atom/gpgkey | sudo apt-key add -
  # sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/AtomEditor/atom/any/ any main" > /etc/apt/sources.list.d/atom.list'
  # sudo apt-get -y update
  # # Install Atom
  # sudo apt-get -y install atom


  echo -----------------------------------
  echo INSTALL Visual Studio Code
  echo -----------------------------------
  # ref: https://askubuntu.com/questions/616075/how-do-i-install-visual-studio-code
  sudo apt install snapd-xdg-open
  sudo snap install vscode --classic

  # # echo -----------------------------------
  # # echo INSTALL CLANG COMPILER
  # # echo -----------------------------------
  # #
  # # CLANG_VERSION=5.0.1
  # #
  # # for PROG in clang lldb; do
  # # 	sudo apt-get -y install ${PROG}-${CLANG_VERSION}
  # # 	for C in /usr/bin/${PROG}*${CLANG_VERSION}; do
  # # 		L=${C%-$CLANG_VERSION}
  # # 		B=$(basename $L)
  # # 		sudo update-alternatives --install $L $B $C 1000
  # # 	done
  # # done
  # #
  # # sudo update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100
  # # sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++ 100

  echo -----------------------------------
  echo INSTALL CMAKE
  echo -----------------------------------
  sudo apt-get -y install cmake
  # sudo apt-get -f install

  echo -----------------------------------
  echo DOWNLOAD CLION
  echo -----------------------------------
  CLION_VERSION=2017.3.4
  sudo wget -q http://download.jetbrains.com/cpp/CLion-${CLION_VERSION}.tar.gz
  # sudo wget -q http://download.jetbrains.com/cpp/CLion-2017.3.4.tar.gz
  sudo tar xfz CLion-${CLION_VERSION}.tar.gz -C /opt
  # sudo tar xfz CLion-2017.3.4.tar.gz -C /opt

  echo -----------------------------------
  echo CREATE CLION LAUNCHER TOOL
  echo -----------------------------------
  # https://askubuntu.com/questions/141229/how-to-add-a-shell-script-to-launcher-as-shortcut
  FILE=/usr/share/applications/jetbrains-clion.desktop

  /bin/cat <<EOM >$FILE
  [Desktop Entry]
  Version=1.0
  Type=Application
  Name=CLion
  Icon=/opt/clion-${CLION_VERSION}/bin/clion.svg
  Exec="/opt/clion-${CLION_VERSION}/bin/clion.sh" %f
  Comment=The Drive to Develop
  Categories=Development;IDE;
  Terminal=false
  StartupWMClass=jetbrains-clion
EOM

  echo -----------------------------------
  echo DOWNLOAD PYCHARM
  echo -----------------------------------
  sudo snap install pycharm-professional --classic    # Full-featured IDE for Python & Web development
  # sudo snap install pycharm-community --classic     # Free Lightweight IDE for Python & Scientific development
  # Note. PyCharm is pretty nice, but agonizingly slow in a virtualbox environment.

  # Alternative, use the same method as Clion...   the whole snap thing leaes way odd feedback, takes a long time.
  # https://download.jetbrains.com/python/pycharm-professional-2017.3.4.tar.gz

  # echo -----------------------------------
  # echo DOWNLOAD CANOPY
  # echo -----------------------------------
  # Canopy is a pretty awesome IDE for Python.. Runs very well inside a virtual environment.
  # Unfortuantely it doesn't seem like an install that can be easily automated.
  # Any shell we write would be very fragile if the folks at Enthought update the software package.
  # Perhaps we should start up the browser and navigate to https://store.enthought.com/downloads/

  echo -----------------------------------
  echo Install support for Coursera DSP class...
  echo -----------------------------------
  # clone the repo
  # sudo cd ~/
  # git clone https://github.com/MTG/sms-tools.git    #ouch.  installing the repo from here makes it root access only.
  # check out this posting: https://stackoverflow.com/questions/23841427/setting-up-shell-script-for-vagrant-setup
  # https://stackoverflow.com/questions/1988249/how-do-i-use-su-to-execute-the-rest-of-the-bash-script-as-that-user
  su -c "git clone https://github.com/MTG/sms-tools.git" -m "vagrant"    # seperate mutiple commands inside the quotes with semicolon ;

  # install pip
  sudo apt-get -y install python-pip python-dev build-essential
  sudo pip install --upgrade pip
  sudo pip install --upgrade virtualenv

  # install iPython
  sudo python -m pip install --upgrade pip
  sudo python -m pip install jupyter

  # Install and compile special tools per readme.md guidelines for sms-tools
  su -c "sudo apt-get install python-dev ipython python-numpy python-matplotlib python-scipy cython" -m "vagrant"
  su -c "cd sms-tools/software/models/utilFunctions_C ; python compileModule.py build_ext --inplace" -m "vagrant"

  echo -----------------------------------
  echo Turn Off the Screen Saver
  echo -----------------------------------
  # https://askubuntu.com/questions/544818/how-do-i-disable-automatic-screen-locking-in-xubuntu

  sudo killall light-locker

  echo -----------------------------------
  echo ALL DONE...
  echo -----------------------------------

SHELL


end

## xubuntu-desktop installs XFCE Desktop
## virtualbox-guest-dkms allows for flexible desktop sizing
## http://purpleplutonium.blogspot.com/2014/04/how-to-create-new-ubuntu-1404-vagrant.html
## sudo apt-get install g++ cmake libglu-dev libxi-dev
## reference: https://gist.github.com/fernandoaleman/5083680   (how to update VBox Guest Additions)

## note to self.. need to fix guest additions here...

## clipboard problems: https://superuser.com/questions/42134/how-do-i-enable-the-shared-clipboard-in-virtualbox
##  apt-get install make gcc linux-headers-$(uname -r)
##  sudo rcvboxadd setup
##  sudo apt-get install virtualbox-guest-x11
