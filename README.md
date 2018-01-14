## Building UltraNote Wallet

### On *nix:

Dependencies: GCC 4.7.3 or later, CMake 3.1 or later, Boost 1.55 or later, and Qt 5.9 or later.

You may download them from:

- http://gcc.gnu.org/
- http://www.cmake.org/
- http://www.boost.org/
- https://www.qt.io

Alternatively, it may be possible to install them using a package manager.

To acquire the source via git and build the release version, run the following commands:
```
cd ~
git clone https://github.com/UltraNote/UltraNoteWallet.git
cd UltraNoteWallet
git submodule init
git submodule update --remote
make
```

You find the executable in the `build/release` directory.
For a faster build, you can add -jX to the end of the make instruction, where X is the number of threads to use. Example: `make -j8`, for 4 cores with 2 threads each.
You may also want to run `make clean` after to remove the build files, which are all stored under the build directory.

If you need to build with a specific Qt version or your Qt is installed in a non-standard path you may specify the location like so:
```
# when using the Makefile wrapper
make QT5_ROOT_PATH=~/Qt/5.10.0/clang_64/

# or when you use cmake directly
cmake -DQT5_ROOT_PATH=~/Qt/5.10.0/clang_64/
```

### On Windows:
Dependencies: MSVC 2013 or later, CMake 3.1 or later, and Boost 1.55, and Qt 5.9 or later. You may download them from:

- http://www.microsoft.com/
- http://www.cmake.org/
- http://www.boost.org/
- https://www.qt.io

To build run one of the following commands:
```
# for 64bit builds
make WINDOWS_BUILD=Win64

# for 32bit builds
make WINDOWS_BUILD=Win32

# to select a specific Visual Studio version
make WINDOWS_BUILD="Visual Studio 14 2015"
```

And then open and build the generated project file, located in the build/release directory, with Visual Studio. To use a different Visual Studio version, specify it's full name instead. Default Windows build use Visual Studio 14 2015. It may also be possible to build with other compilers, like MinGW.

## Building Packages:
To build a DEB file, from the directory with this file, run:
```
make package-deb
```

To build an RPM file, from the directory with this file, run:
```
make package-rpm
```

To build an OS X DMG, from the directory with this file, run:
```
make package-dmg
```


Good luck!
