# Creating a New Project with AirSim
## Create a New Project
1. Open Unreal Project Browser
2. Under "New Project" Tab > "C++" Tab, and choose "No Starter Content"
![Step2](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step1.2.png?raw=true)
3. Choose a location to save your project under "Folder", and choose a project name under "Name" (*In this example, we set the name to be __MyProj__*)
4. Click on **Create Project**
5. At this point your project will be created, and *Visual Studio 2017* will open your project solution `MyProj.sln`  automatically.  Wait for a little bit as it will have to parse all files in the solution. It will also open the project in *Unreal Editor*
![Step1.5](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step1.5.png?raw=true)
![Step1.4](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step1.4.png?raw=true)
6. Note how you will then have files under "Config" folder, and some code in the "__MyProj__.uproject" which will all have to be modified.

## Use a Pre-existing World as Template
Here, we will look at world that has already been created, and will put its features into our **MyProj**. 
1. Go to "Epic Games Launcher" 
2. Click on the "Learn" tab (assuming you are under the *Unreal Engine* tab), and choose a world to download by clicking "Create Project"
   - Now, here there will be a plethora of different worlds in which you can choose from. You can choose something like "Landscape Mountains" or "Water Planes", which will be smaller in size (~ 2GB). Some others may be bigger (~ 30GB). 
![Step2.1](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step2.1.png?raw=true)
3. By this point, you should have a new project named after the world you have just downloaded. Now we will go onto merging things up!

## Copying Features onto Your Project
At this point, you should have two projects: your project which will be the one you'll be working on, and the template world. There will be several things to modify. 

*Note: Our project in this example will be called __MyProj__ and we will use __LandscapeMountains__ as our template world*

### Content Folder
When comparing the Content folder, there will be the`Assets/` and `Maps/`directories in `LandscapeMountains/Content/`, but they won't be present in `MyProj/Content/`.
1. Copy those folders from `LandscapeMountains/Content/` into `MyProj/Content/`

### DerivedDataCache Folder
1. Copy the DerivedDataCache folder from `LandscapeMountains/` into `MyProj/`

### Config Folder
The files you'll want to focus on are "DefaultEditor" and "DefaultEngine". The idea is that you want the "features" that are present in `LandscapeMountains/...` to also be present in `MyProj/...`
1. Open the files in pairs (e.g. "DefaultEditor" in __LandscapeMountains__ and in __MyProj__)
2. Whatever is present in __LandscapeMoutains__'s, copy and paste it in __MyProj__'s.
3. Repeat this for each file

#### Example: 
Before merging, "DefaultEngine" in __MyProj__ is:
```
[URL]

[/Script/HardwareTargeting.HardwareTargetingSettings]
TargetedHardwareClass=Desktop
AppliedTargetedHardwareClass=Desktop
DefaultGraphicsPerformance=Maximum
AppliedDefaultGraphicsPerformance=Maximum
```
Before merging, "DefaultEngine" in __LandscapeMountains__ is:
```
[URL]
GameName=LandscapeMountains

[/Script/EngineSettings.GameMapsSettings]
GameDefaultMap=/Game/Maps/LandscapeMap
GameStartupMap=/Game/Maps/LandscapeMap
EditorStartupMap=/Game/Maps/LandscapeMap

[SystemSettings]
r.vsync=1

[/Script/IOSRuntimeSettings.IOSRuntimeSettings]
MinimumiOSVersion=IOS_8
```
MERGE!
After merging, "DefaultEngine" in __MyProj__ is:
```
[URL]
GameName=LandscapeMountains

[/Script/EngineSettings.GameMapsSettings]
GameDefaultMap=/Game/Maps/LandscapeMap
GameStartupMap=/Game/Maps/LandscapeMap
EditorStartupMap=/Game/Maps/LandscapeMap

[SystemSettings]
r.vsync=1

[/Script/IOSRuntimeSettings.IOSRuntimeSettings]
MinimumiOSVersion=IOS_8

[/Script/HardwareTargeting.HardwareTargetingSettings]
TargetedHardwareClass=Desktop
AppliedTargetedHardwareClass=Desktop
DefaultGraphicsPerformance=Maximum
AppliedDefaultGraphicsPerformance=Maximum
```
After merging, "DefaultEngine" in __LandscapeMountains__ is:
```
[URL]
GameName=LandscapeMountains

[/Script/EngineSettings.GameMapsSettings]
GameDefaultMap=/Game/Maps/LandscapeMap
GameStartupMap=/Game/Maps/LandscapeMap
EditorStartupMap=/Game/Maps/LandscapeMap

[SystemSettings]
r.vsync=1

[/Script/IOSRuntimeSettings.IOSRuntimeSettings]
MinimumiOSVersion=IOS_8
```

