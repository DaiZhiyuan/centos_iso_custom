centos_iso_custom
=================

custom the centos ISO  

build the CentOS RPM

##Step1.
Get the developer host ready:

[root@hostname ~]# yum install -y createrepo rpm-build gcc make

add an new user for development

[userid@hostname ~]$ mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}

[userid@hostname ~]$ echo '%_topdir %(echo $HOME)/rpmbuild' > ~/.rpmmacros


##Step2. 
Get the source package from the redhat

http://vault.centos.org

http://ftp.redhat.com/pub/redhat/linux/enterprise/6Server/en/os/

##Step3.
rebuild the rpm

[userid@hostname ~]$ rpm -ivh target_package.src.rpm

edit the spec

[userid@hostname ~]$ rpmbuild -ba target_package.spec

##Step4. 
rebuild the repo file

[userid@hostname ~]$ mount -o loop CentOS.iso /mnt

[userid@hostname ~]$ mkdir ~/centos_iso

[userid@hostname ~]$ rsync -avP /mnt/* ~/centos_iso

copy the rpm to new Packages.

[userid@hostname ~]$ cd ~/centos_iso/Packages

[userid@hostname ~]$ createrepo ..

edit the repomd.xml , copy the group_z group part from the existing repodata.


##Step5. 
UltraISO edit the iso file and then replace with the new files.
