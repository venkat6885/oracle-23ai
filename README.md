# oracle-23ai

1. Downloaded Oracle Virtual Box 7.0.22
2. Pre-requisites to install Oracle Virtual Box are Microsoft Visual C++ Redistributable version 19, Python, pywin32, 
      Microsoft Visual C++ Redistributable latest supported downloads	https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170
      Install Python then pip install pywin32 from cmd prompt to fix the below missing dependencies.
3. Install Oracle Virtual Box 7.0.22
4. Install Oracle Linux 8 using https://github.com/oracle/vagrant-projects/tree/main/OracleLinux/8. You can browse https://github.com/Oracle for all the repositories.
5. You can follow below mentioned steps at https://github.com/oracle/vagrant-projects/tree/main/OracleLinux/8, ensure vagarnt is installed on your system.
      Clone this repository git clone https://github.com/oracle/vagrant-projects
      Change into the vagrant-projects/OracleLinux/8 directory
      Run vagrant status to check Vagrantfile status and possible plugin(s) required
      Run vagrant up
      The first time you run this it will provision everything and may take a while. Ensure you have a good internet connection!
      The Vagrant file allows for customization.
      SSH into the VM either by using vagrant ssh If required, by Vagrantfile you can also setup ssh port forwarding.
      You can shut down the VM via the usual vagrant halt and the start it up again via vagrant up.

6. Used https://github.com/oracle/vagrant-projects/tree/main/OracleLinux/8 git repo to install Oracle Linux 8 on the laptop.

Once OEL 8 is ready, I have installed Oracle Database 23ai Free on Linux.

Download Oracle Database 23ai Free on Linux from https://www.oracle.com/in/database/technologies/oracle-database-software-downloads.html#db_free
Follow the steps under Enterprise Linux 8 in https://www.oracle.com/in/database/free/get-started/

oracle-database-preinstall-23ai-1.0-2.el8.x86_64.rpm
oracle-database-free-23ai-1.0-1.el8.x86_64.rpm

as a root user,

	
Run dnf install -y oracle-database-preinstall*
Run dnf install -y oracle-database-free*
Run /etc/init.d/oracle-free-23ai configure

which Installs and creates Oracle database.

Feature.

1. All tablespaces except temp are Big file tablespaces in Oracle 23ai.

Below are the steps.

$ ssh vagrant
Welcome to Oracle Linux Server release 8.10 (GNU/Linux 5.15.0-206.153.7.el8uek.x86_64)

The Oracle Linux End-User License Agreement can be viewed here:

  * /usr/share/eula/eula.en_US

For additional packages, updates, documentation and community help, see:

  * https://yum.oracle.com/

[vagrant@ol8-vagrant ~]$ 
Welcome to Oracle Linux Server release 8.10 (GNU/Linux 5.15.0-206.153.7.el8uek.x86_64)

The Oracle Linux End-User License Agreement can be viewed here:

  * /usr/share/eula/eula.en_US

For additional packages, updates, documentation and community help, see:

  * https://yum.oracle.com/

[vagrant@ol8-vagrant ~]$ 
[vagrant@ol8-vagrant ~]$ df -h
Filesystem                   Size  Used Avail Use% Mounted on
devtmpfs                     955M     0  955M   0% /dev
tmpfs                        980M     0  980M   0% /dev/shm
tmpfs                        980M   17M  964M   2% /run
tmpfs                        980M     0  980M   0% /sys/fs/cgroup
/dev/mapper/vg_main-lv_root   32G  2.3G   30G   8% /
/dev/sda1                   1014M  173M  842M  18% /boot
tmpfs                        196M     0  196M   0% /run/user/1000
vagrant                      473G  385G   89G  82% /media/sf_vagrant
Downloads                    473G  385G   89G  82% /media/sf_Downloads
[vagrant@ol8-vagrant ~]$ sudo -u root -i
[root@ol8-vagrant ~]# cd /media/sf_Downloads/
[root@ol8-vagrant sf_Downloads]# 
[root@ol8-vagrant sf_Downloads]# ll *database*
-rwxrwx---. 1 root vboxsf 1379391728 Nov 30 06:09 oracle-database-free-23ai-1.0-1.el8.x86_64.rpm
-rwxrwx---. 1 root vboxsf      31152 Dec  2 05:54 oracle-database-preinstall-23ai-1.0-2.el8.x86_64.rpm
[root@ol8-vagrant sf_Downloads]#
[root@ol8-vagrant sf_Downloads]#
[root@ol8-vagrant sf_Downloads]# rpm -qa|grep -i preinstall
[root@ol8-vagrant sf_Downloads]# dnf install -y oracle-database-preinstall*
Last metadata expiration check: 20:40:22 ago on Sun 01 Dec 2024 09:19:31 AM UTC.
Dependencies resolved.
==================================================================================================================================================================================================================
 Package                                                     Architecture                       Version                                                       Repository                                     Size
==================================================================================================================================================================================================================
Installing:
 oracle-database-preinstall-23ai                             x86_64                             1.0-2.el8                                                     @commandline                                   30 k
Installing dependencies:
 bc                                                          x86_64                             1.07.1-5.el8                                                  ol8_baseos_latest                             129 k
 bind-libs                                                   x86_64                             32:9.11.36-16.el8_10.2                                        ol8_appstream                                 176 k
 bind-libs-lite                                              x86_64                             32:9.11.36-16.el8_10.2                                        ol8_appstream                                 1.2 M
 bind-license                                                noarch                             32:9.11.36-16.el8_10.2                                        ol8_appstream                                 104 k
 bind-utils                                                  x86_64                             32:9.11.36-16.el8_10.2                                        ol8_appstream                                 453 k
 compat-openssl10                                            x86_64                             1:1.0.2o-4.el8_6                                              ol8_appstream                                 1.1 M
 dejavu-fonts-common                                         noarch                             2.35-7.el8                                                    ol8_baseos_latest                              74 k
 dejavu-sans-fonts                                           noarch                             2.35-7.el8                                                    ol8_baseos_latest                             1.5 M
 fontconfig                                                  x86_64                             2.13.1-4.el8                                                  ol8_baseos_latest                             274 k
 fontpackages-filesystem                                     noarch                             1.44-22.el8                                                   ol8_baseos_latest                              16 k
 fstrm                                                       x86_64                             0.6.1-3.el8                                                   ol8_appstream                                  29 k
 gssproxy                                                    x86_64                             0.8.0-21.el8                                                  ol8_baseos_latest                             119 k
 keyutils                                                    x86_64                             1.5.10-9.0.1.el8                                              ol8_baseos_latest                              65 k
 ksh                                                         x86_64                             20120801-267.0.1.el8                                          ol8_appstream                                 923 k
 libICE                                                      x86_64                             1.0.9-15.el8                                                  ol8_appstream                                  74 k
 libSM                                                       x86_64                             1.2.3-1.el8                                                   ol8_appstream                                  47 k
 libX11                                                      x86_64                             1.6.8-9.el8_10                                                ol8_appstream                                 611 k
 libX11-common                                               noarch                             1.6.8-9.el8_10                                                ol8_appstream                                 157 k
 libX11-xcb                                                  x86_64                             1.6.8-9.el8_10                                                ol8_appstream                                  14 k
 libXau                                                      x86_64                             1.0.9-3.el8                                                   ol8_appstream                                  37 k
 libXcomposite                                               x86_64                             0.4.4-14.el8                                                  ol8_appstream                                  28 k
 libXext                                                     x86_64                             1.3.4-1.el8                                                   ol8_appstream                                  45 k
 libXi                                                       x86_64                             1.7.10-1.el8                                                  ol8_appstream                                  49 k
 libXinerama                                                 x86_64                             1.1.4-1.el8                                                   ol8_appstream                                  15 k
 libXmu                                                      x86_64                             1.1.3-1.el8                                                   ol8_appstream                                  75 k
 libXrandr                                                   x86_64                             1.5.2-1.el8                                                   ol8_appstream                                  34 k
 libXrender                                                  x86_64                             0.9.10-7.el8                                                  ol8_appstream                                  33 k
 libXt                                                       x86_64                             1.1.5-12.el8                                                  ol8_appstream                                 185 k
 libXtst                                                     x86_64                             1.2.3-7.el8                                                   ol8_appstream                                  22 k
 libXv                                                       x86_64                             1.0.11-7.el8                                                  ol8_appstream                                  20 k
 libXxf86dga                                                 x86_64                             1.1.5-1.el8                                                   ol8_appstream                                  26 k
 libXxf86misc                                                x86_64                             1.0.4-1.el8                                                   ol8_appstream                                  23 k
 libXxf86vm                                                  x86_64                             1.1.4-9.el8                                                   ol8_appstream                                  19 k
 libbasicobjects                                             x86_64                             0.1.1-40.el8                                                  ol8_baseos_latest                              31 k
 libcollection                                               x86_64                             0.7.0-40.el8                                                  ol8_baseos_latest                              48 k
 libdmx                                                      x86_64                             1.1.4-3.el8                                                   ol8_appstream                                  22 k
 libev                                                       x86_64                             4.24-6.el8                                                    ol8_appstream                                  52 k
 libini_config                                               x86_64                             1.3.1-40.el8                                                  ol8_baseos_latest                              70 k
 libmaxminddb                                                x86_64                             1.2.0-10.el8_9.1                                              ol8_appstream                                  32 k
 libnfsidmap                                                 x86_64                             1:2.3.3-59.0.2.el8                                            ol8_UEKR7                                     121 k
 libpath_utils                                               x86_64                             0.2.1-40.el8                                                  ol8_baseos_latest                              34 k
 libref_array                                                x86_64                             0.1.5-40.el8                                                  ol8_baseos_latest                              33 k
 libverto-libev                                              x86_64                             0.3.2-2.el8                                                   ol8_appstream                                  16 k
 libxcb                                                      x86_64                             1.13.1-1.el8                                                  ol8_appstream                                 231 k
 lm_sensors-libs                                             x86_64                             3.4.0-23.20180522git70f7e08.el8                               ol8_baseos_latest                              59 k
 net-tools                                                   x86_64                             2.0-0.52.20160912git.el8                                      ol8_baseos_latest                             322 k
 nfs-utils                                                   x86_64                             1:2.3.3-59.0.2.el8                                            ol8_UEKR7                                     516 k
 protobuf-c                                                  x86_64                             1.3.0-8.el8                                                   ol8_appstream                                  37 k
 python3-bind                                                noarch                             32:9.11.36-16.el8_10.2                                        ol8_appstream                                 151 k
 python3-ply                                                 noarch                             3.9-9.el8                                                     ol8_baseos_latest                             111 k
 python3-pyyaml                                              x86_64                             3.12-12.el8                                                   ol8_baseos_latest                             193 k
 quota                                                       x86_64                             1:4.04-14.el8                                                 ol8_baseos_latest                             214 k
 quota-nls                                                   noarch                             1:4.04-14.el8                                                 ol8_baseos_latest                              95 k
 rpcbind                                                     x86_64                             1.2.5-10.el8                                                  ol8_baseos_latest                              70 k
 smartmontools                                               x86_64                             1:7.1-3.el8                                                   ol8_baseos_latest                             556 k
 sysstat                                                     x86_64                             11.7.3-13.0.1.el8_10                                          ol8_appstream                                 426 k
 xorg-x11-utils                                              x86_64                             7.5-28.el8                                                    ol8_appstream                                 136 k
 xorg-x11-xauth                                              x86_64                             1:1.0.9-12.el8                                                ol8_appstream                                  39 k
