## Building UltraNote Wallet

### On Linux

Dependencies: GCC 4.7.3 or later, CMake 3.9 or later, Boost 1.55 or later, and Qt 5.9 or later.

You may download them from here:

- https://gcc.gnu.org/
- https://www.cmake.org/
- https://www.boost.org/
- https://www.qt.io

or install them using your distribution's package manager.

Clone the source repository with git and build the release version with the following commands:
```
git clone https://github.com/xun-project/UltraNoteWallet.git
cd UltraNoteWallet
git submodule init
git submodule update
make package-deb
```

The top-level Makefile is actually a wrapper for cmake. To use cmake directly, call
```
mkdir -p build/release
cd build/release
cmake -DCMAKE_BUILD_TYPE=Release ../..
make -j4
make package-deb
```

You can find the executable and the DEB package under `build/release`.

### On OSX

Install dependencies with Homebrew:

```
brew install cmake qt
git clone https://github.com/xun-project/UltraNoteWallet.git
cd UltraNoteWallet
git submodule init
git submodule update
make -j4
```

Qt 5.10 installed via Homebrew is difficult to bundle with an application. If you care about shipping UltraNoteWallet as DMG image for install on a different system, download QT from https://qt.io and run the following command instead:

```
# when using the Makefile wrapper
make QT5_ROOT_PATH=~/Qt/5.10.0/clang_64/

# or when you use cmake directly
cd build/release
cmake -DQT5_ROOT_PATH=~/Qt/5.10.0/clang_64/ ../..
make -j4
```

Set `QT5_ROOT_PATH` to the directory where you have installed Qt .


To build an OS X DMG image for distribution, run from either top-level or `build/release`:
```
make package-dmg
```

Note that the distributed app will not be signed and users who install it will have to explicitly allow the app to run at first start via `System Preferences > Security & Privacy`.

### On Windows:

Note that the Windows packages are not signed.

First install all dependencies:
* MSVC 2013 or later from https://www.microsoft.com/
* CMake 3.9 or later from https://www.cmake.org/
* Boost 1.55 or later from https://www.boost.org/
* Qt 5.9 or later from https://www.qt.io
* Git 2.16 or later from https://git-scm.com/download/win
* (optional) NSIS from http://nsis.sourceforge.net/Download

Install with Git Bash and OpenSSL support to make the following commands work. Start a Git Bash terminal (yes, the forward slashes in paths are correct). To build run the following commands and make sure you change the paths to match your installed versions:

```
# fetch sources
git clone https://github.com/xun-project/UltraNoteWallet.git
cd UltraNoteWallet
git submodule init
git submodule update

# prepare build
mkdir -p build/release
export VCINSTALLDIR=/C/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/

# build
cd build/release
cmake -DCMAKE_BUILD_TYPE=Release -DQT5_ROOT_PATH=C/Qt/5.9.2/msvc2015 -G "Visual Studio 15 2017 Win64" ../..
cmake --build . --config Release
cpack -C Release
```

Alternatively you can use the Visual Studio GUI for building. To do so, run just the first cmake command above from the command line, then open the generated file `build/release/UltraNoteWallet.sln` in Visual Studio. Select build type 'Release' and build the target 'UltraNoteWallet' or for a distribution package build target 'PACKAGE'.

**Critical note when you intend to distribute UltraNoteWallet:** QT5 up to version 5.9.2 contains a bug that prevents us from embedding the MSVC redistributable DLLs into the target package when built with Visual Studio. You must globally set the environment variable `VCINSTALLDIR` before you start Visual Studio. Alternatively you must distribute `vcredist_x86.exe` for 32bit or `vcredist_x64.exe` for Win64 separately.


The above commands use cmake directly. If you happen to have `make` installed on your system a more convenient method is to call the following command from the repo top-level directory:

```
# for 64bit builds
make WINDOWS_BUILD=Win64 QT5_ROOT_PATH=C/Qt/5.9.2/msvc2015 package-msi

# for 32bit builds
make WINDOWS_BUILD=Win32 QT5_ROOT_PATH=C/Qt/5.9.2/msvc2015  package-msi

# to select a specific Visual Studio version
make WINDOWS_BUILD="Visual Studio 15 2017" QT5_ROOT_PATH=C/Qt/5.9.2/msvc2015  package-msi
```

Good luck!
