Oracle 23ai free installation on Oracle Linux 8

1. Downloaded Oracle Virtual Box 7.0.22
2. Pre-requisites to install Oracle Virtual Box are Microsoft Visual C++ Redistributable version 19, Python, pywin32.
3. Microsoft Visual C++ Redistributable latest supported downloads location at https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170
4. Install Python and pywin32 (pip install pywin32) to fix the below missing dependencies.
5. Install Oracle Virtual Box 7.0.22
6. Install Oracle Linux 8 using git repo https://github.com/oracle/vagrant-projects/tree/main/OracleLinux/8. You can browse https://github.com/Oracle for all the repositories.
7. You can follow steps 1-6 mentioned at https://github.com/oracle/vagrant-projects/tree/main/OracleLinux/8, ensure vagarnt is installed on your system.
8. Once OEL 8 is ready, install Oracle Database 23ai Free on Linux.

Download and follw steps in https://www.oracle.com/in/database/free/get-started/ at "Enterprise Linux 8".
https://www.oracle.com/in/database/technologies/oracle-database-software-downloads.html#db_free

	oracle-database-preinstall-23ai-1.0-2.el8.x86_64.rpm
	oracle-database-free-23ai-1.0-1.el8.x86_64.rpm

Execute below commands as root user on Linux 8 that Installs and creates Oracle database.

dnf install -y oracle-database-preinstall*
dnf install -y oracle-database-free*
/etc/init.d/oracle-free-23ai configure

Oracel 23ai new features are

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
[root@ol8-vagrant sf_Downloads]# ll *database*
-rwxrwx---. 1 root vboxsf 1379391728 Nov 30 06:09 oracle-database-free-23ai-1.0-1.el8.x86_64.rpm
-rwxrwx---. 1 root vboxsf      31152 Dec  2 05:54 oracle-database-preinstall-23ai-1.0-2.el8.x86_64.rpm
[root@ol8-vagrant sf_Downloads]#
[root@ol8-vagrant sf_Downloads]#
[root@ol8-vagrant sf_Downloads]# rpm -qa|grep -i preinstall
[root@ol8-vagrant sf_Downloads]# dnf install -y oracle-database-preinstall*
...
...
Complete!
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

