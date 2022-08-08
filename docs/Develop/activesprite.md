# Active Sprites:

In YASDOE we have a special type of **Sprite** (bitmapped Graphics) called an **Active Sprite**.  An Active Sprite is like a normal masked bitmap (Sprite) in the WIMP that is displayed in a visible window, though it allows the contents to be updated and displayed up to date without explicitly making it dirty.  This allows more effecinet implementation of animation or other rapidly changing content (playing videos, games, etc).

The format in memory is the same as a normal **Sprite**, which can be used as a pseudo frame buffer.  The difference is that the WIMP is told that the **Sprite** is Active, so the WIMP can automatically keep it up to date.   The details of how this is done vary a bit depending on the graphics HW in the system.

If the system has a GPU that allows for layers, then the display is divided so that the active content has its own layer, and the GPU can do most of the work of updating the display.   If this is not available then software rendering is used, taking advantage of DMA if available, to update the sprite with clipping for anything infront of it.  Either way it is quite a bit faster than the old method of having to tell the WIMP that the area is dirty and needs to be redrawn.

This is always a speed up as it avoids multiple SWI calls (as would normally be needed) or direct WIMP calls (YASDOE enhanced calling).  This eases the overhead when writing anything that does a lot of constant updating of a graphics buffer, thus easing the creation of Video players, Animation viewers, Games, active graphics of other kinds, etc.

It is also possible to specify an **Active Sprite** as having sound.  As part of the definition of an **Active Sprite** is the frame rate, if the sound source buffer specified is updated once per frame the WIMP will automatically play the stereo sound samples at the specified rate.  This means that an **Active Sprite** is extreamly useful for many forms of multimedia in an intuitive way that reduces the load on the system.
