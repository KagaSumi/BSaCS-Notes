# Game Loop
The *game loop* is a loop that performs 3 main tasks each iteration
- Listens for system and input events
- Modifies your game state
- Draws the current game state to the screen
The Order of the tasks is important, for example
1. Check and see if a certain key was pressed
2. Move the player based off the input
3. Draw the player to the new position of the screen

Each iteration of a game loop is called a *frame*

A game loop is capped so it doesn't run too fast (aka. frame limiting)
	E.g., 60fps,30fps,etc.
	Refresh rate for most modern monitors is 60hz

If a game loop is not capped, it will push th ehardware to process as many frames as possible
- Overheating
- Wasted energy
- Tearing

# SDL

A **SDL** is a multimedia library that provides low level access to:
- Audio
- Keyboard
- Mouse
- Joystick
- Graphics hardware

Other common multimedia libraries are
- SFML
- GLFW
- Raylib

It sits between the operating system and engine
- Hardware
- OS Drivers
- SDL
- Game Engine
- Game

This abstraction layer allows us to access the OS's native tools
- Win32, Cocoa (macOS),Android NDK, iOS UIKit, etc.

The SDL is used to create out game window and render