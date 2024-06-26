## Coverage

·       Github

o   Branch/Fork

o   Learn that to save a Unity Project, **you only need the following three folders**

§  **_Assets_**, **_Packages_**, **_ProjectSettings_** [Actually, you only need to save the **Assets** folder, other two folders remembers project settings]

§  There is no reason to push the other folders to Github (or to submit them), e.g., all of these can be re-computed when Unity editor start your project: _Library_, _Temp_, _Logs_, _obj_, _.vs_

·       Basic

o   Open and work with the Unity editor

o   Setup for 2D camera, including setting world size

o   Build to EXE and WebGL

o   Hosting of a WebGL game

·       User Interaction

o   Polling of keyboard states

·       Unity Objects

o   Work with textures, creation of 2D sprite objects

o   Attach Scripts (mono-behavior objects)

o   Assign GameObject to script variables in the editor

o   Work with the Transform object to modify object position

**Unity:** Download and install Unity 3D. Refer to this link for [Unity installation help](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/UnityHelp.html). Take note of the version I am using, for this class, I do not see any reason to update to newer version. Note, after you choose a version _do not_ change/update during this class! Updating software versioning during a project is a major cause for project delay. Something to avoid at all cost.

**On-line tools:**

·       Hosting a web-page: (in Part-2) you will have to host Web-GL builds for your assignments/projects. Here is a free and convenient way to host your own web-page:

o   Via GitHub: [https://pages.github.com/](https://pages.github.com/)

**Git** and **Github:**

·       At the very minimum, you should fork off the provided link so that if there are changes you will know.

·       Now, create a fork and pull the source to your local machine.

·       **DO NOT** start Unity, instead open GitHub folder via your explorer

·       **Observe**: the Unity project folder **1.BasicSimpleProject**

o   There are two subfolders: **Assets** and **EXE**

o   You only need to pay attention to the **Assets** folder.

§  You should/will keep all of your created resources under this folder

o   The EXE folder is the _build_ result of the project.

·       **Learned**: Before submitting _source_ to your programming assignments, you should navigate to the project folder and remove all useless folders, e.g., Temp, Obj, Library, Logs, Builds.

o   **Warning**: always keep backup copies. If you accidentally removed files/folders you need, you must have a way to revert your changes.

·       **Observe**: Now go ahead and open 1.BasicSimpleProject with Unity3D. Notice that after the project is opened, there are many new folders created including: Library, Logs, Temp

o   **None** of these new folders are necessary in saving/retrieving your work.

o   **Although**, these folders speed-up Unity startup time, please do NOT submit these folders and do NOT push the contents of these folders to GitHub.

§  If you are using the free version of GitHub, the Library folder may be too large to push (will lock up your repo).

**Examples for Module-1**

1. **[Basic Simple Projec](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/WebGL-Builds/1.1)t**: start this project and

- Open the Scene:

- Look at the **Project** panel (WindowsàPanelsàProject)
- Notice: **Assets** and **Packages** folders, these are exact views of the file system that we have examined via the explorer.
- Click on **Assets**, and then **Scenes**
- Double click on **ClassExample**: this is our initial scene (level)
- Make sure to work in 2D space by clicking on the 2D option located in the top-left of the Scene window

![](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/index_files/image001.png)

o   The many editor windows

§  **Scene**: for editing

§  **Project**: we saw that keeping your stuff

§  **Hierarchy:** Examine your entire scene (all objects are listed here)

§  **Inspector**: Examining the details of the selected object

§  **Game**: for playing, try it (click on the Play button)

§  Be careful: confusion between **Scene** and **Game** Windows, look at the background color!  
  

o   Configuration editor

§  Drag the tab of **Game** window, you can detach the window!

§  Put Game and Scene windows and side-by-side

§  **Scene** Window: make sure you can see the camera boundaries

§  Re-size the **Game** window, notice how the camera boundaries in the Scene window updates to match with the aspect ratio of the **Game** window

§  Leads us to talk about the Camera.  
  

o   2D Environment: Main Camera setting

§  Click on the MainCamera object in the Hierarchy Window and refer to the Inspector Window (both of these windows can be opened via: WindowàGeneral)

§  Go into 3D mode, and see that the “Camera” defines a rectangular cube in the world. The content of the cube is shown in the world

1.     **Alt-Left-Mouse-Button**: to tumble the 3D editor camera

2.     **Middle-Mouse-Button** scroll: to zoom in/out

3.     Click on the manipulator button to active the **displacement** tool, notice the **rotate**, and the **scale** tools  
![](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/index_files/image004.jpg)

§  Notice the “**Transform**” values in the Inspector, in particular, the Position. That is the position of the Camera. Try changing it!

1.     Move the camera using the displacement tool (click on the arrows) or

2.     Type values in the Transform.Position x/y/z

![](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/index_files/image007.jpg) 

o   Initial camera settings:

§  Position: (0, 0, **-10**)

§  Rotation: (0, 0, 0)

§  Projection: **Orthographic**

§  Size: **100** (this is half the world vertical size, from the middle of the screen to the **top** of game window)

§  Clipping Planes: Near (0.3 is good). Far: **1000**

§  Now, our world:

§  +-100 in height (notice the total vertical size is actually 200)

§  Left/Right is X (transform.right is the unit X-vector)

§  Up/Down is Y (transform.up is the unit Y-vector)

§  transform.forward: is the z axis direction.

o   To zoom into the game camera (or any selected object):, select "Main Camera" (from Hierarchy window):

§  GameObjectàAlign View to Selected (or simply double click on the object in the Hierarchy window)

§  Remember, middle mouse button scroll to zoom

·       Textures (fancy name for images):

o   Drag any image into the **Project** folder (NOTE: will copy the image over to the project folder)

o   I created the **Textures** subfolder and dragged **GreenUp** into the subfolder.

o   Make sure the **Texture Type** è Sprite (2D and UI)

o   Note: the **Pixel per Unit** setting. E.g., a 1000x500 image, with pixel per unit setting of 100, will appear as a 10x5 object.

·       2D Sprite Objects:

o   Most (if not all) of objects we work with will be 2D Sprite Objects.

§  The "Arrow" is a 2D Sprite

o   GameObjectà2D ObjectàSprite

o   Drag the texture from **Project/Assets/Textures** to SpriteRendereràSprite

o   Make Arrow size 10x10 (otherwise, you can't see it ... 1x1 can be difficult to see)

§  Note, z-size is always 1

o   Alternatively,

§  You can simply drag the GreenUp texture into the Scene Window

·       Size of the visible world (of the Game window)

o   What is the height of the Game window?

§  NO! not in pixels, but, object’s coordinate (World Coordinate)

§  Try changing the GreenArrow Transform.Position.y to 100, what do you see, why?

o   What is the width of the Game window? [Try changing the size of the Game window and see the camera boundary size change!]

§  How can we find out?

§  Need to know the Game window pixel resolution and compute aspect ratio!

·       Editor vs Game mode

o   Editor mode: typical editing

o   Play mode: when the game is running in the editor

§  **Nice:** you can continue to make changes via the editor

§  **Warning:** all changes will be **_lost_** after Play mode exists!

§  **Recommendation:** set up hint for yourself: EditàPreference: Look for Colors and set the Playmode tint to remind yourself.  
![](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/index_files/image009.jpg)

·       Build your game: make sure you know how to build

o   To a [PC EXE where you can download, unzip, and double click on EXE](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/1.1.BasicSimpleProject/EXE/Module-1-Ex1-EXE.zip) file and run.

o   To a [WebGL where you can run in your browser](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/1.1.BasicSimpleProject/EXE/Module-1-Ex1-WebGL/index.html).  (**Make sure** to [read this, you may run into build errors](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/WebGL-Builds/WebGLBuildSetting.html))

§  Notice, it takes a LONG TIME to build WebGL

§  Make sure you learn and practice how to host your own unity web GL game.

·       **Learned:**

o   Open a Unity Scene

o   2D Camera settings and the size of the visible world

o   How to create new textures for 2D Sprite Objects

o   Creation and manipulation of 2D Sprite objects via the editor

o   Unity editor observations, Key Windows:

§  **Scene**: Interactive editor window

§  **Hierarchy**: Listing of all objects in Scene

§  **Inspector**: Details of current selected object

§  **Project**: Convenient view into the file system for working with resources

§  **Game**: What is visible through the MainCamera in the Scene

§  **Console**: Error and status messages show up here (Note on convenient settings: **_Clear on Play_**, and **_Collapse_**)

o   Editor vs Play mode: and play mode changes are NOT saved!  
  

**Entity-Component-System (ECS) Architecture and Unity:**

·       Entity è GameObject

·       Component **è** Components (e.g., Camera, Sprite Renderer, your script)

·       System **è**The organization and protocol provided by Unity, e.g.,

o   Calling sequence of components: Constructor(), Awake(), Start(), and continuously call Update()

2. **[Scripts on GameObjects](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/WebGL-Builds/1.2)** and Keyboard input:

- To _add_ a script to an object:

- Inspector Window: Add Component
- Drag a script file onto the inspector
- Programming Model: Entity-Component-System

- A script is an instantiated MonoBehavior object, stored as a component on GameObject

- MonoBehavior objects:

- Awake()/Start(): to initialize your object. Awake() is guaranteed to be called before any of the Start().
- Update(): called once per frame.

- GreenUp object has a GreenArrowBehavior script/component

- Script file: Project/Assets/GreenArrowBehavior.cs
- Double click to examine the file in VisualStudio

- Scene vs Game Windows

- Scene Window: for editing
- Game Window: what your player will see

- Run the game (the Triangle button in the middle of the editor):

- WASD: to move the green arrow around

- Verify top of the screen is y=100

1. With GreenUp selected, run and examine the Inspector

- What is the width of the world and why?

- Changes during the game is **_not_** saved!

- With the game running, select the GreenUp and delete it!
- Quit game to see the object returns

- Unit of the world:

- Independent from pixels!
- Defined by the Camera’s Size
- How do we estimate “speed” (displacement / unit-time)?

- **Debug:** please refer to **_Debugging_** on the [Unity help page](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/UnityHelp.html).
- **Learned:**

- How to add scripts to game objects
- ECS and Unity architecture
- Scripts

- Programing model (ECS) an instantiated MonoBehavior attached to GameObject as a component
- Running protocol: Start() of all objects called, then, one Update() called per frame

- In the editor: when game running, changes are NOT SAVED!!

- ***** NOTE THIS *****: do not waste time editing your game while the game is running!!
- You will waste time on this, and you will learn!  
      
      
    

4. **[In class self-exercise:](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-1/Self_Exercise/Self-PracticeEX1.htm)**

- In class, follow the above instructions and practice what we have learned today.
- After each step, I will show you what I would do

=================

**Credit of images**: All of the clipped arts used in all examples of this class are from "_Microsoft Office Free Clip Art Library_." These were images found from many years ago. The website upon which these images were downloaded from cannot be found anymore. One source that seem to include some of the images is: [http://clipart-library.com/microsoft-cliparts.html](http://clipart-library.com/microsoft-cliparts.html) (Links to an external site.). This is not the original site I downloaded from, but, they do seem to include some of the arts I used.