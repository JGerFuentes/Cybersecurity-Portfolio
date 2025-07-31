## tar and gzip
These file types refer to an ___archive of files___, they contain many files inside of them, but they come in this very neat single file known as a ___tar archive___ or a ___gzip archive___.

### Compressing files with **gzip**

**gzip** is program used to compress files in Linux. These files then end in a ***.gz*** extension.

- The command to ***compress*** a file down is:
    ```
    gzip myFile
    ```

- And the command to ***decompress*** it is:
    ```
    gunzip myFile.gz
    ```

### Creating archives with **tar**
Unfortunately, gzip can't add multiple files into one archive for us. Luckily we have the tar program which does. When you create an archive using **tar**, it will have a ***.tar*** extension.
```
$ tar cvf myTarFile.tar myFile1 myFile2
```

>- **c**: create.
>- **v**: tell the program to be verbose and let us see what it's doing.
>- **f**: the filename of the tar file has to come after this option, if you are creating a tar file you'll have to come up with a name.

### Unpacking archives with **tar**
The command used to extract the contents of a tar file is:
```
tar xvf myTarFile.tar
```

>- **x**: extract.
>- **v**: tell the program to be verbose and let us see what it's doing.
>- **f**: the filename you want to extract.

### Compressing/uncompressing archives with **tar** and **gzip**
Many times you'll see a ***tar*** file that has been compressed such as: *myCompressedArchive.tar.gz*. 

All you need to do is work outside in, so first remove the compression with ***gunzip*** and then you can unpack the tar file. Or you can alternatively use the "**z**" option with ***tar***, which just tells it to use the *gzip* or *gunzip* utility.

#### Create a compressed **tar** file
```
tar czf myCompressedFile.tar.gz
```

#### Uncompressed and unpack with **tar**
```
tar xzf myCompressedFile.tar.gz
```

---

## Package management tools: ***dpkg*** and ***rpm***

Just like *.exe* is a single executable file, so is *.deb* and *.rpm*. These are popular formats of downloaded packages. They are exclusive to their distributions: ***.deb* for Debian** based and ***.rpm* for Red Hat** based.

###  **dpkg**: The mechanic of local packages
> - It works directly with the ***.deb*** files.
> - Doesn't download anything from the Internet.
> - It can only **install**, **remove** or **check for** packages that are already installed in our system or that we manually indicate it to.

**Example:**
```
sudo dpkg -i my_deb_package.deb     # Installs a .deb file locally.

dpkg -l     # Lists all installed packages.

dpkg -L some_package      # Lists the package's files.
```

#### Installing a package
```
Debian: $ dpkg -i my_deb_package.deb

Red Hat: $ rpm -i some_rpm_package.rpm
```
The **i** stands for *install* (**--install**).

#### Removing a package
```
Debian: $ dpkg -r a_deb_package.deb

Red Hat: $ rpm -e some_rpm_package.rpm
```
Here, **r** stands for *remove* and **e** stands for *erase*.

#### Listing installed packages
```
Debian: $dpkg -l

Red Hat: $ rpm -qa
```
In this case, **l** stands for *list* and **q** stands for *query* and **a** for *all*.

---

## Package management systems: ***apt*** and ***yum***

***Apt* is exclusive to the Debian** family and ***yum* is exclusive to the Red Hat** family.

### apt: The complete manager, connected to the Internet
> - It uses ***dpkg*** underneath.
> - It checks for remote repositories.
> - Resolves dependencies automatically.

**Example:**
```
sudo apt update     # Updates the available packages list.

sudo apt install some_package     # Downloads and installs the package and its dependencies.

sudo apt remove some_package        # Removes the package.
```

#### Installing a package from a repository
```
Debian: $ apt install my_package_name

Red hat: $ yum install my_package_name
```

#### Removing a package
```
Debian: $ apt remove my_package_name

Red Hat: $ yum erase my_package_name
```

---
### Updating packages of a repository
In Linux, programs are installed from repositories (lists of available software that your system knows about). These lists don't automatically update themselves, they live locally on your computer and may become outdated if you don't synchronize them. Therefore, it's always a good practice to:
> ***update the local package database before installing or upgrading something***.

```
Debian: $ sudo apt update && sudo apt upgrade

Red Hat: $ yum update
```
> Which means:
>- **update**: Updates de list of available packages.
>- **upgrade**: Installs the pending updates

---
> Una analogía simple
>
> - **dpkg** es como un **instalador manual de paquetes *.deb***, como un doble clic en Windows.
>
> - **apt** es como una **tienda de aplicaciones**, *como Play Store*: sirve para **buscar, instalar, actualizar, desinstalar y resolver lo necesario para que todo funcione**.
---

#### Getting information about an installed package
```
Debian: $ apt show my_package_name

Red Hat: $ yum info my_package_name
```
> **If you want to see information about which repositories your system is using, you can use:**
    ```
    $ dpkg -l
    ```

---

## Compile Source Code
Often times you will encounter packages that only come in form of pure source code. You'll need to use a few commands to get that source code package compiled and installed on your system.

- First, you'll need to have some software to install the tools that will allow you to compile it.
    ```
    $ sudo apt install build-essential
    ```

- Once you do that, extract the contents of the package file (most likely a *.tar.gz* file)
    ```
    $ tar -xzvf my_package.tar.gz
    ```

> Before you do anything, take a look at the README or INSTALL file inside the package. Sometimes there will be specific installation instructions.

- Next, use the **checkinstall** command.
    ```
    $ sudo checkinstall
    ```
    This will *"make install"* and build a ***.deb*** package and install it (build the software and copy the correct files to the correct locations on your computer). It makes it easier and more secure to remove the package later on.