Installing weak dependencies:
 geolite2-city                                               noarch                             20180605-1.el8                                                ol8_appstream                                  19 M
 geolite2-country                                            noarch                             20180605-1.el8                                                ol8_appstream                                 1.0 M

Transaction Summary
==================================================================================================================================================================================================================
Install  61 Packages

Total size: 31 M
Total download size: 31 M
Installed size: 90 M
Downloading Packages:
(1/60): dejavu-fonts-common-2.35-7.el8.noarch.rpm                                                                                                                                 118 kB/s |  74 kB     00:00
(2/60): bc-1.07.1-5.el8.x86_64.rpm                                                                                                                                                154 kB/s | 129 kB     00:00
(3/60): fontpackages-filesystem-1.44-22.el8.noarch.rpm                                                                                                                            199 kB/s |  16 kB     00:00
(4/60): fontconfig-2.13.1-4.el8.x86_64.rpm                                                                                                                                        846 kB/s | 274 kB     00:00
(5/60): keyutils-1.5.10-9.0.1.el8.x86_64.rpm                                                                                                                                      613 kB/s |  65 kB     00:00
(6/60): gssproxy-0.8.0-21.el8.x86_64.rpm                                                                                                                                          690 kB/s | 119 kB     00:00
(7/60): dejavu-sans-fonts-2.35-7.el8.noarch.rpm                                                                                                                                   1.3 MB/s | 1.5 MB     00:01
(8/60): libcollection-0.7.0-40.el8.x86_64.rpm                                                                                                                                     338 kB/s |  48 kB     00:00
(9/60): libbasicobjects-0.1.1-40.el8.x86_64.rpm                                                                                                                                   179 kB/s |  31 kB     00:00
(10/60): libini_config-1.3.1-40.el8.x86_64.rpm                                                                                                                                    503 kB/s |  70 kB     00:00
(11/60): libref_array-0.1.5-40.el8.x86_64.rpm                                                                                                                                     385 kB/s |  33 kB     00:00
(12/60): libpath_utils-0.2.1-40.el8.x86_64.rpm                                                                                                                                    288 kB/s |  34 kB     00:00
(13/60): lm_sensors-libs-3.4.0-23.20180522git70f7e08.el8.x86_64.rpm                                                                                                               590 kB/s |  59 kB     00:00
(14/60): python3-pyyaml-3.12-12.el8.x86_64.rpm                                                                                                                                    1.4 MB/s | 193 kB     00:00
(15/60): python3-ply-3.9-9.el8.noarch.rpm                                                                                                                                         630 kB/s | 111 kB     00:00
(16/60): net-tools-2.0-0.52.20160912git.el8.x86_64.rpm                                                                                                                            1.5 MB/s | 322 kB     00:00
(17/60): quota-nls-4.04-14.el8.noarch.rpm                                                                                                                                         1.0 MB/s |  95 kB     00:00
(18/60): quota-4.04-14.el8.x86_64.rpm                                                                                                                                             1.6 MB/s | 214 kB     00:00
(19/60): rpcbind-1.2.5-10.el8.x86_64.rpm                                                                                                                                          611 kB/s |  70 kB     00:00
(20/60): bind-libs-9.11.36-16.el8_10.2.x86_64.rpm                                                                                                                                 1.4 MB/s | 176 kB     00:00
(21/60): bind-license-9.11.36-16.el8_10.2.noarch.rpm                                                                                                                              1.0 MB/s | 104 kB     00:00
(22/60): smartmontools-7.1-3.el8.x86_64.rpm                                                                                                                                       1.8 MB/s | 556 kB     00:00
(23/60): bind-utils-9.11.36-16.el8_10.2.x86_64.rpm                                                                                                                                1.5 MB/s | 453 kB     00:00
(24/60): fstrm-0.6.1-3.el8.x86_64.rpm                                                                                                                                             335 kB/s |  29 kB     00:00
(25/60): compat-openssl10-1.0.2o-4.el8_6.x86_64.rpm                                                                                                                               1.4 MB/s | 1.1 MB     00:00
(26/60): bind-libs-lite-9.11.36-16.el8_10.2.x86_64.rpm                                                                                                                            717 kB/s | 1.2 MB     00:01
(27/60): geolite2-country-20180605-1.el8.noarch.rpm                                                                                                                               1.2 MB/s | 1.0 MB     00:00
(28/60): libICE-1.0.9-15.el8.x86_64.rpm                                                                                                                                           493 kB/s |  74 kB     00:00
(29/60): libSM-1.2.3-1.el8.x86_64.rpm                                                                                                                                             294 kB/s |  47 kB     00:00
(30/60): libX11-1.6.8-9.el8_10.x86_64.rpm                                                                                                                                         1.0 MB/s | 611 kB     00:00
(31/60): libX11-common-1.6.8-9.el8_10.noarch.rpm                                                                                                                                  753 kB/s | 157 kB     00:00
(32/60): libX11-xcb-1.6.8-9.el8_10.x86_64.rpm                                                                                                                                     117 kB/s |  14 kB     00:00
(33/60): ksh-20120801-267.0.1.el8.x86_64.rpm                                                                                                                                      564 kB/s | 923 kB     00:01
(34/60): libXau-1.0.9-3.el8.x86_64.rpm                                                                                                                                            244 kB/s |  37 kB     00:00
(35/60): libXcomposite-0.4.4-14.el8.x86_64.rpm                                                                                                                                    307 kB/s |  28 kB     00:00
(36/60): libXext-1.3.4-1.el8.x86_64.rpm                                                                                                                                           376 kB/s |  45 kB     00:00
(37/60): libXi-1.7.10-1.el8.x86_64.rpm                                                                                                                                            559 kB/s |  49 kB     00:00
(38/60): libXinerama-1.1.4-1.el8.x86_64.rpm                                                                                                                                       199 kB/s |  15 kB     00:00
(39/60): libXmu-1.1.3-1.el8.x86_64.rpm                                                                                                                                            626 kB/s |  75 kB     00:00
(40/60): libXrandr-1.5.2-1.el8.x86_64.rpm                                                                                                                                         264 kB/s |  34 kB     00:00
(41/60): libXrender-0.9.10-7.el8.x86_64.rpm                                                                                                                                       354 kB/s |  33 kB     00:00
(42/60): libXtst-1.2.3-7.el8.x86_64.rpm                                                                                                                                           192 kB/s |  22 kB     00:00
(43/60): libXt-1.1.5-12.el8.x86_64.rpm                                                                                                                                            648 kB/s | 185 kB     00:00
(44/60): libXv-1.0.11-7.el8.x86_64.rpm                                                                                                                                            177 kB/s |  20 kB     00:00
(45/60): libXxf86misc-1.0.4-1.el8.x86_64.rpm                                                                                                                                      194 kB/s |  23 kB     00:00
(46/60): libXxf86dga-1.1.5-1.el8.x86_64.rpm                                                                                                                                       159 kB/s |  26 kB     00:00
(47/60): libdmx-1.1.4-3.el8.x86_64.rpm                                                                                                                                            184 kB/s |  22 kB     00:00
(48/60): libXxf86vm-1.1.4-9.el8.x86_64.rpm                                                                                                                                        117 kB/s |  19 kB     00:00
(49/60): libmaxminddb-1.2.0-10.el8_9.1.x86_64.rpm                                                                                                                                 299 kB/s |  32 kB     00:00
(50/60): libev-4.24-6.el8.x86_64.rpm                                                                                                                                              308 kB/s |  52 kB     00:00
(51/60): libverto-libev-0.3.2-2.el8.x86_64.rpm                                                                                                                                    173 kB/s |  16 kB     00:00
(52/60): protobuf-c-1.3.0-8.el8.x86_64.rpm                                                                                                                                        238 kB/s |  37 kB     00:00
(53/60): libxcb-1.13.1-1.el8.x86_64.rpm                                                                                                                                           669 kB/s | 231 kB     00:00
(54/60): python3-bind-9.11.36-16.el8_10.2.noarch.rpm                                                                                                                              729 kB/s | 151 kB     00:00
(55/60): xorg-x11-utils-7.5-28.el8.x86_64.rpm                                                                                                                                     291 kB/s | 136 kB     00:00
(56/60): sysstat-11.7.3-13.0.1.el8_10.x86_64.rpm                                                                                                                                  684 kB/s | 426 kB     00:00
(57/60): xorg-x11-xauth-1.0.9-12.el8.x86_64.rpm                                                                                                                                   308 kB/s |  39 kB     00:00
(58/60): libnfsidmap-2.3.3-59.0.2.el8.x86_64.rpm                                                                                                                                  523 kB/s | 121 kB     00:00
(59/60): nfs-utils-2.3.3-59.0.2.el8.x86_64.rpm                                                                                                                                    1.1 MB/s | 516 kB     00:00
(60/60): geolite2-city-20180605-1.el8.noarch.rpm                                                                                                                                  2.5 MB/s |  19 MB     00:07
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                             3.2 MB/s |  31 MB     00:09
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                          1/1
  Installing       : protobuf-c-1.3.0-8.el8.x86_64                                                                                                                                                           1/61
  Installing       : fstrm-0.6.1-3.el8.x86_64                                                                                                                                                                2/61
  Installing       : bind-license-32:9.11.36-16.el8_10.2.noarch                                                                                                                                              3/61
  Installing       : libXau-1.0.9-3.el8.x86_64                                                                                                                                                               4/61
  Installing       : libxcb-1.13.1-1.el8.x86_64                                                                                                                                                              5/61
  Installing       : libICE-1.0.9-15.el8.x86_64                                                                                                                                                              6/61
  Installing       : libref_array-0.1.5-40.el8.x86_64                                                                                                                                                        7/61
  Installing       : libcollection-0.7.0-40.el8.x86_64                                                                                                                                                       8/61
  Installing       : libbasicobjects-0.1.1-40.el8.x86_64                                                                                                                                                     9/61
  Installing       : fontpackages-filesystem-1.44-22.el8.noarch                                                                                                                                             10/61
  Installing       : dejavu-fonts-common-2.35-7.el8.noarch                                                                                                                                                  11/61
  Installing       : dejavu-sans-fonts-2.35-7.el8.noarch                                                                                                                                                    12/61
  Installing       : fontconfig-2.13.1-4.el8.x86_64                                                                                                                                                         13/61
  Running scriptlet: fontconfig-2.13.1-4.el8.x86_64                                                                                                                                                         13/61
  Installing       : libSM-1.2.3-1.el8.x86_64                                                                                                                                                               14/61
  Installing       : libnfsidmap-1:2.3.3-59.0.2.el8.x86_64                                                                                                                                                  15/61
  Installing       : libev-4.24-6.el8.x86_64                                                                                                                                                                16/61
  Installing       : libverto-libev-0.3.2-2.el8.x86_64                                                                                                                                                      17/61
  Installing       : libX11-xcb-1.6.8-9.el8_10.x86_64                                                                                                                                                       18/61
  Installing       : libX11-common-1.6.8-9.el8_10.noarch                                                                                                                                                    19/61
  Installing       : libX11-1.6.8-9.el8_10.x86_64                                                                                                                                                           20/61
  Installing       : libXext-1.3.4-1.el8.x86_64                                                                                                                                                             21/61
  Installing       : libXi-1.7.10-1.el8.x86_64                                                                                                                                                              22/61
  Installing       : libXrender-0.9.10-7.el8.x86_64                                                                                                                                                         23/61
  Installing       : libXrandr-1.5.2-1.el8.x86_64                                                                                                                                                           24/61
  Installing       : libXtst-1.2.3-7.el8.x86_64                                                                                                                                                             25/61
  Installing       : libXinerama-1.1.4-1.el8.x86_64                                                                                                                                                         26/61
  Installing       : libXv-1.0.11-7.el8.x86_64                                                                                                                                                              27/61
  Installing       : libXxf86dga-1.1.5-1.el8.x86_64                                                                                                                                                         28/61
  Installing       : libXxf86misc-1.0.4-1.el8.x86_64                                                                                                                                                        29/61
  Installing       : libXxf86vm-1.1.4-9.el8.x86_64                                                                                                                                                          30/61
  Installing       : libdmx-1.1.4-3.el8.x86_64                                                                                                                                                              31/61
  Installing       : libXcomposite-0.4.4-14.el8.x86_64                                                                                                                                                      32/61
  Installing       : xorg-x11-utils-7.5-28.el8.x86_64                                                                                                                                                       33/61
  Installing       : libXt-1.1.5-12.el8.x86_64                                                                                                                                                              34/61
  Installing       : libXmu-1.1.3-1.el8.x86_64                                                                                                                                                              35/61
  Installing       : xorg-x11-xauth-1:1.0.9-12.el8.x86_64                                                                                                                                                   36/61
  Installing       : ksh-20120801-267.0.1.el8.x86_64                                                                                                                                                        37/61
  Running scriptlet: ksh-20120801-267.0.1.el8.x86_64                                                                                                                                                        37/61
  Installing       : geolite2-country-20180605-1.el8.noarch                                                                                                                                                 38/61
  Installing       : geolite2-city-20180605-1.el8.noarch                                                                                                                                                    39/61
  Installing       : libmaxminddb-1.2.0-10.el8_9.1.x86_64                                                                                                                                                   40/61
  Running scriptlet: libmaxminddb-1.2.0-10.el8_9.1.x86_64                                                                                                                                                   40/61
  Installing       : bind-libs-lite-32:9.11.36-16.el8_10.2.x86_64                                                                                                                                           41/61
  Installing       : bind-libs-32:9.11.36-16.el8_10.2.x86_64                                                                                                                                                42/61
  Installing       : compat-openssl10-1:1.0.2o-4.el8_6.x86_64                                                                                                                                               43/61
  Running scriptlet: compat-openssl10-1:1.0.2o-4.el8_6.x86_64                                                                                                                                               43/61
  Running scriptlet: smartmontools-1:7.1-3.el8.x86_64                                                                                                                                                       44/61
  Installing       : smartmontools-1:7.1-3.el8.x86_64                                                                                                                                                       44/61
  Running scriptlet: smartmontools-1:7.1-3.el8.x86_64                                                                                                                                                       44/61
  Running scriptlet: rpcbind-1.2.5-10.el8.x86_64                                                                                                                                                            45/61
  Installing       : rpcbind-1.2.5-10.el8.x86_64                                                                                                                                                            45/61
  Running scriptlet: rpcbind-1.2.5-10.el8.x86_64                                                                                                                                                            45/61
  Installing       : quota-nls-1:4.04-14.el8.noarch                                                                                                                                                         46/61
  Installing       : quota-1:4.04-14.el8.x86_64                                                                                                                                                             47/61
  Installing       : python3-pyyaml-3.12-12.el8.x86_64                                                                                                                                                      48/61
  Installing       : python3-ply-3.9-9.el8.noarch                                                                                                                                                           49/61
  Installing       : python3-bind-32:9.11.36-16.el8_10.2.noarch                                                                                                                                             50/61
  Installing       : bind-utils-32:9.11.36-16.el8_10.2.x86_64                                                                                                                                               51/61
  Installing       : net-tools-2.0-0.52.20160912git.el8.x86_64                                                                                                                                              52/61
  Running scriptlet: net-tools-2.0-0.52.20160912git.el8.x86_64                                                                                                                                              52/61
  Installing       : lm_sensors-libs-3.4.0-23.20180522git70f7e08.el8.x86_64                                                                                                                                 53/61
  Running scriptlet: lm_sensors-libs-3.4.0-23.20180522git70f7e08.el8.x86_64                                                                                                                                 53/61
  Installing       : sysstat-11.7.3-13.0.1.el8_10.x86_64                                                                                                                                                    54/61
  Running scriptlet: sysstat-11.7.3-13.0.1.el8_10.x86_64                                                                                                                                                    54/61
  Installing       : libpath_utils-0.2.1-40.el8.x86_64                                                                                                                                                      55/61
  Installing       : libini_config-1.3.1-40.el8.x86_64                                                                                                                                                      56/61
  Installing       : gssproxy-0.8.0-21.el8.x86_64                                                                                                                                                           57/61
  Running scriptlet: gssproxy-0.8.0-21.el8.x86_64                                                                                                                                                           57/61
  Installing       : keyutils-1.5.10-9.0.1.el8.x86_64                                                                                                                                                       58/61
  Running scriptlet: nfs-utils-1:2.3.3-59.0.2.el8.x86_64                                                                                                                                                    59/61
  Installing       : nfs-utils-1:2.3.3-59.0.2.el8.x86_64                                                                                                                                                    59/61
  Running scriptlet: nfs-utils-1:2.3.3-59.0.2.el8.x86_64                                                                                                                                                    59/61
  Installing       : bc-1.07.1-5.el8.x86_64                                                                                                                                                                 60/61
  Running scriptlet: bc-1.07.1-5.el8.x86_64                                                                                                                                                                 60/61
  Installing       : oracle-database-preinstall-23ai-1.0-2.el8.x86_64                                                                                                                                       61/61
  Running scriptlet: oracle-database-preinstall-23ai-1.0-2.el8.x86_64                                                                                                                                       61/61


  Running scriptlet: fontconfig-2.13.1-4.el8.x86_64                                                                                                                                                         61/61
  Verifying        : bc-1.07.1-5.el8.x86_64                                                                                                                                                                  1/61
  Verifying        : dejavu-fonts-common-2.35-7.el8.noarch                                                                                                                                                   2/61
  Verifying        : dejavu-sans-fonts-2.35-7.el8.noarch                                                                                                                                                     3/61
  Verifying        : fontconfig-2.13.1-4.el8.x86_64                                                                                                                                                          4/61
  Verifying        : fontpackages-filesystem-1.44-22.el8.noarch                                                                                                                                              5/61
  Verifying        : gssproxy-0.8.0-21.el8.x86_64                                                                                                                                                            6/61
  Verifying        : keyutils-1.5.10-9.0.1.el8.x86_64                                                                                                                                                        7/61
  Verifying        : libbasicobjects-0.1.1-40.el8.x86_64                                                                                                                                                     8/61
  Verifying        : libcollection-0.7.0-40.el8.x86_64                                                                                                                                                       9/61
  Verifying        : libini_config-1.3.1-40.el8.x86_64                                                                                                                                                      10/61
  Verifying        : libpath_utils-0.2.1-40.el8.x86_64                                                                                                                                                      11/61
  Verifying        : libref_array-0.1.5-40.el8.x86_64                                                                                                                                                       12/61
  Verifying        : lm_sensors-libs-3.4.0-23.20180522git70f7e08.el8.x86_64                                                                                                                                 13/61
  Verifying        : net-tools-2.0-0.52.20160912git.el8.x86_64                                                                                                                                              14/61
  Verifying        : python3-ply-3.9-9.el8.noarch                                                                                                                                                           15/61
  Verifying        : python3-pyyaml-3.12-12.el8.x86_64                                                                                                                                                      16/61
  Verifying        : quota-1:4.04-14.el8.x86_64                                                                                                                                                             17/61
  Verifying        : quota-nls-1:4.04-14.el8.noarch                                                                                                                                                         18/61
  Verifying        : rpcbind-1.2.5-10.el8.x86_64                                                                                                                                                            19/61
  Verifying        : smartmontools-1:7.1-3.el8.x86_64                                                                                                                                                       20/61
  Verifying        : bind-libs-32:9.11.36-16.el8_10.2.x86_64                                                                                                                                                21/61
  Verifying        : bind-libs-lite-32:9.11.36-16.el8_10.2.x86_64                                                                                                                                           22/61
  Verifying        : bind-license-32:9.11.36-16.el8_10.2.noarch                                                                                                                                             23/61
  Verifying        : bind-utils-32:9.11.36-16.el8_10.2.x86_64                                                                                                                                               24/61
  Verifying        : compat-openssl10-1:1.0.2o-4.el8_6.x86_64                                                                                                                                               25/61
  Verifying        : fstrm-0.6.1-3.el8.x86_64                                                                                                                                                               26/61
  Verifying        : geolite2-city-20180605-1.el8.noarch                                                                                                                                                    27/61
  Verifying        : geolite2-country-20180605-1.el8.noarch                                                                                                                                                 28/61
  Verifying        : ksh-20120801-267.0.1.el8.x86_64                                                                                                                                                        29/61
  Verifying        : libICE-1.0.9-15.el8.x86_64                                                                                                                                                             30/61
  Verifying        : libSM-1.2.3-1.el8.x86_64                                                                                                                                                               31/61
  Verifying        : libX11-1.6.8-9.el8_10.x86_64                                                                                                                                                           32/61
  Verifying        : libX11-common-1.6.8-9.el8_10.noarch                                                                                                                                                    33/61
  Verifying        : libX11-xcb-1.6.8-9.el8_10.x86_64                                                                                                                                                       34/61
  Verifying        : libXau-1.0.9-3.el8.x86_64                                                                                                                                                              35/61
  Verifying        : libXcomposite-0.4.4-14.el8.x86_64                                                                                                                                                      36/61
  Verifying        : libXext-1.3.4-1.el8.x86_64                                                                                                                                                             37/61
  Verifying        : libXi-1.7.10-1.el8.x86_64                                                                                                                                                              38/61
  Verifying        : libXinerama-1.1.4-1.el8.x86_64                                                                                                                                                         39/61
  Verifying        : libXmu-1.1.3-1.el8.x86_64                                                                                                                                                              40/61
  Verifying        : libXrandr-1.5.2-1.el8.x86_64                                                                                                                                                           41/61
  Verifying        : libXrender-0.9.10-7.el8.x86_64                                                                                                                                                         42/61
  Verifying        : libXt-1.1.5-12.el8.x86_64                                                                                                                                                              43/61
  Verifying        : libXtst-1.2.3-7.el8.x86_64                                                                                                                                                             44/61
  Verifying        : libXv-1.0.11-7.el8.x86_64                                                                                                                                                              45/61
  Verifying        : libXxf86dga-1.1.5-1.el8.x86_64                                                                                                                                                         46/61
  Verifying        : libXxf86misc-1.0.4-1.el8.x86_64                                                                                                                                                        47/61
  Verifying        : libXxf86vm-1.1.4-9.el8.x86_64                                                                                                                                                          48/61
  Verifying        : libdmx-1.1.4-3.el8.x86_64                                                                                                                                                              49/61
  Verifying        : libev-4.24-6.el8.x86_64                                                                                                                                                                50/61
  Verifying        : libmaxminddb-1.2.0-10.el8_9.1.x86_64                                                                                                                                                   51/61
  Verifying        : libverto-libev-0.3.2-2.el8.x86_64                                                                                                                                                      52/61
  Verifying        : libxcb-1.13.1-1.el8.x86_64                                                                                                                                                             53/61
  Verifying        : protobuf-c-1.3.0-8.el8.x86_64                                                                                                                                                          54/61
  Verifying        : python3-bind-32:9.11.36-16.el8_10.2.noarch                                                                                                                                             55/61
  Verifying        : sysstat-11.7.3-13.0.1.el8_10.x86_64                                                                                                                                                    56/61
  Verifying        : xorg-x11-utils-7.5-28.el8.x86_64                                                                                                                                                       57/61
  Verifying        : xorg-x11-xauth-1:1.0.9-12.el8.x86_64                                                                                                                                                   58/61
  Verifying        : libnfsidmap-1:2.3.3-59.0.2.el8.x86_64                                                                                                                                                  59/61
  Verifying        : nfs-utils-1:2.3.3-59.0.2.el8.x86_64                                                                                                                                                    60/61
  Verifying        : oracle-database-preinstall-23ai-1.0-2.el8.x86_64                                                                                                                                       61/61

