# Build Requirements

## gcc 
  
Or clang, or any gcc option compatible compiler.

The build system uses the cc command, which is usually the systems default compiler.

You can change compilers at build time if needed by using: 

```
(full make command) CC=compiler
```


## nasm  

If your using MAC, use the newer version from MAC ports.

## make  

Or gmake depending on platform, see below.
	
	
**Note:** The build is compatible with the yasm assembler,  so if you have it installed and want to use it instead;

Use: 

```
(full make command) AS=yasm
```
	  

# Supported Platforms


The build system will auto detect your platform and build the library and examples appropriately for it.
Supported platforms are:

  
* Linux  (Ubuntu, Debian and CentOS Tested so far)
* Windows (Ubuntu Linux Sub-System for Windows, on Windows 10)
* Darwin (MacOS)
* Cygwin (Windows)
* FreeBSD
* NetBSD
* OpenBSD
* GhostBSD
  
# gmake Workaround on BSD platforms

You will need to install 'gmake' (GNU Make) and use it instead of 'make' on these platforms:

* FreeBSD
* NetBSD
* OpenBSD
* GhostBSD
	
This is because these platforms use BSD make, which in some aspects is incompatible with GNU make
if you just use the systems default **'make'** command on these platforms, you will get a lot of make
syntax errors.
	
# Building The Library

To build the library by itself, just run this in the source directory:

```bash
make
```


## Clean the library by itself

```bash
make clean
```


## Install the library (On Cygwin, you do not need sudo)


```bash
sudo make install
```



The following are installed:


```

(Library object) -> /usr/lib/libasm_io.a

(Main header)    -> /usr/local/include/libasm_io.inc

(Platform Specific macros and defines) -> 
	/usr/local/include/libasm_io_cdecl.inc
	/usr/local/include/libasm_io_libc_call.inc
	/usr/local/include/libasm_io_defines.inc

```


## Build the library with all examples


```bash
make examples
```


**Note:** The executable for each compiled example is located at **"examples/{example name}/bin/main"** 
in the examples folder under the top directory of **libasm_io**.


## Clean the examples

```bash
make clean_examples
```


## Clean the library and the examples

```bash
make clean_all
```


# Build with pake

install python3.5+, python3-pip, nasm and gcc.

install pake:

`sudo pip3 install python-pake --upgrade`

change to the root directory.

`pake -ti` lists all documented targets:

```

# Default Tasks

build_library

# Documented Tasks

clean_examples:  Clean the library examples.
clean:           Clean the library
build_examples:  Build all of the library examples
clean_all:       Clean the library and library examples.
build_library:   Build the library.


```

Running `pake` will run the default target **"build_library"**.

Running `pake build_examples` will build the library and examples together.


You can also specify a compiler or nasm compatible assembler using pake defines:

`pake -D CC=clang -D AS=(your assembler)`


# Note About -fPIC

You may need to force compilation with **-fPIC** to prevent errors if
**./platform.sh** does not guess it correctly.

If you encounter an **-fPIC** related linker error when building the examples
you can get around it with:

```

make clean_all
make examples FPIC=true

```

or:

```

pake clean_all
pake build_examples -D FPIC

```





