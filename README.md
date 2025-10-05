# Unity First Person Controller
A complete first-person character controller for Unity using the new Input System with mouse look, movement, sprinting, and jumping mechanics.

## Features
- **WASD Movement**: Smooth character movement with customizable walk speed
- **Sprint System**: Hold shift to sprint at increased speed
- **Mouse Look**: Full 360° rotation with pitch clamping to prevent over-rotation
- **Jump Mechanics**: Physics-based jumping with ground detection
- **Ground Check**: Sphere-cast ground detection for reliable jumping
- **Input System Integration**: Built with Unity's new Input System for flexible input mapping

## Requirements
- Unity 2021.3 or higher
- Unity Input System package (install via Package Manager)
- Character Controller component
- Camera (Main Camera or assigned camera transform)

## Input System Setup
1. Create a new Input Actions asset (Right-click → Create → Input Actions)
2. Create the following actions:
   - **Move**: Action Type = Value, Control Type = Vector2
   - **Look**: Action Type = Value, Control Type = Vector2
   - **Jump**: Action Type = Button
   - **Sprint**: Action Type = Button
3. Bind the actions:
   - Move → WASD or Left Stick
   - Look → Mouse Delta or Right Stick
   - Jump → Space or Gamepad South Button
   - Sprint → Left Shift or Gamepad Left Shoulder
4. Add a **Player Input** component to your player GameObject
5. Assign your Input Actions asset to the Player Input component
6. Set Behavior to "Invoke Unity Events"
7. Connect the events to the script methods:
   - Move → `FirstPersonController.OnMove`
   - Look → `FirstPersonController.OnLook`
   - Jump → `FirstPersonController.OnJump`
   - Sprint → `FirstPersonController.OnSprint`

## Configuration

### Movement Parameters
| Parameter | Description | Default |
|-----------|-------------|---------|
| Walk Speed | Base movement speed (units/second) | 5.0 |
| Sprint Speed | Movement speed while sprinting | 8.0 |
| Jump Height | Maximum jump height in units | 2.0 |
| Gravity | Gravity force applied to player | -9.81 |

### Mouse Look Parameters
| Parameter | Description | Default |
|-----------|-------------|---------|
| Mouse Sensitivity | Look rotation speed multiplier | 2.0 |
| Max Look Angle | Maximum up/down camera angle (degrees) | 80° |
| Camera Transform | Reference to the camera transform | Auto-detected |

### Ground Check Parameters
| Parameter | Description | Default |
|-----------|-------------|---------|
| Ground Check | Transform position for ground detection | Assigned in Inspector |
| Ground Distance | Radius of ground check sphere | 0.4 |
| Ground Mask | Layer mask for walkable surfaces | Default |

## How It Works

1. **Movement**: The controller reads WASD input and moves the character relative to where they're facing
2. **Sprinting**: When the sprint button is held, movement speed increases from walk speed to sprint speed
3. **Mouse Look**: 
   - Horizontal mouse movement rotates the entire player body (Y-axis)
   - Vertical mouse movement rotates only the camera (X-axis) with clamping to prevent flip-over
4. **Jumping**: 
   - Ground check uses a sphere cast to detect solid ground beneath the player
   - Jump applies an upward velocity calculated from the desired jump height
   - Gravity continuously pulls the player downward
5. **Cursor Lock**: The cursor is automatically locked and hidden when the game starts

## Customization Tips

### Adjusting Jump Feel
Modify jump height and gravity together for different jump feels:
```csharp
// Floaty jump
[SerializeField] private float jumpHeight = 3f;
[SerializeField] private float gravity = -5f;

// Snappy jump
[SerializeField] private float jumpHeight = 1.5f;
[SerializeField] private float gravity = -15f;
```

### Adding Sprint Stamina
Integrate with the Oxygen System or create a stamina system:
```csharp
if (isSprinting && currentStamina > 0)
{
    currentSpeed = sprintSpeed;
    currentStamina -= Time.deltaTime;
}
```

### Changing Mouse Sensitivity at Runtime
```csharp
public void SetMouseSensitivity(float newSensitivity)
{
    mouseSensitivity = newSensitivity;
}
```

## License
This controller is provided as-is for educational and commercial use.****