Installed:
  bc-1.07.1-5.el8.x86_64                        bind-libs-32:9.11.36-16.el8_10.2.x86_64               bind-libs-lite-32:9.11.36-16.el8_10.2.x86_64                bind-license-32:9.11.36-16.el8_10.2.noarch
  bind-utils-32:9.11.36-16.el8_10.2.x86_64      compat-openssl10-1:1.0.2o-4.el8_6.x86_64              dejavu-fonts-common-2.35-7.el8.noarch                       dejavu-sans-fonts-2.35-7.el8.noarch
  fontconfig-2.13.1-4.el8.x86_64                fontpackages-filesystem-1.44-22.el8.noarch            fstrm-0.6.1-3.el8.x86_64                                    geolite2-city-20180605-1.el8.noarch
  geolite2-country-20180605-1.el8.noarch        gssproxy-0.8.0-21.el8.x86_64                          keyutils-1.5.10-9.0.1.el8.x86_64                            ksh-20120801-267.0.1.el8.x86_64
  libICE-1.0.9-15.el8.x86_64                    libSM-1.2.3-1.el8.x86_64                              libX11-1.6.8-9.el8_10.x86_64                                libX11-common-1.6.8-9.el8_10.noarch
  libX11-xcb-1.6.8-9.el8_10.x86_64              libXau-1.0.9-3.el8.x86_64                             libXcomposite-0.4.4-14.el8.x86_64                           libXext-1.3.4-1.el8.x86_64
  libXi-1.7.10-1.el8.x86_64                     libXinerama-1.1.4-1.el8.x86_64                        libXmu-1.1.3-1.el8.x86_64                                   libXrandr-1.5.2-1.el8.x86_64
  libXrender-0.9.10-7.el8.x86_64                libXt-1.1.5-12.el8.x86_64                             libXtst-1.2.3-7.el8.x86_64                                  libXv-1.0.11-7.el8.x86_64
  libXxf86dga-1.1.5-1.el8.x86_64                libXxf86misc-1.0.4-1.el8.x86_64                       libXxf86vm-1.1.4-9.el8.x86_64                               libbasicobjects-0.1.1-40.el8.x86_64
  libcollection-0.7.0-40.el8.x86_64             libdmx-1.1.4-3.el8.x86_64                             libev-4.24-6.el8.x86_64                                     libini_config-1.3.1-40.el8.x86_64
  libmaxminddb-1.2.0-10.el8_9.1.x86_64          libnfsidmap-1:2.3.3-59.0.2.el8.x86_64                 libpath_utils-0.2.1-40.el8.x86_64                           libref_array-0.1.5-40.el8.x86_64
  libverto-libev-0.3.2-2.el8.x86_64             libxcb-1.13.1-1.el8.x86_64                            lm_sensors-libs-3.4.0-23.20180522git70f7e08.el8.x86_64      net-tools-2.0-0.52.20160912git.el8.x86_64
  nfs-utils-1:2.3.3-59.0.2.el8.x86_64           oracle-database-preinstall-23ai-1.0-2.el8.x86_64      protobuf-c-1.3.0-8.el8.x86_64                               python3-bind-32:9.11.36-16.el8_10.2.noarch
  python3-ply-3.9-9.el8.noarch                  python3-pyyaml-3.12-12.el8.x86_64                     quota-1:4.04-14.el8.x86_64                                  quota-nls-1:4.04-14.el8.noarch
  rpcbind-1.2.5-10.el8.x86_64                   smartmontools-1:7.1-3.el8.x86_64                      sysstat-11.7.3-13.0.1.el8_10.x86_64                         xorg-x11-utils-7.5-28.el8.x86_64
  xorg-x11-xauth-1:1.0.9-12.el8.x86_64

