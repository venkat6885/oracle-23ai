Oracle 23ai free installation on Oracle Linux 8

1. Downloaded Oracle Virtual Box 7.0.22
2. Pre-requisites to install Oracle Virtual Box are Microsoft Visual C++ Redistributable version 19, Python, pywin32.
3. Microsoft Visual C++ Redistributable latest supported downloads location at https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170
4. Install Python and pywin32 (pip install pywin32) to fix the missing dependencies.
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

All tablespaces in oracle database 23ai are bigfile tablespaces, except temp tablespace.

The minimum datafile size needs to be 784 blocks i.e. 6.25 MB.

The tablespaces created under root container are SYSTEM, SYSAUX, USERS, UNDOTBS1, TEMP.

The tablespaces created under seed container are SYSTEM, SYSAUX, UNDOTBS1, TEMP.

PDB has its own  SYSTEM, SYSAUX, USERS, UNDOTBS1, TEMP.
