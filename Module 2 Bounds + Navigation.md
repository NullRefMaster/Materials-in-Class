## Coverage

Unity specific skills you will need, practice, and demonstrate include:

·        Working with Unity Prefab

o   Create a prefab in the editor

o   Create/Delete objects at run time

·        Continue working with Transform of GameObject

o   Set positions

o   Set object rotation/orientation

·        User Interface

o   Getting world position from the mouse

·        Object collisions and responses

Concepts you will explore and understand include

·        The camera and visible world bound

·        Frame update time vs wall-clock real time

·        Randomness and simple applications in games

·        Direct object control: driving an object

1.      **[Camera bounds](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/WebGL-Builds/2.1)**

- **Run Behavior**: WASD place the arrow, touch the camera bounds to re-spawn randomly
- **Organization**: created a new folder in Assets, **Scripts**, to organize the scripts

- Two subfolders in Scripts (for now): Hero (support GreenUp), and Utilties
- In Utilities folder: CameraSupport

- **Scene setup**

- MainCamera: has a CameraSupport component
- GreenUp: has a GreenArrowBehavior

- **CameraSupport** script

- mTheCamea: reference to the camera
- mWorldBound: the current bounds of the world
- Behavior: updates the world bound per frame
- functions:

- GetWorldBound(): get the current world bounds
- CollideWorldBound(): collide a bound (of an object) with the world bound and returns collision status

- **GreenArrowBehavior**

- WASD: as previously move
- Now, collide with the world bound
- Print out collision status if collided, output shown in the Console Panel (WindowàPanels àConsole)
- Notice:

- How to get access to the MainCamera (Camera.main)
- How to get access to our own bounds (GetComponent<Renderer>().bounds)

- **Learned:**

- Source code (script) organization is important!

- Strategy: organize based using folder structure

- Unity’s function calling sequence!

- Constructor èAwake èStart èUpdate

- Unity components:

- Can always call gameObject.GetComponent<ComponentClassName>() to access component on an object

1. gameObject is a MonoBehavior instance variable that references the hosting GameObject

- Returns null when the component is not defined

- Locating game objects and/or components

- At initialization time (e.g., CameraSupport’s reference to the camera)
- At run time (e.g., GreenArrow’s reference to the CameraSupport component)

- Camera bound:

- Apply simple arithmetic in computing world bounds
- Notice the use of camera.aspect
- Compute intersection of bounds

- Random:

- Min + Random * Size

- Debug.Log() to printout to console panel

**2.**      **[Object navigation](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/WebGL-Builds/2.2):** All in **GreenArrowBehavior**.cs

o   **Run Behavior:** green arrow follow mouse, or <Space> and navigate with WASD

§  Space bar: to toggle mouse positioning vs keyboard WASD

o   **Public variables:** show up in Inspector and you can change these during runtime via the editor!

§  **WATCH OUT:** changes made during runtime in the editor WILL NOT be saved!

§  Mouse vs Keyboard control can be toggled

§  Travel speed/rotation speed can be controlled

o   **Speed:** Distance per unit time. Update() function is called at about 60 times per second!

§  mHeroSpeed: is units per second (Unity defines: Time.**smoothDeltaTime**) to convert frame update time period to wall clock time

§  Remember total height of the world is 200 units. Verify travel from top to bottom is about 10 seconds

§  mHeroRotateSpeed: 45-degree/second, takes about 8 seconds to do a 360-degree rotation

o   **Mouse** **position**: must translate pixel position to camera space

§  Make sure to zero out the z-component

o   **GetKey** vs **GetKeyDown****:**

§  State of a key vs. Event of a key went down

§  Many times vs only once!

o   **Navigation:**

§  Move towards the original y-direction: this is transform.up

newPosition  = oldPosition + (Speed * Time.smoothDeltaTime * transform.up)

§  Rotate left/right: rotation with respect to the z-axis or the transform.forward

Transform.Rotate(transform.forward, RotateSpeed * Time.smoothDeltaTime)

o   **Learned**:

§  Public variables show up in the Inspector window: Convenient!

§  **WATCH OUT****:** The configuration of these variables in the editor when the game is running will NOT be saved!

§  Frame rate vs real time wall clock

§  Unity variable: Time.smoothDeltaTime

§  Access mouse position (via the camera!)

§  Navigate an object by keyboard

§  **How to move forward:** transform.up/forward/right variables

1.      Note: these directions updates as you change the objects orientation

§  **How to rotate:** transform.rotate function changes the transform.up (forward/right) directions!

**3.**      **[Pre fab](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/WebGL-Builds/2.3):** Editor create prefabs and instantiate at runtime

- **Run Behavior**: space bar to spawn new eggs
- **Prefab**: "programming by example" drag an object (Egg) from Hierarchy/Scene-Window to Asset!

- Created a subfolder to keep Assets folder organized.
- **_NOTE:_** the "**Resources**" folder name is not an option!! Resources.Load(): depends on it!!

- **EggBehavior**

- Spawns and travels in its transform.up direction
- Kills self in a fix amont of time

- GreeArrowBehavior.cs::SpawnAnEgg

- How to load and instantiate from Resources folder.
- After instantiated, can change new objects’ values (e.g., localPosition)

- **Learned:**

- How to create and use Prefabs in the editor:

- Drag a GameObject into the Assets folder
- Drag a Prefab back into the Scene Window
- **Warning:** changing instances of a Prefab does NOT change the Prefab

- Organization of Prefeb: must be in the **Resources** folder (under Assets)
- How to instantiate a prefab at run time
- How to delete (Destroy) a GameObject

- **Note:** as in C++, you create, you delete, if you don’t delete, it will be there forever!

**4.**      **[Game Manager + Simple UI Text](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/WebGL-Builds/2.4)**

