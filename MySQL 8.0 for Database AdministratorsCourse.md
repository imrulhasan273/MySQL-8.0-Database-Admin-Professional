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