*Note: In this scenario, you are to ignore "DefaultGame" because this essentially stores information about the project (e.g. description, project name). And you will also be ignoring "DefaultInput" because the AirSim has its own set of types of inputs, so you don't want these*

### The .uproject File
The .uproject file needs to know about your plugin!
![Step3.0](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.0.png?raw=true)
1. By this point, you should might need to go to the main directory of AirSim again and build it with `build.cmd` for your files. In case you didn't build it, you may have the following error message
![Step3.4](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.4.png?raw=true)
2. Go to the AirSim directory and navigate to the Unreal folder (`cd AirSim/Unreal`), where you will find a single Plugins folder
![Step3.1](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.1.png?raw=true)
3. Copy the entire Plugins folder into your __MyProj__ folder. Unreal Engine looks for a directory called "Plugins" in order to operate. By this point, your structure should look similar to this
![Step3.2](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.2.png?raw=true)
4. Close _Visual Studio_ and _Unreal Editor_
5. Enable your Plugins by opening the .uproject file in your favorite text editor, and add a `Plugins`  section, and key `AdditionalDependencies` so that your project looks somewhat like this:
```
{
	"FileVersion": 3,
	"Enginessociation": "4.16",
	"Category": "",
	"Description": "",
	"Modules": [
		{
			"Name": "MyProj",
			"Type": "Runtime",
			"LoadingPhase": "Default",
			"AdditionalDependencies": [
				"AirSim"
			]
		}

	],
	"Plugins": [
		{
			"Name": "AirSim",
			"Enabled": true
		}
	]
}
```

Now you are almost good to go!

## Features are Copied. Now, Unreal Editor
Great! Now, we need to set our settings on Unreal Editor!

1. Open up _Unreal Editor_ and open your project **MyProj**
2. Go to `File`>`Refresh Visual Studio Project`
![Step3.3](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.3.png?raw=true)
3. Setup the Mode as AirSim: Go to `Window`>`World Settings`, making sure it's checked
![Step3.5](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.5.png?raw=true)
4. Setup the Mode as AirSim: In the `World Settings` tab (located in the bottom right corner), under `World Settings`>`Game Mode` > `GameMode Override`, choose **AirSimGameMode**
![Step3.6](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.6.png?raw=true)

## Specific Additions to LandscapeMountains
In this specific example, there are multiple hangliders starting off from multiple different places. So, in this case, we just need a first start:
1. In `World Outliner` (located on the top right corner), if you look for "start", you will find multiple starting points. So you can delete all but one. 
![Step3.7](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.7.png?raw=true)
2. Once a single starting point is set, you can choose the initial location by hovering your mouse over the $(x,y,z)$ unit vectors and drag them around. If the starting point is located at an inaccessible point, then the central white sphere will turn shaded. 
![Step3.8](https://github.com/nicolasshu/Guides/blob/master/AirSim/Create%20New%20Project/images/Step3.8.png?raw=true)

## Running It
At this point, you may choose to either press on the "Play" button to run a diluted down simulation, or you may press on "Launch" button adjacent to "Play" in order to run the simulation more "*officially*"

## Inputs to Quadcopter
![xbox360](https://raw.githubusercontent.com/nicolasshu/Guides/master/AirSim/Create%20New%20Project/images/xbox360controller.jpg)
When using an Xbox 360 Controller on a drone, below are the inputs to the drone:

### Movement - Joystick (T,R,P,Y,Buttons)
Assuming (L) is for the left analog stick, and (R) is for the right analog stick, four floats are passed to the simulator, as 
$[L_{vertical}, R_{horizontal}, R_{vertical}, L_{horizontal} ]$, 
where the bounds are:

(This was edited in [StackEdit](https://stackedit.io/))
