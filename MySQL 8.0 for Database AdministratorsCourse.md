# MySQL 8.0 for Database AdministratorsCourse

---

# Installation and Upgrading

### MySQL Installation - Key Steps

* **Platform Check:** Verify MySQL support for your operating system.
* **Distribution Selection:** Choose a suitable package (pre-compiled binaries like RPM, PKG, MSI, or generic archives like ZIP, TAR.gz; or source code).
* **Download:** Obtain the selected distribution.
* **Installation:** Install the downloaded package.
* **Post-Install Configuration:** Perform any necessary setup after installation.

### Installing MySQL from Downloaded Packages

* After you download MySQL Linux packages, install them by using the following commands:
    * On RPM systems:
        ```bash
        rpm -ivh packagename.rpm
        ```
    * On APT systems:
        ```bash
        dpkg -i packagename.deb
        ```
* You must identify and resolve dependencies when you install packages.
    * Install any dependencies before you install MySQL packages.
        * For example, MySQL has a dependency on the `libaio` library. Data directory initialization and subsequent server startup steps will fail if this library is not installed.
    * Install MySQL packages in the correct order.
        * For example, install the `libs` package before installing `client` or `server`.

### MySQL RPM Installation Files for Linux

![alt text](image-1.png)

### MySQL RPM Installation Files for Linux - Package Descriptions

* **server:** Core MySQL Server daemon (`mysqld`) and server utilities.
* **common:** Shared files and configuration templates for various MySQL components.
* **client:** MySQL client programs (e.g., `mysql` command-line client).
* **devel:** Header files and libraries for developing MySQL client applications.
* **embedded-compat:** Compatibility libraries for embedded MySQL server versions.
* **libs:** Core client libraries used by applications to connect to the server.
* **libs-compat:** Compatibility libraries for older MySQL client library versions.
* **test:** Test suites and files for MySQL installation testing.
* **router:** MySQL Router for transparent routing between applications and servers.
* **backup:** Utilities and scripts for performing MySQL database backups.

**Important Notes:**

* Some packages are **Distribution-Independent**, while others are **Distribution-Specific**.
* Pay attention to **dependencies**. For example, install `libs` before `client` or `server`.
* For a basic setup, you'll typically need `server`, `client`, and `libs`. Install other packages based on your specific requirements.
* Always consult the official MySQL documentation for your specific version and Linux distribution for the most accurate information.

### MySQL RPM Installation Process

* The RPM installation performs the following tasks:
    * Extracts RPM files to their default locations.
    * Registers SysV init or systemd startup scripts.
    * Sets up the `mysql` user and group in the operating system.
        * The MySQL server process runs as the `mysql` user.
* When you start the service for the first time using `service mysqld start` or `systemctl start mysqld`, MySQL:
    * Creates the data directory and the default `my.cnf` file.
        * These files are owned by the `mysql` user and group.
    * Creates the default `root@localhost` account.
    * Sets up a random temporary password for the `root` account and writes that password to the error log file (`/var/log/mysqld.log`).
        * **You must change the password before you can use MySQL.**


### MySQL DEB Installation

* DEB packages are available for APT Linux systems, either individually or bundled.
* For a standard installation, install the following packages in the specified order:
    1. The database common files package
    2. The client package
    3. The client metapackage
    4. The server package
    5. The server metapackage

```bash
sudo dpkg -i mysql-{common,community-client,client,community-server,server}_*.deb
```

### Linux Distribution-Specific Repositories

* Many Linux distributions maintain their own package repositories.
    * Hosted on the web or on a local filesystem.
    * Accessed by using package managers.
        * The repository website is specified in the package manager configuration on each host.
        * You can download individual packages manually.
* Contain software packages and their dependencies.
* Supplemented by additional repositories that contain software not contained in the standard package repositories.
    * You can add these additional repositories to the package manager configuration on each host.
* Example: `http://public-yum.oracle.com/` contains Oracle Linux packages.

### Installing MySQL by Using a Package Manager

On RPM-based systems, including Oracle Linux, Red Hat, Fedora, and CentOS, use `yum install`.
```bash
yum install mysql-community-server
```
```bash
yum install mysql-workbench
```

On APT-based systems, including Ubuntu and Debian, use `apt-get install`:
```bash
apt-get install mysql-community-server
```
```bash
apt-get install mysql-workbench
```
> Installing the `mysql-community-server` packages also installs the packages for the components the server requires.

### Adding a Yum Repository for MySQL

* Download the Yum repository RPM file from `http://dev.mysql.com/downloads/repo/yum/`.
    * Choose the correct RPM for your distribution.
    * Example: The "Red Hat Enterprise Linux 7 / Oracle Linux 7 (Architecture Independent), RPM Package" is called `mysql80-community-release-el7-3.noarch.rpm`.

* Install the file by using the `yum localinstall` command, for example:
    ```bash
    yum localinstall mysql80-community-release-el7-3.noarch.rpm
    ```
    * The preceding command adds the MySQL Yum repository to the host's Yum configuration.

* Enable or disable specific versions.
    * MySQL 8.0 is enabled by default. Other versions are disabled.

* Run `yum install packagename` to install a package from the new repository.

