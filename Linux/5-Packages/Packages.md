## tar and gzip
These file types refer to an ___archive of files___, they contain many files inside of them, but they come in this very neat single file known as a ___tar archive___ or a ___gzip archive___.

### Compressing files with **gzip**

**gzip** is program used to compress files in Linux, they end in a ***.gz*** extension.

The command to compress a file down is:
```
gzip myFile
```

And the command to decompress it is:
```
gunzip myFile.gz
```

### Creating archives with **tar**
Unfortunately, gzip can't add multiple files into one archive for us. Luckily we have the tar program which does. When you create an archive using tar, it will have a ***.tar*** extension.
```
$ tar cvf myTarFile.tar myFile1 myFile2
```

- **c**: create.
- **v**: tell the program to be verbose and let us see what it's doing.
- **f**: the filename of the tar file has to come after this option, if you are creating a tar file you'll have to come up with a name.

### Unpacking archives with **tar**
The command used to extract the contents of a tar file is:
```
tar xvf myTarFile.tar
```

- **x**: extract.
- **v**: tell the program to be verbose and let us see what it's doing.
- **f**: the filename you want to extract.

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
