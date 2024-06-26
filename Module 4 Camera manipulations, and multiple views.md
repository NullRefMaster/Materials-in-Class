## Coverage

Unity specific skills you will need, practice, and demonstrate include:

·         Working with camera viewport

·         Changing scenes

·         Information persisting across scenes

·         Sprite sheet (Atlas)

Concepts you will explore and understand include

·         More about the lerp function

·         Camera views and the game world,

·         Soft and hard movement of the camera: lerp and shake

1. **[Basic Camera Controls](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-4/WebGL-Builds/4.1):**  

- **Run Behavior**:

- N: Move camera by (x, y) values (from the X/Y slider bars)
- M: Move camera to (x, y) values (to where Dye is located)
- H: Zoom with respect to the center (zoom factor slider bar)
- J: Zoom with respect to Dye (zoom factor slider bar)

- **Scene setup:**

- MainCamera:

- Has CameraSupport

- UI-Canvas:

- X/Y/Zoom: sliders (all connected to UserControlLogic)

- TheWorld: has UserControlLogic

- Background: Z=1 (larger than hero and egg)
- Hero and Egg

- **UserControlLogic****:** central object that receives and parses user input

- Connection to UI sliders and other game objects
- Transmits user input to game objects to cause changes

- **Camera folder**/

- CameraSupport: seen this before, new function: ClampToWorldBound()
- CameraSupport_Manipulate: manipulates the connected camera

- MoveBy, Moveto, Zoom(towards center), ZoomTowards(point), PushCameaByPos()

- **Testing**:

- HeroControl (on the Hero)

- CollideWorldBound code
- PushCamera

- EggBehavior

- ClamAtWorldBound (always inside)

- **Unity How to**:

- Slicing Sprite Sheet (Atlas)

- Import Sprite Sheet (Type: Sprite (2D and UI))
- Select the Sprite
- Sprite Mode èMultiple
- Invoke the Sprite Editor, Click on Slice è Apply

1. You may have to install the Sprite Editor [using PackageManager](https://docs.unity3d.com/Manual/upm-ui.html)
2. Search for “2D Sprite” to install under “Unity Registry”

- Empty GameObject on TheWorld: UserControlLogic

- For organization

- **Learned:**

- Camera manipulation: simple changes to camera’s transform object (position, and orthographicSize)

- Note: the _partial class_ to separate implementation into logical units

- Depth layering:

- Background with Z=1 (behind Hero and Egg)

- Unity: slicing of a sprite sheet  
      
      
    

3. [Taking a closer look at **Lerp**](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-4/WebGL-Builds/4.2)

- **Run Behavior**: **Z** to see Lerp

- Try type Z-repeatedly!

- Increase to twice current size and tries to Lerp back gradually
- If continue to increase size before lerping to original size, net growth in size
- This can be easily avoided in HeroControl (how? e.g., ignore z-key when LerpIsActive())

- Examine: **TimedLerp** class

- Perform lerp for a fixed duration
- Rate is in units of second (easier to think about?)
- Rate and Duration are sliders in the UI-Canvas

- Look at **HeroControl**

- BeginLerp() to begin

- do not need to always SetLerpParms(), if you know the values

- LerpIsActive() to receive proper lerp results

- **Learned**:

- TimedLerp:

- Pretty handy class in general?
- This is is _NOT_ a MonoBehavior!

- Note on testing: separate and trivial test environment, test all aspects  
      
      
    

5. [More respectful **camera manipulation**](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-4/WebGL-Builds/4.3):

- **Run Behavior**: same as previous examples, but notice the damping effect!

- N: Move camera by (x, y) values (from the X/Y slider bars)
- M: Move camera to (x, y) values (to where Dye is located)
- H: Zoom with respect to the center (zoom factor slider bar)
- J: Zoom with respect to Dye (zoom factor slider bar)

- **CameraSupport**:

- Position Lerp
- Size Lerp
- Update() function must check,

- If Lerps are going, must set accordingly

- **Learned**:

- One simple example of using the TimeLerp function (in lerping the camera position and size)  
      
      
    

7. **[Shaking](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-4/WebGL-Builds/4.4)** … for the camera and more

- **Run Behavior**: same as previous examples, added key control

- **X:** To shake the camera (boss is coming!)

- Utility/**ShakePosition** (in Utility)

- Sampling on a DampedHarmonic function
- Number of cycles
- Length of shake duration

- **CameraSupport_Manipulate**:

- SetShakeParameters
- UpdateShake()

- When done, will return the original position

- **Learned**:

- Describe behavior and search functions learn, appropriately sample functions

- **More advanced camera behaviors**:

- Parallax, following: look for existing solutions (try to avoid implementing solutions that are already out there).  
      
      
    

9. **[Viewport and Hero Cam](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-4/WebGL-Builds/4.5)**:

- **Run Behavior**: same as previous examples

- with a small cam focusing on the hero

- **Small cam**: Create a new Camera

- Projection: Orthographic
- Depth: > 0 (Main Camera is -1, the bigger the number, the more front)
- Check out the Viewport setting

- **CameraSupport**:

- SetViewportMinPos(x, y)
- SetViewportSize(w, h)

- **UserControlLogic**: testing

- Sliders connected to the HeroCam
- Change the small view viewport settings

- **HeroControl**:

- Changing the CamPosition of small view

- Questions:

- What does it mean to zoom in the small view?
- What does the orthographicsSize of Small view mean?

- **Learned:**

- What is a viewport and its settings
- How to work with the Unity viewport  
      
      
    

11. **[New Scene](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-4/WebGL-Builds/4.6)** and Game State that persists over scenes

- **Run Behavior**: same as previous examples

- Perform some hero lerp and camera shakes (see the text echo)
- **L** key to load new scene: notice lerp and shake info persisted across scenes

- **Unity details**:

- Using **UnityEngine.SceneManagement**: [https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadScene.html](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadScene.html)
- MUST:

- FileàBuild Settings

1. Make sure all levels to be loaded are in the Scenes In Build

- **Level Persistency**: Singleton Pattern

- **GameState** class

- Print from UserControlLogic

- NewLevel level

- Simply echo, value persisted levels!

- **Organization**:

- Level-Specific folders

- Level-specific behavior: NewLevelGameManager

- Level-ClassExample

- HeroControl, EggBehavior, and UserControlLogic

- Move Camera into Utilities

- **Learned**:

- All game objects are erased when a new scene is loaded
- Must take special care (e.g., Singleton pattern) to create and maintain info across scenes
- Unity how to: create/load scene

- Take a look at:

- DontDestroyOnLoad()
- [https://learn.unity.com/tutorial/implement-data-persistence-between-scenes](https://learn.unity.com/tutorial/implement-data-persistence-between-scenes)