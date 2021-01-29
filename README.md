# Deployment of QT Applications on Windows

Example how to deploy a QT application on Windows. Tested with MinGW 64-Bit.  
All information can be found here:

- [Qt for Windows - Deployment](https://doc.qt.io/qt-5/windows-deployment.html)  
- [Tutorial: Creating an Installer](https://doc.qt.io/qtinstallerframework/ifw-tutorial.html)

## Prerequisites

- Installation of the QT Framework
- Installation of the qt-installer-framework
  - Get an official release: https://download.qt.io/official_releases/qt-installer-framework/4.0.1/
  - Build it from source: https://doc.qt.io/qtinstallerframework/ifw-getting-started.html

## Preparations

- Build Qt application with Qt-Creator (release)
- Copy application dependencies with the 'windeployqt' tool to the deploying structure
  - Copy executable example-app.exe to the 'package\com.vendor.product\data' folder
  - Get all dependencies of the application with the 'windeployqt' tool:

    ```cmd
    windeployqt path_to_deploy_dir\packages\com.vendor.product\data\example-app.exe
    ```

- The following DLL's are still missing and have to be copied manually to the 'package/data' folder:
  - libgcc_s_seh-1.dll
  - libstdc++-6.dll
  - libwinpthread-1.dll  
  They are located in 'C:\Qt\5.15.2\mingw81_64\bin'
- Modify the 'config\config.xml' and the 'packages\com.vendor.product\meta\package.xml' ([More info](https://doc.qt.io/qtinstallerframework/ifw-tutorial.html))
- Copy a proper license to 'packages\com.vendor.product\meta\license.txt'

## Build

- Build the installer with the 'binarycreator' form the qt-installer-framework

  ```cmd
  path_to_qt-installer-framework\bin\binarycreator.exe -c conifg\config.xml -p packages ExampleAppInstaller.exe
  ```
