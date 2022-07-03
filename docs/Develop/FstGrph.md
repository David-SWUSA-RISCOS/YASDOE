[Back to Programming Documentation Index](./Index.md)

This page is still a Work In Progress (WIP).  It will take a little time to complete as this is a large component of the OS.

# FastGraph:

FastGraph is the YASDOE vector graphics library, and clipping support.  In many ways it is the equal to the RISC OS OS_Plot, AmigaOS Graphics.library, and the GS/OS graphics library (name omitted for reason) in functionality.

All primitive drawing operations are done by creating regions, and thus allow for significant flexibility.  This makes it possible to do any region operations between consecutive drawing operations very quickly and efficiently.  This also means that drawing to a region and then drawing the region is just as fast as normal drawing, which is very fast indeed.

Regions also provide the means of clipping, which works very simply do to the inversion point nature, as well as the ability to quickly do operations between regions.

Output can be to the screen or to any native raster graphics in RAM.  The native raster graphics format is that of the Sprite in a Sprite Area, this is the same as what is used by RISC OS, and similar blitting abilities exist.

---
## Drawng Functions:

The primary drawing functions are:

| Function       | Description |
|:--------------:|-------------|
| **Move**       | Moves the graphics cursor (Pen) location to specified point. Implemented as **Plot 68, x, y** . |
| **MoveTo**     | Move the graphics cursor (pen) to location relative to its current position.  Implemented as **Plot 64, x, y** |
| **LineTo**     | Draws a line from the current graphics cursor location to the specified location.  Implemented as **Plot 0, x, y** or if patterned pen **Plot 16, x, y** |
| **Line**       | Draws a line from one location to another.  Implemented as **Plot 68, x1, y1 : Plot 0, x2, y2** or if patterned pen **Plot 68, x1, y1 : Plot 16, x2, y2** |
| **FrameRect**  | Draw the outline of a rectangle.  Implemented as **Plot 68, x1, y1 : Plot 96, x2, y2** |
| **FrameRRect** | Draw the outline of a rectangle with rounded corners (roundrect).  Custom implementation (faster than the 16 plot calls). |
| **FrameCircle  | Draw the outline of a circle.  Implemented as **Plot 68, x, y : Plot 144, x+r, y** |
| **FrameOval**  | Draw the outline of an Oval. Implemented as **Plot 68, x, y : Plot x+r1, y : Plot x, y+r2** |
| **FrameArc**   | Draw an arc.  Custom implmentation, to reduce the calculations that would be needed to use **Plot 160** for this. |
| **FramePoly**  | Draw a polygon of arbitrary number of sides and shape.  Implementation does one **Plot 68, x, y** for the first point, then uses multiple **Plot 0, x, y** calls one per point,after the final point one more **Plot 0, x, y** call is used to close the polygon.
| **FrameRgn** Draw the outline of a region.  Custom implementation, as regions are a bit foreign to Plot in concept (have idea to fix that with custom **Plot 240** and **Plot 248** commands, though not done yet).
| **Plot**       | **The primary drawing call**, for which many of the others are just aliases.  The parameters are the same for OS_Plot in RISC OS (so is the SWI call number &45).  Plot may be called either by *SWI &45* or by calling Library &00 function &45. |

When a shape or region is displayed it can be painted, that is filled with a specific color.  This done by simply drawing horizontal lines in each internal span on each scanline.  This is an operation that can be performed very quickly in pure software rendering, and can also be easily accelerated by HW.  It is also possible to use a pattern when performing these operations.

Any of the drawing functions that begin with frame can be filled, the call names are composed by replacing **Frame** with either **Paint** or **Fill**.  To fill a shape drawn with the background color instead of the foreground you can use **Erase** to replace **Frame**, to invert background and foreground colors in a drawn shape you can replace **Frame** with **Invert**.

In most cases it is a little faster to use the Plot call, though this call does not yet support Regions.


---
## Pens, patterns, and Colors:

When you are drawing the color and pattern is set separately.  It is said that you setup the pen to draw with, a symbolic pin as it were.  The drawing mode is also set as part of the pen setup, that is to say if it is drawn by **SET** pixels, **OR** Pixel with previous contents, **XOR** pixels with previous contents, **EOR** the pixels at location, **NOT** the existing pixels, **BIC** the pixel color previous, **NOT OR** the previous content, or **NoDraw** (leave existing content untouched).

The default routine to set the color, pattern, and drawing mode is **Color** also aliased as **Colour** as a nod to those on the other side of the Atlantic creek.  This is very much the same as using **OS_Colour** (which I always defined the alias **OS_Color** for) in the ARM Computer OS.

The primary calls for setting up the pen are:

|                |                           |
|:--------------:|---------------------------|
| **Color**           | This is the primary call, most of the others convert parameters as needed and call this. |
| **HidePen**         | Decreases the pen count and sets the Drawing Mode to *NoDraw* if  pen count is zero. |
| **ShowPen**         | Increment pen count, if pen count was zero before increment restore previous drawing mode. |
| **SetPenMode**      | Transform the parameter, and set the pen mode as requested. |
| **GetPenMode**      | Returns the currently set pen mode. |
| **SetPenPat**       | Set the current pen pattern to use in drawing. |
| **GetPenPat**       | Get the currently set pen pattern. |
| **SetSolidPenPat**  |  Set the pen pattern to a solid color. |
| **SetBackPat**      | Set the background pattern for drawing. |
| **GetBackPat**      | Get the currently set background pattern. |
| **SetSolidBackPat** | Set solid color for background pattern. |



---
## Blitting:

Blitting is supported with many options.  This can be accomplished with CopyBits, or SpriteOp calls, and can be clipped by a region or by a rectangle.

There is also a series of operations that deal with memory based Sprite format bitmaps and blitting in relation to these.


---
## Regions and Clipping:

Line inversion point clipping for raster graphics goes back at least to the mid 1970's and if implemented well is very efficient.  Until the early 1980's this method was mainly used for sprites.  Inversion point masks can also be used as a means of defining an outline for drawing a complex shape (or even a simple shape).

In the early 1980's Bill Atkinson invented an improved form of inversion point raster graphics definition and clipping.  This improved form is known as regions and was patented, with protection running out in 2006 (so we can now use the concept).  The main improvement was on the storage format, which also had the side effect of reducing memory accesses thus speeding up drawing and clipping using inversion points.  Bill Atkinson also was the first that I am aware of to define that the inversion points be used directly for drawing to the raster display.  All previous inversion point clipping systems that I am aware of were just used to clip (mask) an image being displayed, and represented every line of the inversion point mask, even lines that were the same.

We use the improved form of inversion point clipping known as regions in FastDraw, as it is difficult to beat.  We use this for both Drawing primitives as well as for clipping

Regions are defined in the form of inversion points, with only lines where the inversion points change needing to be defined.  A region starts with its size, a rectangle defining the absolute bounds, then is the list of scan line inversion points in the rgnData part.  Each scan line that is different from the one above it (including the first scanline obviously) starts with the line number (relative to the bounding rectangle) and contains the position of each inversion (there should be an even number of inversions) terminated by the value $7FFF (largest positive 16-bit signed integer), after the very last scanline that produces changes the structure is terminated by an extra $7FFF.

If a the inversion points defined for a series of scanlines are odd in number (no closing point) then the rectangles left side bounds are used as the final closing position.  This is a rare situation, though none the less one that must be handled.

Yes regions are limited to the range of 16-bit signed integers, this is alright as display resolutions are unlikely to reach such a value.  Traditionally the size of a region is defined as a 16-bit value also, we use a 32-bit value as region data can exceed 65535 bytes in some cases.

**CLIPING** :

When used for clipping the regions are applied against the intended output on a per scanline bases, in a way that is much faster than traditional rectangle clipping.

It is also easy to create a clip mask region form the regions that cover the one being clipped.  This is done by starting with the region for the clip mask to be created for, then for each region that is blocking in front of our clipped region XOR it with the clipped region, until all objects forward of the clipped region have been XORed with the clip mask region.  Then the region is easily used as a clipping mask for output to the partially covered region (very useful with windows).  This should help illustrate why Region based clipping is way faster than using a rectangle list.

**DRAW TO REGION*** :

One way to create a region is to draw to the region.  This can be used to create complex shapes, though if you draw inside another shape already drawn it will create a hole, and if you surround an already drawn shape by another to draw the existing will become a hole.

In order to draw to a region you OpenRgn for output then when done you CloseRgn.

**MULTI REGION OPERATIONS** :

Regions can be combined in many ways, including the boolean Operations **OR,** **AND,** and **XOR** .  This allows for quickly creating very complex shapes.

**Operations on Regions:**

| Ooeration   |                |
|:-----------:|----------------|
| **XORRgn**  | Takes two regions, produces one region that consists of the parts of the two regions that do not overlap. |
| **ORRgn**   | Takes two regions and produces one region that has the area of both regions.
| **ANDRgn**  | Takes two regions and produces one region that is only the area overlapped by both regions.

**Defining Regions:**


**FAKING RECTANGLE LIST CLIPPING:**

When a program requests a list of visible rectangles from the window managers for updating the program is returned a single rectangle of the size of the visible area of the window.  Then when the program sets the clipping rectangle after the clipping is set to a region that occupies the visible area of the window in question, thus transparently using region clipping behind the back of a program that expects rectangle clipping, this is a lot faster.  There is one exception, in the case the window is completely obscured (has zero points in its visible region) it is returned an appropriate rectangle list to show this (that is to say it is passed zero rectangles total).

To create the visible region of any given window the window manager XORs the region of the windows in question with that of each and every window that is in front of the window, then it ANDs the resulting region with the Windows original region.  The resulting region represents the visible region of that window.  This is done when ever the region of a window changes, thus easing the work on everything else.


---
## Text and Font Support:



............