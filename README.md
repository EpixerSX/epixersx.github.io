# [Promo PRM Engine](https://github.com/EpixerSX/epixersx.prm.engine/releases/download/prm03/prm4.03.zip) (v4.03)
### Open Source 2D Engine based on Python (PyGame + PyOpenGL)
#### Created by @epixersx

## Main Frameworks
- [PyGame](https://pypi.org/project/pygame/) - Workplace
- [PyOpenGL](https://pypi.org/project/PyOpenGL/) - Graphics
### 🔗 [About OpenGL (Open Graphics Library)](https://ru.wikipedia.org/wiki/OpenGL)


## Content
### Modules
- [Software Module](#software-module)
- [Key Module](#prm-key-module)
- [Color Module](#prm-color-module)
- [Gravity Module](#gravity-module)
- [Collision Module](#collision-module)
- [Data Saving Module](#value-module)
### Objects
- [Image Object](#image-object)
- [Text Object](#text-object)
### Samples
- [Default Sample](#maindemo)



## Maindemo
```python
import engine.promo as prm

Software = prm.software()
Software.initialize()


def update():
    pass

def update_tick():
    pass

Software.run(update=update, update_tick=update_tick)
```





# Software Module

```python
Software = prm.software()

# There you can place Software settings

Software.initialize()
```

### Software Configuration (Main)
```python
Software.RESOLUTION # (base = [1300,800]) / App Size (Pixels)
Software.FPS # (base = 120) / main update() function activations per second
Software.TITLE # (base = "PRM") / App Title
Software.TICKRATE # (base = 30) / cycle update_tick() activations per second 
Software.SyncLock # (base = False) / FPS Lock on main display hertz clock
Software.VSync # (base = False) / Vertical Synchronization
```
#### 🔗 [About VSync (Vertical Synchronization) ](https://steamcommunity.com/discussions/forum/1/648817377892882003/?l=hungarian)

### Software Configuration (Other)
```python
Software.adaptive_keybind # (base = True) / limits the number of keybind activations accepted by engine per second
Software.keybind_rate # (base = 60) / keybind per second limit
# For example: Player moving with 240 fps faster then 120 or lower, but adaptive_keybind fixing it
```
#### and you can get from Software
```python
Software.refresh_rate # Main display Hertz Clock
```

## Software Useful Functions
### Key Binds

### Once activation

```python
Software.bindkey(key, func) # function argument func will activate ONCE if key got pressed
```
#### Example:
```python
def trigger():
    print("Triggered")

Software.bindkey(prm.key["space"], trigger)

# But if function have arguments or not working

Software.bindkey(prm.key["space"], lambda: print("Triggered"))
```
### PRM Key Module
all english alphabet (non caps)
#### Special keys
alt, right_alt, shift, right_shift, space, ctrl
right_ctrl, tab, caps, esc, enter

### Multy activations
```python
Software.bindhold(key, func) # function argument func will activate MULTY if key got pressed
```
#### Example:
```python
# all same as bindkey but minor changes
```

### set_
```python
# I think this not need any explanation.
Software.set_title(title)
Software.set_resolution(resolution)
```

### Bind Button / Mouse Click Check / Mouse Hold Check

#### Bind Button
```python
Software.bindbutton(object, func, mode)

# This function making graphic object clickable to lmb.
# Mode == "up" or "down", default mode = "up"
# With mode "up" you func activation after let lmb.
# With mode "down" you func activation with lmb press

```
#### Example:
```python
# Read a bindkey / binhold function before this

points = 0
def click(count = 1):
    global points
    points += count

Software.bindbutton(coin, lambda: click(prm.rand(3,10)) # prm.rand(min, max) - random number
 
```



#### Mouse Click Check
```python
Software.is_clicked(functrue, funcfalse) # funcfalse base - None
# Mouse lmb click in general.
# functrue triggering if lmb clicked
# funcfalse triggering if lmb click not yet clicked
```
#### Example
```python
# Place in update() function

def clicked():
    print("Mouse Clicked")

Software.is_clicked(functrue = clicked)
# or use "lambda: " if you function have arguments

```

#### Mouse Hold Check
```python
Software.is_holding(functrue, funcfalse) # funcfalse base - None
```
#### Example
```python
# all same as Mouse Click Check but minor changes
```

### PRM Color Module
```python
prm.color._color_
```
#### Color List
```
gray / black / white / green / red / blue / purple
cyan / orange / violet / yellow / dark_gray / light_gray
```
#### Other Functions:
```python
prm.color.random_color() # You get Fully random RGBA OpenGL Color (0.0-1.0)x3
prm.color.list_random() # You get rendom color from Color List 
```


# Objects Classes
```python
prm.object.
```

## Image Object
```python
object = prm.object.image(Software)
```

### Configuration
```python
object.image # Write "file_name.extension", Place you image to engine\images
object.flip # (base = False, True) / Image Flip X/Y
object.color # (base = prm.color.white) / Image Coloring
object.rotation # (base = 0) / Image Rotation (Degrees)
object.scale # (base = 1.0) /  Image Size Scaling (100% - 1.0)
# after object.load_texture()
object.size # (base = [96,96]) / Image Size X/Y
object.position # (base = (Resolution-Size)/2) / Image Position X/Y

object.collision.scale # (base = 0.75) / Hitbox scaling for image size*scale
```

### Image Animation System
Created - 4.03 // Updated - 4.03
#### Functional
```python
image.add_animation(name, frames, speed, loop) # Base speed = 0.1, loop = True
image.play_animation(animation)
image.stop_animation()
```
#### Example
```python
player.add_animation(
    name = "Run",
    frames = ["player_run0.png", "player_run1.png", "player_run2.png"],
    speed = 0.075,
    loop = True
)

player.play_animation("Run")
```




### Image Useful Functions
```python
object.rotate(angle) # base = 0
object.move(pos) # base = [0,0]

# Not need to explanation
object.get_size()
object.get_pos()
object.set_pos(position) # base = (0,0)

object.draw() # Place it to update() cycle. outputs image to screen

# Collision
object.check_col(target, func_true, func_false) # If object touching target, triggering func_true.
# Triggering func_false if not (if func_false != None)
# base: func_false = None

# Unusual Functions
object.target(targetpos, stoprange, speed, funconend)
# Base, / targetpos - (0,0) / stoprange = (-5,5) / speed = 3 / funconend = None
# object.target - makes image move to targetpos, speed - not need to explanation
# stoprange - radius in which object stop moving and triggering funconend ("if it is not None")
object.reached(functrue, funcfalse, target, stoprange) # Now unusable

object.move_center() # Set image position to screen centre.
object.move_ur() # Set image position to screen up-right.
object.move_ul() # Set image position to screen up-left.
object.move_dr() # Set image position to screen down-right.
object.move_dl() # Set image position to screen down-left.

```
### Image Example
```python
image = prm.object.image(Software)
image.image = "image.png"
image.load_texture()
```
Update
```python
image.draw()```


## Text Object
```python
text = prm.object.text(Software)
```

### Configuration
```python
text.color # (base = prm.color.white) / Text Color
text.font # (base = None) / Text Special Font
text.font_scale # (base = 48) / Font Scaling
text.text # (base = "text") / Text
text.position # (base = [100, 100]) / Position on Screen X/Y
text.size # (base = [0, 0]) / Text Size X/Y
text.scale # (base = 1.0) / 1.0 - 100% / Text Size Scaling
text.flip # (base = [False, True]) / Text Filp X/Y
```
### Functions
```python
text.draw() # Place it to update() cycle. outputs image to screen
text.edit(text, color) # (base text = None, base color = None)
```



# Gravity Module
#### In Development / Not Recommended to use
## Gravity - World
```python
gravity = prm.gravity.world()
```
### Configuration
```python
gravity.power # (base = 0.66) / Gravity Powerful
```

## Gravity - Object
```python
object_gravity = prm.gravity.object(world_gravity)
```

### Configuration
```python
object_gravity.offset # (base = 0) / object Y offset with gravity interaction
object_gravity.weight # (base = 1) / object weight (interaction with gravity power)
object_gravity.acceleration # (base = 0) / moment of speed at Y
```

### Functions
```python
object_gravity.set_offset(offset) # offset base = 0
object_gravity.set_acceleration(acceleration) # acceleration base = 0
object_gravity.update() # -
object_gravity.touch() # Trigger this function if object colliding with ground
```

### Example
```python
None
```

# Collision Module

```python
col = prm.collision(position, size, object_scale) # object_scale base = 1.0
```
### Configuration
```python
col.scale # base = 0.75 
```
### Functions
```python
col.update_collisionz(position, size)
col.collide_check(object)
```

# Value Module
```python
val = prm.VALUE(name, base)
# name - File name on you PC 
# base - Value (INT/FLOAT) with whom value creating (If file uncreated), base = 0.0
```
### Functions
```python
val.get_value() # Returns a current value
val.add_value(count) # (base count = 1.0) / Increases Value on count
val.set_value(count) # (base count = 0.0) / Set Value on count
val.save() # Saving Value on PC
```
#### Configuration (Other)
##### File engine/config.py
Default
```python
project = {
    "name": "PRM_GRAPHICS_ENGINE",
    "version": "0.0.0A",
    "creators": "@epixersx",
    "saves_format": ".sv"
}
```
##### File Saving+
File saving at 
current_user/Documents/config.project["name"]/val.name/config.project["saves_format"]

### Example
```python
points = prm.VALUE("points")
points.set_value(10)
print(points.get_value())
points.save()

# File:
# C:\Users\EpixerSX\Documents\PRM_GRAPHICS_ENGINE\points.sv
# points.sv Value - 10.0
```







## To do
- [x] Test
- [ ] Test

