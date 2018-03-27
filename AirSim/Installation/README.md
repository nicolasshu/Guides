# Build AirSim on Windows

## Install Unreal Engine

1. Download the [Epic Game Launcher](https://www.unrealengine.com/download). While the Unreal Engine is open source and fee to download, registration is still required.
2. Run the Epic Games Launcher, and open the Library Tab on the left
3. Click on "Add Versions", which should show the option to download __Unreal 4.16__
4. If you have multiple versions of Unreal installed, then make sure 4.16 is the "Current" by clicking down arrow next to the Launch button for the version
![UnrealEngine](https://github.com/nicolasshu/Guides/blob/master/AirSim/Installation/images/Install_UnrealEngine_1.jpg?raw=true)

## Build AirSim
1. Install [**Visual Studio 2017**](https://www.visualstudio.com/downloads/). In such case, if you download **Visual Studio Code**, it will **NOT** have some of the tools necessary to complete the installation. I would suggest using **Visual Studio Community**. 
2. Once installed, open __x64 Native Tools Command Prompt for VS 2017__. *Make sure __not__ to open Windows' Command Prompt*
3. Create a folder for the repository and run `git clone https://github.com/Microsoft/AirSim.git`
4. Start to install [CMake](https://cmake.org/download/). A few notes:
   - When installing, by default, the installer sets it such that cmake won't be on PATH. So, make sure to check the box, setting it to be on PATH. If you don't, when trying to run it later on, it will give you errors with: `find: 'cmake version': No such file or directory` ([Source](https://github.com/Microsoft/AirSim/issues/755))
   - To test to make sure CMake was properly installed, go into the directory of AirSim and type in `cmake` to make sure you don't get an error
   - CMake will be used to build the **rpclib** submodule
5. Go to the AirSim directory, while still on __x64 Native Tools Command Prompt for VS 2017__, and run `build.cmd` from that command prompt. This will create ready to use plugin bits in the `Unreal\Plugins` folder that can be dropped into any Unreal project. 
   - In case you get an error in regards to missing "v140 Toolsets", your Visual Studio installation will need to be modified, and you'll have to do the following steps ([Source](https://developercommunity.visualstudio.com/content/problem/48806/cant-find-v140-in-visual-studio-2017.html)):  
      1. Go to 'Control Panel' and select the "Modify/Change" button for 'Microsoft Visual Studio"
      2. Under the "Summary" pane of the workload selector, click the "Desktop development with C++" expander (if it is collapsed)
      3. Check the "VC++ 2015.3 v140 toolset (x86,x64)" optional feature 
   ![v140](https://github.com/nicolasshu/Guides/blob/master/AirSim/Installation/images/v140%20Toolset%20Error.png?raw=true)
   
6. Now you have finished installing AirSim which uses Unreal Engine.



(Edited in [JBT's Markdown Editor](https://jbt.github.io/markdown-editor/))