Complete!
[root@ol8-vagrant sf_Downloads]#
[root@ol8-vagrant sf_Downloads]#
[root@ol8-vagrant sf_Downloads]# dnf install -y oracle-database-free*
Last metadata expiration check: 20:41:56 ago on Sun 01 Dec 2024 09:19:31 AM UTC.
Dependencies resolved.
==================================================================================================================================================================================================================
 Package                                                        Architecture                                Version                                       Repository                                         Size
==================================================================================================================================================================================================================
Installing:
 oracle-database-free-23ai                                      x86_64                                      1.0-1                                         @commandline                                      1.3 G

Transaction Summary
==================================================================================================================================================================================================================
Install  1 Package

Total size: 1.3 G
Installed size: 3.5 G
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                          1/1
  Running scriptlet: oracle-database-free-23ai-1.0-1.x86_64                                                                                                                                                   1/1
  Installing       : oracle-database-free-23ai-1.0-1.x86_64                                                                                                                                                   1/1
  Running scriptlet: oracle-database-free-23ai-1.0-1.x86_64                                                                                                                                                   1/1
[INFO] Executing post installation scripts...
[INFO] Oracle home installed successfully and ready to be configured.
To configure Oracle Database Free, optionally modify the parameters in '/etc/sysconfig/oracle-free-23ai.conf' and then run '/etc/init.d/oracle-free-23ai configure' as root.

  Verifying        : oracle-database-free-23ai-1.0-1.x86_64                                                                                                                                                   1/1