o   **Run Behavior**: space-bar to spawn eggs, see the echo count on screen

o   **Create UI**:

§  RMB: UI => Text (**Canvas** and **EventSystems** created automatically if not already there)

§  UI elements MUST BE child of Canvas, otherwise, will not show

§  Zoom out to see two spaces: Camera and UI

§  UI elements are in pixel space! (NOT camera space)

§  Size of UI space corresponds 1:1 to Game Window

§  Use Layer manager show/hide UI

![](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/index_files/image001.png)

o   **GreenArrowBehavior**: includes an int to keep track of number of eggs on screen

o   **EggBehavior**:

§  Static variable: refer to GreenArrowBehavior

§  What is a “static” variable?

§  Tells GreenArrowBehavior when an egg is destroyed

o   **GameManager**: central object to coordinate the entire game state

§  Hang off the MainCamera (always there), can also hang off an empty object

§  Two public variables must be set in the editor before game starts

§  GreeArrowBehavior and

§  UI-Text for echoing egg status (UI-CanvasàEggStatusEcho [a UI Text object])

§  Singleton pattern: One instance in the world, “well-known”

§  What is a “static” variable?

§  This is a GLOBAL variable!

§  Note: Play the important role of “central coordinator”

§  Connect GreenArrowBehavior to EggBehavior

§  Central place for echoing state of the game

o   **Learned:**

§  GameManager: Need to a central coordinator, often enforce to only have one

§  **static** declaration in a class

§  Class Variable persist for the entire process life time

§  Will persist over different levels (scenes)

§  UI: Two objects created automatically:

§  A **Canvas** object will be created, all UI objects must be a child of this canvas

**1.**      All UI elements must be a child to this object! (otherwise will not be visible)

§  An **EventSystem** object, I drag the EventSystem to be a child of the Canvas (for organization purpose).

§  Default UI-Layer: to see or not to see

- Coordinate Systems:

- Working on TWO separate groups of objects: GameObjects and UI
- Two distinct coordinate systems!!?

1. GameObjects: arbitrary
2. UI: Pixels

- Learn about Canvas and placement of GUI elements

- Canvas: [UI Canvas - Unity Official Tutorials](https://www.youtube.com/watch?v=OD-p1eMsyrU)
- Rect Transform: [Rect Transform - Unity Official Tutorials](https://www.youtube.com/watch?v=FeheZqu85WI)

1. UI element references are **NOT** with respect to the main camera!!

1. They are with respect to the Canvas! (in pixels!)

**5.**      **[Collision + Color + Texture](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/WebGL-Builds/2.5/index.html):** this WebGL link is useless as object manipulation must be done in the editor window!

- **Run Behavior**: boring! Does not even do anything!!

- You must run and move objects in the editor to overlap the two
- Move either of the objects to collide the two
- Wiggle Plane or Arrow to see Plane disappear and regenerate as an Egg

- **How Unity Collision** **works**, conceptual model: Mechanics and Cost

- Arrow and Plane wants to collide.

- Requirements: Both must have Collider2D defined, at least one has a RigithBody2D
- I looked at this: [https://answers.unity.com/questions/536674/how-to-detech-collision-without-rigidbody.html](https://answers.unity.com/questions/536674/how-to-detech-collision-without-rigidbody.html)

- NOTE: this is NOT physics, just collision detection
- In this example: Arrow has RigidBody, Plane does not

- Two Arrows can collide
- An Arrow can collide with an Plane
- Two Planes CANNOT collide

- **Arrow**: [The object that wants to handle the collision]

- Add BoxCollider2D (can be any collider 2D)

- Check “**isTriggered**”
- Trigger-related functions on this object will be called

- Add RigidBody2D (in Physics2D)

- Typeè**Kinematic**

- **Plane**:

- Add CapsuleColldier2D (or any collider 2D)
- If Plane has a script, its onTrigger functions will also be called independent from if “isTrigger” is enabled.
- Try:

- Toggle on Plane’s isTriggered (it’s script’s triggered-function will be called)
- When to switch on isTriggered? Only the “actively colliding objects” need to have isTriggered on.

1. E.g., my car is driving down the road, I want my car to collide with all the objects in the world, so my car is the “active colliding objects” and its “isTriggered” should be on. The rest of the objects in the world, they are NOT actively colliding with anything, so, I should not switch on their isTriggered. It is all about performance!

- Scripts:

- Arrow: onTrigger() functions
- Plane: onTrigger è calls UpdateColor()

- NOTICE: onTriggerStay2D() is called as long as collision status changes (e.g., if the two objects stop moving, this function is not called, but will get called again when the either of or both of the two objects move).
- **Texture/Sprite loading**: [https://docs.unity3d.com/ScriptReference/Resources.Load.html](https://docs.unity3d.com/ScriptReference/Resources.Load.html)

- Notice the “GetComponent<aComponent>()

- aComponent: look at the Unity editor, Inspector Window, any component is accessible!

- SpriteRenderer:

- Color + Sprite
- Adjust in UI, adjust from Script

- **WATCH OUT!**

- If Obj-A collides with ObjB + ObjC at the same time (e.g., ObjB and ObjC are perfectly overlapped), then ObjA.OnTriggered2D() will be called twice!

- **Learned**:

- How to enable and work with Unity 2D collisions and receive the collision function calls for response
- How to change the color/transparency of an object at run time.
- How to change the texture of an object at run time
- **OnMouseDown**: a method on MonoBehavior that can be over-written to receive calls when right mouse button goes down on the game object. You can take a look at this function.  
      
    

Here is [a self-practice exercise](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-2/Self-Exercise/Self-PracticeEX2.htm) to practice some of the above coverage.