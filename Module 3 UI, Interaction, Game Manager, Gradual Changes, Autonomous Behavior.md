## Coverage

Unity specific skills you will need, practice, and demonstrate include:

·         User Interface

o   Sharing the editor between the GameObject world and the UI coordinate system

o   Working with UI RectTransform

·         Packages: create and import

Concepts you will explore and understand include

·         The lerp function: gradual rotation and chasing

·         Simple implementation of a finite state machine

·         Randomness and simple examples in games (again)

**1.**      **[User Interface and Packages](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.1):** Example based on Module-2 Example-4

o    **Run Behavior:** press-space bar to launch egg at slider-bar-value interval

o    **Packet Import:**

§  Assets èImport Package: select SliderWithEcho.unitypackage

§  From the github look for **ClassExample****/Packages**

§  PreFab: UI-SliderWithEcho

§  Scripts/UI/SliderWithEcho.cs

§  To create your own package, do the reverse: AssetsèExport and select the appropriate components (remember to select the necessary scripts)

o    **UI**: Using the imported package

§  Remember, first your scene must have a Canvas (create by: UIàCanvas)

§  To use: drag SliderWithEcho pre-fab into the Canvas:

**1.**      Align anchor: lower-left

§  Rename to: SpawnRate

§  Must configure: (Select SpawnRate and look in the Inspector Window)

**1.**      mLabelText

**2.**      SliderValue: (this is a Text UI object)

**1.**      Customize the text detail, e.g., color

**3.**      SliderBar (in the Slider component)

**1.**      Set:   Min Value, Max Value, Init Value

§  Careful: when adjusting positions of the SliderWithEcho object, do not adjust the children positions!

o    **GreenArrowBehavior**: reference an SliderWithEcho

§  In the editor: drag the entire SliderWithEcho (SpawnRate) to the GreenArrowBehaivor object

§  The value() of SpwanRate is how many seconds to wait in between spawning new eggs

§  Note: **Time.time** amount of seconds elapsed since the beginning of the game

o    **Learned:**

§  Almost all Unity specific:

§  Time.time: time (in seconds) after game began

§  Package: import/export of prefab watch to check all dependent components

§  Note the logic in GreeArrowBehavior::Update() on check for spawn rate.

o    **Alternate implementation**:

§  SpawnRateèSliderBar has a call back (event handler)

§  Can define a function in GreenArrowBehavior and add the function here.

**1.**      Pros: Receives value change via event, no need to refer in update()

**2.**      Cons: Implicit references (via event service functions), can be challenging to figure out all event handlers.

§  I usually poll UI events in Update() function.

§  Exercise:

§  Implement this alternative.

- **WARNING**: Text echo is not kind, default horizontal overflow is set to truncate, meaning, if a text is too long (e.g., number with many precision digits), the number will not show! Try it!!

- UI-Canvas àSpawnRateàSliderValue: under Text (Script)

§  A wrap in the horizontal and truncate in the vertical may result in part of the message not shown!

§  Look for **Horizontal Overflow**, try different settings!  
  

2. **[Cool Down Bar](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.2):** simple continuation from the previous example

- **Run Behavior:** press-space bar to launch egg at slider-bar-value interval and **_watch_** the cool down bar
- **Package Import**:

- Assets èImport Package: select CoolDownBar.unitypackage
- From the github look for **ClassExample****/Packages**

- PreFab: UI-CoolDownBar
- Scripts/UI/CoolDownBar.cs

- **UI**: Using the imported package

- Remember: you must have a Canvas (to create: UIàCanvas)
- Optional: set the value of _Sec_To_Cool_Down_

- Select CoolDownBar, and look for the CoolDownBar.cs component

- **GreenArrowBehavior**: reference an SliderWithEcho, and CoolDownBar

- In the editor: connect CoolDownBar UI to the instance variable
- Note: the re-spawn time restriction logic is now hidden

- **Learned:** Importance and beauty of OO, CoolDownBar hides spawn rate logic from GreenArrowBehavior!  
      
      
    

4. **[Gradual Rotation and Chasing](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.3)**

- **Run Behavior**:

- WASD: move the egg
- UpArrow chase after the egg
- TurnRate:  (be careful, slider bar may keep focus of mouse, click somewhere else to un-focus)

- 0 does not turn towards egg
- 1 always point at egg
- 0 < rate < 1: turns gradually from very slow (values close to 0), to very quick (values close to 1)

- **Egg**: WASD_Movement: trivial behavior
- **GreenArrowBehavior**:

- Public variables

- TurnRate: connects to the slider
- Target: connects to the egg

- PointAtPosition(): function

- Pointing the transform.up towards any given position

1. Incremental rotation of transform.up to align with V
2. Watch out, if transform.up and V are pointing in perfect opposite directions, the turning does not work.

- Update()

- Calls PointAtPosition()
- Move in the direction of transform.up