Installed:
  oracle-database-free-23ai-1.0-1.x86_64

Complete!
[root@ol8-vagrant sf_Downloads]# /etc/init.d/oracle-free-23ai configure
Specify a password to be used for database accounts. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9]. Note that the same password will be used for SYS, SYSTEM and PDBADMIN accounts:
Confirm the password:
Configuring Oracle Listener.
Listener configuration failed. Check log '/opt/oracle/cfgtoollogs/netca/netca_configure_out.log' for more details.
[root@ol8-vagrant sf_Downloads]#


[root@ol8-vagrant ~]# vi /opt/oracle/cfgtoollogs/netca/netca_configure_out.log
Netca configuration log

Parsing command line arguments:
    Parameter "orahome" = /opt/oracle/product/23ai/dbhomeFree
    Parameter "instype" = typical
    Parameter "inscomp" = client,oraclenet,javavm,server,ano
    Parameter "insprtcl" = tcp
    Parameter "cfg" = local
    Parameter "authadp" = NO_VALUE
    Parameter "responsefile" = /opt/oracle/product/23ai/dbhomeFree/network/install/netca_typ.rsp
    Parameter "silent" = true
    Parameter "orahnam" = OraHomeFree
    Parameter "listenerparameters" = DEFAULT_SERVICE=FREE
Done parsing command line arguments.
Oracle Net Services Configuration:
Profile configuration complete.
Oracle Net Listener Startup:
No valid IP Address returned for the host ol8-vagrant.
Check the trace file for details: /opt/oracle/cfgtoollogs/netca/trace_OraDBHome23aiFree-2412026AM1146.log
Oracle Net Services configuration failed.  The exit code is 1

[root@ol8-vagrant ~]# vi /opt/oracle/cfgtoollogs/netca/trace_OraDBHome23aiFree-2412026AM1146.log
...
...
...
[main] [ 2024-12-02 06:11:56.032 UTC ] [ConfigureListener.isPortFree:1366]  No IP address returned for host. ol8-vagrant
oracle.net.ca.IllegalEndpointException: No valid IP Address returned for the host ol8-vagrant.
        at oracle.net.ca.ConfigureListener.isPortFree(ConfigureListener.java:1367)
        at oracle.net.ca.ConfigureListener.validatePort(ConfigureListener.java:1256)
        at oracle.net.ca.ConfigureListener.validateEndPoint(ConfigureListener.java:1240)
        at oracle.net.ca.ConfigureListener.typicalConfigure(ConfigureListener.java:307)
        at oracle.net.ca.SilentConfigure.performSilentConfigure(SilentConfigure.java:212)
        at oracle.net.ca.InitialSetup.<init>(NetCA.java:4450)
        at oracle.net.ca.NetCA.main(NetCA.java:491)
[main] [ 2024-12-02 06:11:56.032 UTC ] [ConfigureListener.typicalConfigure:311]  No valid IP Address returned for the host ol8-vagrant.
[main] [ 2024-12-02 06:11:56.032 UTC ] [ConfigureListener.typicalConfigure:326]  Failed to get free port. Using port 1521.
[main] [ 2024-12-02 06:11:56.072 UTC ] [CmdlineArgs.getListenerParameters:1317]  Control parameter loaded: DEFAULT_SERVICE
[main] [ 2024-12-02 06:11:56.075 UTC ] [ConfigureListener.typicalConfigure:366]  DEFAULT_SERVICE FREE
[main] [ 2024-12-02 06:11:56.084 UTC ] [ConfigureListener.isPortFree:1274]  Checking if port 1521 is free on local machine...
[main] [ 2024-12-02 06:11:56.084 UTC ] [ConfigureListener.isPortFree:1289]  InetAddress.getByName(127.0.0.1): /127.0.0.1
[main] [ 2024-12-02 06:11:56.084 UTC ] [ConfigureListener.isPortFree:1291]  Local host IP address: ol8-vagrant/127.0.1.1
[main] [ 2024-12-02 06:11:56.084 UTC ] [ConfigureListener.isPortFree:1293]  Local host name: ol8-vagrant
[main] [ 2024-12-02 06:11:56.084 UTC ] [ConfigureListener.isPortFree:1304]  Address ol8-vagrant
[main] [ 2024-12-02 06:11:56.084 UTC ] [ConfigureListener.isPortFree:1366]  No IP address returned for host. ol8-vagrant
Type  :qa!  and press <Enter> to abandon all changes and exit Vim





Disconnected the VPN and retried to configure the oracle-free-23ai.


[root@ol8-vagrant ~]# /etc/init.d/oracle-free-23ai configure
Specify a password to be used for database accounts. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9]. Note that the same password will be used for SYS, SYSTEM and PDBADMIN accounts:
Confirm the password:
Configuring Oracle Listener.
Listener configuration succeeded.
Configuring Oracle Database FREE.
Enter SYS user password:
************
Enter SYSTEM user password:
*************
Enter PDBADMIN User Password:
*************
Prepare for db operation
7% complete
Copying database files
29% complete
Creating and starting Oracle instance
30% complete
33% complete
36% complete
39% complete
43% complete
Completing Database Creation
47% complete
49% complete
50% complete
Creating Pluggable Databases
54% complete
71% complete
Executing Post Configuration Actions
93% complete
Running Custom Scripts
100% complete
Database creation complete. For details check the logfiles at:
 /opt/oracle/cfgtoollogs/dbca/FREE.
Database Information:
Global Database Name:FREE
System Identifier(SID):FREE
Look at the log file "/opt/oracle/cfgtoollogs/dbca/FREE/FREE.log" for further details.

Connect to Oracle Database using one of the connect strings:
     Pluggable database: ol8-vagrant:1539/FREEPDB1
     Multitenant container database: ol8-vagrant:1539
[root@ol8-vagrant ~]#



[vagrant@ol8-vagrant ~]$ cat /etc/oraInst.loc
inventory_loc=/opt/oracle/oraInventory
inst_group=oinstall
[vagrant@ol8-vagrant ~]$


[root@ol8-vagrant ~]# ps -ef|grep pmon
oracle     24805       1  0 06:44 ?        00:00:01 db_pmon_FREE
root       25605   22435 50 07:20 pts/0    00:00:00 grep --color=auto pmon
[root@ol8-vagrant ~]# cat /etc/oratab
#



# This file is used by ORACLE utilities.  It is created by root.sh
# and updated by either Database Configuration Assistant while creating
# a database or ASM Configuration Assistant while creating ASM instance.

# A colon, ':', is used as the field terminator.  A new line terminates
# the entry.  Lines beginning with a pound sign, '#', are comments.
#
# Entries are of the form:
#   $ORACLE_SID:$ORACLE_HOME:<N|Y>:
#
# The first and second fields are the system identifier and home
# directory of the database respectively.  The third field indicates
# to the dbstart utility that the database should , "Y", or should not,
# "N", be brought up at system boot time.
#
# Multiple entries with the same $ORACLE_SID are not allowed.
#
#
FREE:/opt/oracle/product/23ai/dbhomeFree:N
[root@ol8-vagrant ~]#

[root@ol8-vagrant ~]# id oracle
uid=54321(oracle) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54323(oper),54324(backupdba),54325(dgdba),54326(kmdba),54330(racdba)
[root@ol8-vagrant ~]#


