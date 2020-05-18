# Building VSCode (Code - OSS) for Windows/ARM64

Since I use VS Code every day on my Surface Pro X I needed to have some more recent builds for the Win Arm64 platform, I followed the original instructions from here [Building VSCode for Windows/ARM64](https://github.com/dsugiyama/build-vscode-win-arm64) (thanks to dsugiyama).

I'll try to keep this updated as long as new versions of Code - OSS are released

Here is the prebuilt binary archive: [VSCode-win32-arm64-1.45.1.zip](VSCode-win32-arm64-1.45.1.zip)

## Compile it yourself

A few things have changed from the referenced instructions. You no longer need to patch anything since arm64 is included in the build source files.
So really all you need to do is to get your build machine set up correctly with the necessary tools.

### My build machine software

Visual Studio Community 2019 16.5.5, with the following components

- Desktop development with C++ 
- MSVC v142 - VS 2019 C++ ARM64 build tools (v14.25)
- MSVC v142 - VS 2019 C++ x64/x86 build tools (v14.25)
- Python 2 32-bit (2.7.16)
- Windows SDK: 10.0.19041.0

### Node.js - globally installed packages

- node v12.16.3  
- node-gyp v6.1.0

### Build Steps Recap

As I mentioned these are the steps from the linked project above with my comments.

Ensure npm variables are correctly set using Command Prompt. (Setting npm variables in Powershell does not work in this way, stick with CMD)

```Shell
npm config set msvs_version 2019
npm config set python C:\Python27\python.exe
set npm_config_arch=arm64
"C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvarsamd64_arm64.bat"
```

Before you start the code build script, check the variables are set properly with

```Shell
npm config list
```

## Code Build

```Shell
cd vscode
scripts\code.bat
yarn run gulp vscode-win32-arm64
yarn run gulp vscode-win32-arm64-archive
```

If everything works correctly, a binary archive is created in `.build\win32-arm64\archive`.

## Potential Problems

### node-gyp

This seems to be quite sensitive to configuration problems. You can test the MS build tools are correctly set up working, fixing the ones that present failure with

```Shell
node-gyp rebuild --verbose
```

### Clean build folders

After a failed build I found things worked smoothly the next time by manually deleting the previous build folders `.build, node_modules`.


Thanks again to dsugiyama for the original work.