- In game object movement consideration

- **Easy**: Direct control: you control the position of an object
- **Less Easy**: Indirect control: e.g., you control the velocity of an object
- **Obey the rules of physics:** Indirect control in the world with physics (gravity and potentials for collisions), you configure the physics to control the object movement
- **Follow your own algorithm**: No control: autonomous (as in this case)

- **Learned**:

- Gradual rotation**:** Vector3.lerpUnclamped()
- The **PointAtPosition****(****)** function

- Quite reusable

- In-game object movement considerations  
      
      
    

6. **[Autonomous Movement with Randomness](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.4):**

- **Run Behavior**:

- Watch the green arrow chases the egg, when gets close, egg spawn in a new position in the pinkish area
- SliderBar changes the pinkish area size (% of world bound size)
- N-Key: to spawn a new GreenArrow
- H-Key: to hide the egg
- **Try**: spawn 20 arrows, and then hide the egg, see a bunch of patrolling arrows?!

- **Scene Setting**

- **MainCamera**: has **CameraSupport**: for setting and testing bounds

- Child: **GameManager****:** empty game object for hanging the singleton GameManager
- **TargetBoundBox** (pinkish)

1. This box is _behind_ the green arrow (with larger Z-position values, the larger the Z the more behind).
2. **Be careful****:** camera settings only allows z values of up to 1000: **MainCamera.Far**

- **GreenArrow**: chases after the egg

- **GameManager**:

- Awake():

- Initialize must be done before GreenArrowBehavior::Start()!

- Has reference

- CameraSupport: to compute world bound and target bound
- TargetBoundBox: to be scaled into the size user specified
- TargetBoundSlider: child of UI-Canvas, the slider bar

- GetTargetBound: computes the percentage of a given bound

- **GreenArrowBehavior****:**

- ComputeNewTargetPosition: a random target position within a given bound
- Vector.Distance(): Notice this function, convenient to use

- **Learned:**

- Compute the percentage of a given bound (**GameManager****::GetTargetBound()**)
- Random position in a bound (**GreenArrow****::ComputeNewTargetPosition()**)
- Distance between two game objects: **Vector3::Distance()** function
- Game object positions: **z values are important**

- Front is smaller z, behind/far is larger z
- SHOULD NOT change the z-value of an object during game play

1. May cause “flipping” rotation
2. E.g., change the z value of Target to e.g., 1.0f and observe arrow flips

- SliderBar callback function

- Efficient, only compute when there are changes
- Edited in the UI  
      
    

8. **[Finite State Machine](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.5)**

- **Run Behavior**:

- Move the arrow with WASD
- Touch the plane to trigger fixed behavior

- **Finite State Machine**: Simple state on the Plane. Here is the [state transition definition](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/EnemyState.jpg)

- Normally, nothing, when collision
- enlarge for 120 frames
- rotate CW fast for 80 frames
- rotate CCW for 80 frames
- shrink for 120 frames
- return to resting
- **Note:** in our context, if an operation does not need time, it is NOT a state. All states, in the FSM needs more than one update() cycle.

- **Implementation Keys**:

- Draw the state diagram!!
- Instance variables for state definition and transition
- Enum for individual states
- Case statement in update()
- State service: Each state is a separate function!

- As states become complicated, they can be defined as instance of different classes (with shared base class)

- Organization

- Partial class (different files implementing the same class)
- Plane.cs  and Plane_FSM.cs

- Each contains separate details!

- **Learned**:

- Finite State Machine: important to

- Draw out ALL states, and
- Define all possible input and state transitions

- Implementation key: review the above!
- Relatively straightforward to define simple repetitive autonomous behaviors!
- C# Partial class: to help separate source code into different files for organization  
      
    

10. **[FSM + Randomness](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.6)**

- **Run Behavior**:

- All planes cycles through states without going into resting
- Random enlarge and rotation periods (turn constants into variables)
- After a while, look rather random?

- **GameManager**: hanging off MainCamera

- Creates all the planes at startup

- **Plane:**

- Randomness: in the Start() function, sets the number of frames in scale/rotate states to be random

- **Learned**:

- Beauty and simplicity of random

§  Ease of expansion when well abstracted  
  

7. **[Orbiting](https://myuwbclasses.github.io/XJTU-IntroGameDev/Classnotes/Module-3/WebGL-Builds/3.7)**

- **Run Behavior**

- Eggs orbits around hero
- No UI support, must change from the editor, try

- Select Hero in Editor and move hero around (egg follows)
- Select Egg and change

1. Orbit Radius
2. Orbit Speed

- **Scene**:

- Egg is the satellite
- OrbitControlàHostXform points to Hero’s xform

- OrbitControl.cs on the Egg (can be on any objects):

- Literally 3-lines of code!

- **Learned**:

- Nice to know quaternion 😊.