[root@ol8-vagrant FREE]# pwd;ls -ltr
/opt/oracle/oradata/FREE
total 2374476
drwxr-x---. 2 oracle oinstall         85 Dec  2 06:31 pdbseed
-rw-r-----. 1 oracle oinstall   20979712 Dec  2 06:37 temp01.dbf
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 redo02.log
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 redo03.log
-rw-r-----. 1 oracle oinstall    7348224 Dec  2 06:44 users01.dbf
drwxr-x---. 2 oracle oinstall        104 Dec  2 06:46 FREEPDB1
-rw-r-----. 1 oracle oinstall 1080041472 Dec  2 07:19 system01.dbf
-rw-r-----. 1 oracle oinstall   36708352 Dec  2 07:19 undotbs01.dbf
-rw-r-----. 1 oracle oinstall  639639552 Dec  2 07:20 sysaux01.dbf
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:21 control01.ctl
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:21 control02.ctl
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 07:21 redo01.log
[root@ol8-vagrant FREE]# cd FREEPDB1
[root@ol8-vagrant FREEPDB1]# ls -ltr
total 806944
-rw-r-----. 1 oracle oinstall   7348224 Dec  2 06:51 users01.dbf
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 07:01 temp01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 07:21 undotbs01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 07:21 system01.dbf
-rw-r-----. 1 oracle oinstall 419438592 Dec  2 07:21 sysaux01.dbf
[root@ol8-vagrant FREEPDB1]# cd ../pdbseed/
[root@ol8-vagrant pdbseed]# ls -ltr
total 799768
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 06:40 temp01.dbf
-rw-r-----. 1 oracle oinstall 419438592 Dec  2 06:44 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 06:44 system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 06:44 undotbs01.dbf
[root@ol8-vagrant pdbseed]#


[root@ol8-vagrant ~]# su - oracle
[oracle@ol8-vagrant ~]$ sqlplus / as sysdba
-bash: sqlplus: command not found
[oracle@ol8-vagrant ~]$ . oraenv
ORACLE_SID = [oracle] ? FREE
The Oracle base has been set to /opt/oracle
[oracle@ol8-vagrant ~]$ sqlplus / as sysdba

SQL*Plus: Release 23.0.0.0.0 - for Oracle Cloud and Engineered Systems on Mon Dec 2 07:23:29 2024
Version 23.6.0.24.10

Copyright (c) 1982, 2024, Oracle.  All rights reserved.


Connected to:
Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free
Version 23.6.0.24.10

SQL> select banner from v$version;

BANNER
--------------------------------------------------------------------------------
Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free

SQL> sho pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 FREEPDB1                       READ WRITE NO

SQL> !ls -ltr /opt/oracle/oradata/FREE/*/*
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 06:40 /opt/oracle/oradata/FREE/pdbseed/temp01.dbf
-rw-r-----. 1 oracle oinstall 419438592 Dec  2 06:44 /opt/oracle/oradata/FREE/pdbseed/sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 06:44 /opt/oracle/oradata/FREE/pdbseed/system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 06:44 /opt/oracle/oradata/FREE/pdbseed/undotbs01.dbf
-rw-r-----. 1 oracle oinstall   7348224 Dec  2 06:51 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 07:01 /opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf
-rw-r-----. 1 oracle oinstall 429924352 Dec  2 07:26 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 07:26 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 07:26 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         1          1 /opt/oracle/oradata/FREE/system01.dbf                              1030         32768 YES AVAILABLE
         1          3 /opt/oracle/oradata/FREE/sysaux01.dbf                               610         32768 YES AVAILABLE
         1          7 /opt/oracle/oradata/FREE/users01.dbf                                  7         32768 YES AVAILABLE
         1         11 /opt/oracle/oradata/FREE/undotbs01.dbf                               35         32768 YES AVAILABLE
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      410         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                         7         32768 YES AVAILABLE

8 rows selected.

SQL> alter session set container=FREEPDB1;

Session altered.

SQL> alter database datafile '/opt/oracle/oradata/FREE/FREEPDB1/users01.dbf' resize 10m;

Database altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      410         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        10         32768 YES AVAILABLE


SQL> !ls -ltr /opt/oracle/oradata/FREE/*
-rw-r-----. 1 oracle oinstall   20979712 Dec  2 06:37 /opt/oracle/oradata/FREE/temp01.dbf
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 /opt/oracle/oradata/FREE/redo02.log
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 /opt/oracle/oradata/FREE/redo03.log
-rw-r-----. 1 oracle oinstall    7348224 Dec  2 06:44 /opt/oracle/oradata/FREE/users01.dbf
-rw-r-----. 1 oracle oinstall 1080041472 Dec  2 07:19 /opt/oracle/oradata/FREE/system01.dbf
-rw-r-----. 1 oracle oinstall   36708352 Dec  2 07:26 /opt/oracle/oradata/FREE/undotbs01.dbf
-rw-r-----. 1 oracle oinstall  639639552 Dec  2 07:26 /opt/oracle/oradata/FREE/sysaux01.dbf
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 07:30 /opt/oracle/oradata/FREE/redo01.log
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:31 /opt/oracle/oradata/FREE/control01.ctl
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:31 /opt/oracle/oradata/FREE/control02.ctl

/opt/oracle/oradata/FREE/pdbseed:
total 799768
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 06:40 temp01.dbf
-rw-r-----. 1 oracle oinstall 419438592 Dec  2 06:44 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 06:44 system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 06:44 undotbs01.dbf

/opt/oracle/oradata/FREE/FREEPDB1:
total 820256
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 07:01 temp01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 07:26 system01.dbf
-rw-r-----. 1 oracle oinstall 429924352 Dec  2 07:30 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 07:30 undotbs01.dbf
-rw-r-----. 1 oracle oinstall  10493952 Dec  2 07:30 users01.dbf

SQL> alter database datafile '/opt/oracle/oradata/FREE/FREEPDB1/users01.dbf' resize 20m;

Database altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      410         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        20         32768 YES AVAILABLE

SQL> !ls -ltr /opt/oracle/oradata/FREE/*
-rw-r-----. 1 oracle oinstall   20979712 Dec  2 06:37 /opt/oracle/oradata/FREE/temp01.dbf
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 /opt/oracle/oradata/FREE/redo02.log
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 /opt/oracle/oradata/FREE/redo03.log
-rw-r-----. 1 oracle oinstall    7348224 Dec  2 06:44 /opt/oracle/oradata/FREE/users01.dbf
-rw-r-----. 1 oracle oinstall  639639552 Dec  2 07:26 /opt/oracle/oradata/FREE/sysaux01.dbf
-rw-r-----. 1 oracle oinstall 1080041472 Dec  2 07:31 /opt/oracle/oradata/FREE/system01.dbf
-rw-r-----. 1 oracle oinstall   36708352 Dec  2 07:32 /opt/oracle/oradata/FREE/undotbs01.dbf
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 07:32 /opt/oracle/oradata/FREE/redo01.log
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:32 /opt/oracle/oradata/FREE/control01.ctl
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:32 /opt/oracle/oradata/FREE/control02.ctl

/opt/oracle/oradata/FREE/pdbseed:
total 799768
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 06:40 temp01.dbf
-rw-r-----. 1 oracle oinstall 419438592 Dec  2 06:44 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 06:44 system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 06:44 undotbs01.dbf

/opt/oracle/oradata/FREE/FREEPDB1:
total 830496
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 07:01 temp01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 07:26 system01.dbf
-rw-r-----. 1 oracle oinstall 429924352 Dec  2 07:31 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 07:31 undotbs01.dbf
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 07:31 users01.dbf

SQL> alter session set container=CDB$ROOT;

Session altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         1          1 /opt/oracle/oradata/FREE/system01.dbf                              1030         32768 YES AVAILABLE
         1          3 /opt/oracle/oradata/FREE/sysaux01.dbf                               610         32768 YES AVAILABLE
         1          7 /opt/oracle/oradata/FREE/users01.dbf                                  7         32768 YES AVAILABLE
         1         11 /opt/oracle/oradata/FREE/undotbs01.dbf                               35         32768 YES AVAILABLE
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      410         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        20         32768 YES AVAILABLE

8 rows selected.

SQL>


SQL> sho pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 FREEPDB1                       READ WRITE NO

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_temp_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- -------
         1          1 /opt/oracle/oradata/FREE/temp01.dbf                                  20    31.9999847 YES ONLINE
         3          3 /opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf                         20    31.9999847 YES ONLINE

SQL> alter database tempfile '/opt/oracle/oradata/FREE/temp01.dbf' resize 30m;

Database altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_temp_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- -------
         1          1 /opt/oracle/oradata/FREE/temp01.dbf                                  30    31.9999847 YES ONLINE
         3          3 /opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf                         20    31.9999847 YES ONLINE

SQL> alter session set container=FREEPDB1;

Session altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_temp_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- -------
         3          3 /opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf                         20    31.9999847 YES ONLINE

SQL> alter database tempfile '/opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf' resize 40m;

Database altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_temp_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- -------
         3          3 /opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf                         40    31.9999847 YES ONLINE

SQL> alter session set container=CDB$ROOT;

Session altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_temp_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- -------
         1          1 /opt/oracle/oradata/FREE/temp01.dbf                                  30    31.9999847 YES ONLINE
         3          3 /opt/oracle/oradata/FREE/FREEPDB1/temp01.dbf                         40    31.9999847 YES ONLINE

SQL> !ls -ltr /opt/oracle/oradata/FREE/*
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 /opt/oracle/oradata/FREE/redo02.log
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 06:44 /opt/oracle/oradata/FREE/redo03.log
-rw-r-----. 1 oracle oinstall    7348224 Dec  2 06:44 /opt/oracle/oradata/FREE/users01.dbf
-rw-r-----. 1 oracle oinstall   31465472 Dec  2 07:34 /opt/oracle/oradata/FREE/temp01.dbf
-rw-r-----. 1 oracle oinstall   36708352 Dec  2 07:34 /opt/oracle/oradata/FREE/undotbs01.dbf
-rw-r-----. 1 oracle oinstall  639639552 Dec  2 07:34 /opt/oracle/oradata/FREE/sysaux01.dbf
-rw-r-----. 1 oracle oinstall 1080041472 Dec  2 07:34 /opt/oracle/oradata/FREE/system01.dbf
-rw-r-----. 1 oracle oinstall  209715712 Dec  2 07:35 /opt/oracle/oradata/FREE/redo01.log
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:35 /opt/oracle/oradata/FREE/control01.ctl
-rw-r-----. 1 oracle oinstall   18759680 Dec  2 07:35 /opt/oracle/oradata/FREE/control02.ctl

/opt/oracle/oradata/FREE/pdbseed:
total 799768
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 06:40 temp01.dbf
-rw-r-----. 1 oracle oinstall 419438592 Dec  2 06:44 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 06:44 system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 06:44 undotbs01.dbf

/opt/oracle/oradata/FREE/FREEPDB1:
total 830496
-rw-r-----. 1 oracle oinstall 429924352 Dec  2 07:34 sysaux01.dbf
-rw-r-----. 1 oracle oinstall 293609472 Dec  2 07:34 system01.dbf
-rw-r-----. 1 oracle oinstall 104865792 Dec  2 07:34 undotbs01.dbf
-rw-r-----. 1 oracle oinstall  41951232 Dec  2 07:35 temp01.dbf
-rw-r-----. 1 oracle oinstall  20979712 Dec  2 07:35 users01.dbf

SQL>


[root@ol8-vagrant opt]# ls -ltr
total 0
drwxr-xr-x. 3 root   root      28 Oct 25 13:09 rh
drwxr-xr-x. 7 root   root     119 Oct 25 13:11 VBoxGuestAdditions-7.1.4
drwxr-xr-x. 3 root   root      22 Dec  2 06:10 ORCLfmap
drwxr-xr-x. 9 oracle oinstall 113 Dec  2 06:26 oracle
[root@ol8-vagrant opt]# cd ORCLfmap/
[root@ol8-vagrant ORCLfmap]# ls
prot1_64
[root@ol8-vagrant ORCLfmap]# cd prot1_64/
[root@ol8-vagrant prot1_64]# ls
bin  etc  log
[root@ol8-vagrant prot1_64]# cd bin/
[root@ol8-vagrant bin]# ls
fmputl  fmputlhp
[root@ol8-vagrant bin]# cd ../log/
[root@ol8-vagrant log]# ;s
-bash: syntax error near unexpected token `;'
[root@ol8-vagrant log]# ls
[root@ol8-vagrant log]# cd ..
[root@ol8-vagrant prot1_64]# cd ..
[root@ol8-vagrant ORCLfmap]# ls -ltr
total 0
drwxr-xr-x. 5 root root 39 Dec  2 06:10 prot1_64
[root@ol8-vagrant ORCLfmap]# cd ..
[root@ol8-vagrant opt]# cd ..
[root@ol8-vagrant /]# cd opt/
[root@ol8-vagrant opt]# ls -ltr
total 0
drwxr-xr-x. 3 root   root      28 Oct 25 13:09 rh
drwxr-xr-x. 7 root   root     119 Oct 25 13:11 VBoxGuestAdditions-7.1.4
drwxr-xr-x. 3 root   root      22 Dec  2 06:10 ORCLfmap
drwxr-xr-x. 9 oracle oinstall 113 Dec  2 06:26 oracle
[root@ol8-vagrant opt]# cd oracle/
[root@ol8-vagrant oracle]# ls
admin  audit  cfgtoollogs  diag  oradata  oraInventory  product
[root@ol8-vagrant oracle]# ls -ltr
total 4
drwxr-xr-x.  3 oracle oinstall   18 Dec  2 06:03 product
drwxrwxr-x. 25 oracle oinstall 4096 Dec  2 06:10 diag
drwxr-xr-x.  4 oracle oinstall   31 Dec  2 06:26 cfgtoollogs
drwxr-x---.  3 oracle oinstall   18 Dec  2 06:26 oradata
drwxr-x---.  3 oracle oinstall   18 Dec  2 06:26 admin
drwxr-x---.  3 oracle oinstall   18 Dec  2 06:26 audit
drwxrwx---.  4 oracle oinstall   78 Dec  2 06:44 oraInventory
[root@ol8-vagrant oracle]# cd product/
[root@ol8-vagrant product]# ls -ltr
total 0
drwxrwxr-x. 3 oracle oinstall 24 Dec  2 06:03 23ai
[root@ol8-vagrant product]# cd 23ai/
[root@ol8-vagrant 23ai]# ls
dbhomeFree
[root@ol8-vagrant 23ai]# ls -ltr
total 4
drwxrwxr-x. 63 oracle oinstall 4096 Dec  2 06:44 dbhomeFree
[root@ol8-vagrant 23ai]# cd dbhomeFree/
[root@ol8-vagrant dbhomeFree]# ll
total 80
drwxr-xr-x.  2 oracle oinstall   102 Dec  2 06:10 addnode
drwxr-xr-x.  9 oracle oinstall    93 Dec  2 06:05 assistants
drwxr-xr-x.  2 oracle oinstall  8192 Dec  2 06:10 bin
drwxrwx---.  4 oracle oinstall    33 Dec  2 06:31 cfgtoollogs
drwxr-xr-x.  4 oracle oinstall    87 Dec  2 06:10 clone
drwxr-xr-x.  6 oracle oinstall    55 Dec  2 06:06 crs
drwxr-xr-x.  4 oracle oinstall    31 Dec  2 06:06 crypto
drwxr-xr-x.  3 oracle oinstall    18 Dec  2 06:06 css
drwxr-xr-x. 11 oracle oinstall   119 Dec  2 06:06 ctx
drwxr-xr-x.  7 oracle oinstall    71 Dec  2 06:06 cv
drwxr-xr-x.  3 oracle oinstall    20 Dec  2 06:06 data
drwxr-xr-x.  2 oracle oinstall    94 Dec  2 06:44 dbs
drwxr-xr-x.  5 oracle oinstall   173 Dec  2 06:10 deinstall
drwxr-xr-x.  3 oracle oinstall    20 Dec  2 06:06 demo
drwxr-xr-x.  3 oracle oinstall    20 Dec  2 06:06 diagnostics
drwxr-xr-x.  3 oracle oinstall    19 Dec  2 06:06 dv
-rw-r--r--.  1 oracle oinstall   852 Aug 18  2015 env.ora
drwxr-xr-x.  3 oracle oinstall    18 Dec  2 06:06 has
drwxr-xr-x.  5 oracle oinstall    41 Dec  2 06:06 hs
drwxrwx---. 11 oracle oinstall  4096 Dec  2 06:10 install
drwxr-xr-x.  2 oracle oinstall    29 Dec  2 06:10 instantclient
drwxr-x---. 12 oracle oinstall  4096 Dec  2 06:10 inventory
drwxr-xr-x.  9 oracle oinstall    94 Dec  2 06:07 javavm
drwxr-xr-x.  3 oracle oinstall    17 Dec  2 06:07 jdbc
drwxr-xr-x.  6 oracle oinstall    68 Dec  2 06:10 jdk
drwxr-xr-x.  2 oracle oinstall  4096 Dec  2 06:10 jlib
drwxr-xr-x. 10 oracle oinstall   112 Dec  2 06:08 ldap
drwxr-xr-x.  3 oracle oinstall 12288 Dec  2 06:10 lib
-rwxrwxr-x.  1 oracle oinstall  5780 Oct 18 03:13 LICENSE
drwxrwxr-x.  4 oracle oinstall    37 Dec  2 06:27 log
drwxr-xr-x.  5 oracle oinstall    42 Dec  2 06:09 md
drwxr-xr-x.  4 oracle oinstall    31 Dec  2 06:09 mgw
drwxr-xr-x. 11 oracle oinstall   118 Dec  2 06:09 network
drwxr-xr-x.  5 oracle oinstall    46 Dec  2 06:09 nls
drwxr-xr-x.  8 oracle oinstall   133 Dec  2 06:10 odbc
drwxr-xr-x.  5 oracle oinstall    42 Dec  2 06:09 olap
drwxr-xr-x.  4 oracle oinstall    35 Dec  2 06:09 oml4py
drwxr-xr-x. 13 oracle oinstall  4096 Dec  2 06:10 OPatch
drwxr-xr-x.  7 oracle oinstall    65 Dec  2 06:09 opmn
drwxr-xr-x.  5 oracle oinstall    45 Dec  2 06:09 oracore
-rw-r-----.  1 oracle oinstall   130 Dec  2 06:10 oraInst.loc
drwxr-xr-x.  4 oracle oinstall    29 Dec  2 06:09 ord
drwxr-xr-x.  3 oracle oinstall    19 Dec  2 06:09 oss
drwxr-xr-x.  8 oracle oinstall  4096 Dec  2 06:10 oui
drwxr-xr-x.  5 oracle oinstall    39 Dec  2 06:09 perl
drwxr-xr-x.  6 oracle oinstall   106 Dec  2 06:10 plsql
drwxr-xr-x.  7 oracle oinstall    88 Dec  2 06:10 precomp
drwxr-xr-x.  5 oracle oinstall    39 Dec  2 06:09 python
drwxr-xr-x.  2 oracle oinstall    26 Dec  2 06:10 QOpatch
drwxr-xr-x.  5 oracle oinstall    52 Dec  2 06:03 R
drwxr-xr-x.  4 oracle oinstall    29 Dec  2 06:09 racg
drwxr-xr-x. 13 oracle oinstall   140 Dec  2 06:10 rdbms
drwxr-xr-x.  3 oracle oinstall    21 Dec  2 06:10 relnotes
-rwx------.  1 oracle oinstall   525 Oct 18 03:12 root.sh
-rwxr-x---.  1 oracle oinstall  2957 Jun  7 09:10 runInstaller
-rw-r--r--.  1 oracle oinstall  2927 Jul 20  2020 schagent.conf
drwxr-xr-x.  5 oracle oinstall   119 Dec  2 06:10 sdk
drwxr-xr-x.  3 oracle oinstall    18 Dec  2 06:10 slax
drwxr-xr-x.  4 oracle oinstall    28 Dec  2 06:10 sqlcl
drwxr-xr-x.  3 oracle oinstall    17 Dec  2 06:10 sqlj
drwxr-xr-x.  3 oracle oinstall  4096 Dec  2 06:10 sqlpatch
drwxr-xr-x.  6 oracle oinstall    53 Dec  2 06:10 sqlplus
drwxr-xr-x.  6 oracle oinstall    54 Dec  2 06:10 srvm
drwxr-xr-x.  3 oracle oinstall    17 Dec  2 06:10 ucp
drwxr-xr-x.  4 oracle oinstall    31 Dec  2 06:10 usm
drwxr-xr-x.  2 oracle oinstall    33 Dec  2 06:10 utl
drwxr-x---.  7 oracle oinstall    69 Dec  2 06:10 xdk
[root@ol8-vagrant dbhomeFree]#



SQL> alter session set container=FREEPDB1;

Session altered.

SQL> sho pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         3 FREEPDB1                       READ WRITE NO
SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      410         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        20         32768 YES AVAILABLE

SQL>
SQL> sho parameter db_block_size

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
db_block_size                        integer     8192
SQL>
SQL> select 10*8192 "10 blks in bytes: from dual;
ERROR:
ORA-01740: missing double quote in identifier
Help: https://docs.oracle.com/error-help/db/ora-01740/


SQL> select 10*8192 "10 blks in bytes" from dual;

10 blks in bytes
----------------
           81920

SQL> select "How many blocks equal to 20m" from dual;
select "How many blocks equal to 20m" from dual
       *
ERROR at line 1:
ORA-00904: "How many blocks equal to 20m": invalid identifier
Help: https://docs.oracle.com/error-help/db/ora-00904/


SQL> select 20*1024*1024 from dual;

20*1024*1024
------------
    20971520

SQL> #1 block is 8192 bytes
SQL>
SQL> select 20971520/8192 "20m equals to bls?" from dual;

20m equals to bls?
------------------
              2560

SQL>
SQL> select (2560*8192)/1024/1024 from dual;

(2560*8192)/1024/1024
---------------------
                   20

SQL>
SQL> create user u1 identified by u1;

User created.

SQL> grant create session,create table to u1;

Grant succeeded.

SQL> conn u1/u1
ERROR:
ORA-01017: invalid credential or not authorized; logon denied
Help: https://docs.oracle.com/error-help/db/ora-01017/


Warning: You are no longer connected to ORACLE.
SQL> conn u1
Enter password:
ERROR:
ORA-01017: invalid credential or not authorized; logon denied
Help: https://docs.oracle.com/error-help/db/ora-01017/


SQL>
venkavar@VENKAVAR-CPJ7J64 MINGW64 ~/github/vagrant-projects/OracleLinux/8 (main)
$ vagrant ssh

Welcome to Oracle Linux Server release 8.10 (GNU/Linux 5.15.0-206.153.7.el8uek.x86_64)

The Oracle Linux End-User License Agreement can be viewed here:

  * /usr/share/eula/eula.en_US

For additional packages, updates, documentation and community help, see:

  * https://yum.oracle.com/

Last login: Mon Dec  2 07:57:49 2024 from 10.0.2.2
[vagrant@ol8-vagrant ~]$ sudo -u root -i
[root@ol8-vagrant ~]# passwd oracle
Changing password for user oracle.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
[root@ol8-vagrant ~]# logout
[vagrant@ol8-vagrant ~]$ su - oracle
Password:
[oracle@ol8-vagrant ~]$ ps -ef|grep pmon
oracle     24805       1  0 06:44 ?        00:00:03 db_pmon_FREE
oracle     26362   26319  0 07:59 pts/0    00:00:00 grep --color=auto pmon
[oracle@ol8-vagrant ~]$ . oraenv
ORACLE_SID = [oracle] ? FREE
The Oracle base has been set to /opt/oracle
[oracle@ol8-vagrant ~]$ sqlplus / as sysdba

SQL*Plus: Release 23.0.0.0.0 - for Oracle Cloud and Engineered Systems on Mon Dec 2 07:59:14 2024
Version 23.6.0.24.10

Copyright (c) 1982, 2024, Oracle.  All rights reserved.


Connected to:
Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free
Version 23.6.0.24.10

SQL>


SQL> select con_id,TABLESPACE_NAME,BIGFILE from cdb_tablespaces order by 1,2;

    CON_ID TABLESPACE_NAME                BIG
---------- ------------------------------ ---
         1 SYSAUX                         YES
         1 SYSTEM                         YES
         1 TEMP                           NO
         1 UNDOTBS1                       YES
         1 USERS                          YES
         3 SYSAUX                         YES
         3 SYSTEM                         YES
         3 TEMP                           NO
         3 UNDOTBS1                       YES
         3 USERS                          YES

10 rows selected.

SQL>
SQL> col BANNER for a45
SQL> col BANNER_FULL for a45
SQL> col BANNER_LEGACY for a45
SQL> select * from v$version;

BANNER                                        BANNER_FULL                                   BANNER_LEGACY                                     CON_ID
--------------------------------------------- --------------------------------------------- --------------------------------------------- ----------
Oracle Database 23ai Free Release 23.0.0.0.0  Oracle Database 23ai Free Release 23.0.0.0.0  Oracle Database 23ai Free Release 23.0.0.0.0           0
- Develop, Learn, and Run for Free            - Develop, Learn, and Run for Free            - Develop, Learn, and Run for Free
                                              Version 23.6.0.24.10


SQL> sho pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 FREEPDB1                       READ WRITE NO
SQL> alter session set container=FREEPDB1;

Session altered.

SQL> select con_id,TABLESPACE_NAME,BIGFILE from cdb_tablespaces order by 1,2;

    CON_ID TABLESPACE_NAME                BIG
---------- ------------------------------ ---
         3 SYSAUX                         YES
         3 SYSTEM                         YES
         3 TEMP                           NO
         3 UNDOTBS1                       YES
         3 USERS                          YES
		 
SQL> col file_name for a60
SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      420         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        20         32768 YES AVAILABLE

SQL> alter tablespace USERS add datafile '/opt/oracle/oradata/FREE/FREEPDB1/users02.dbf' size 10m autoextend on maxsize 32768m;
alter tablespace USERS add datafile '/opt/oracle/oradata/FREE/FREEPDB1/users02.dbf' size 10m autoextend on maxsize 32768m
*
ERROR at line 1:
ORA-32771: cannot add file to bigfile tablespace
Help: https://docs.oracle.com/error-help/db/ora-32771/

SQL> alter database datafile '/opt/oracle/oradata/FREE/FREEPDB1/users01.dbf' resize 25m;

Database altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      420         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        25         32768 YES AVAILABLE

SQL>
SQL> create tablespace customer datafile '/opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf' size 4m autoextend on maxsize 32768m;
create tablespace customer datafile '/opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf' size 4m autoextend on maxsize 32768m
*
ERROR at line 1:
ORA-03214: The specified file size is smaller than the minimum blocks 784.
Help: https://docs.oracle.com/error-help/db/ora-03214/


SQL> select 784*8192 from dual;

  784*8192
----------
   6422528

SQL> select 6422528/1024/1024 from dual;

6422528/1024/1024
-----------------
            6.125

SQL> create tablespace customer datafile '/opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf' siz 6422528 autoextend on maxsize 32768m;
create tablespace customer datafile '/opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf' siz 6422528 autoextend on maxsize 32768m
                                                                                       *
ERROR at line 1:
ORA-02180: invalid option for CREATE TABLESPACE
Help: https://docs.oracle.com/error-help/db/ora-02180/


SQL>  create tablespace customer datafile '/opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf' size 6422528 autoextend on maxsize 32768m;

Tablespace created.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      420         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        25         32768 YES AVAILABLE
         3         16 /opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf                  6.125            32 YES AVAILABLE

SQL> select con_id,TABLESPACE_NAME,BIGFILE from cdb_tablespaces order by 1,2;

    CON_ID TABLESPACE_NAME                BIG
---------- ------------------------------ ---
         3 CUSTOMER                       YES
         3 SYSAUX                         YES
         3 SYSTEM                         YES
         3 TEMP                           NO
         3 UNDOTBS1                       YES
         3 USERS                          YES

6 rows selected.

SQL>
SQL>  alter database datafile '/opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf' resize 7m;

Database altered.

SQL> select con_id,file_id,file_name,bytes/1024/1024 "Size IN MB",maxbytes/1024/1024/1024 "MaxSize IN GB",autoextensible,status from cdb_data_files order by 1,2;

    CON_ID    FILE_ID FILE_NAME                                                    Size IN MB MaxSize IN GB AUT STATUS
---------- ---------- ------------------------------------------------------------ ---------- ------------- --- ---------
         3         12 /opt/oracle/oradata/FREE/FREEPDB1/system01.dbf                      280         32768 YES AVAILABLE
         3         13 /opt/oracle/oradata/FREE/FREEPDB1/sysaux01.dbf                      420         32768 YES AVAILABLE
         3         14 /opt/oracle/oradata/FREE/FREEPDB1/undotbs01.dbf                     100         32768 YES AVAILABLE
         3         15 /opt/oracle/oradata/FREE/FREEPDB1/users01.dbf                        25         32768 YES AVAILABLE
         3         16 /opt/oracle/oradata/FREE/FREEPDB1/customer01.dbf                      7            32 YES AVAILABLE

SQL>

