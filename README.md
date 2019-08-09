# align_positioned

**Why is this widget an indispensable tool?** 

When your desired layout feels too complex for Columns and Rows, `AlignPositioned` widget is a real life saver.
Flutter is very composable, which is good, but sometimes it's unnecessarily complex to translate some layout 
requirement into a composition of simpler widgets. 

The `AlignPositioned` aligns, positions and optionally sizes its child 
in relation to both the container and the child itself.
In other words, it lets you easily and **declaratively** 
define the position and size of some widget in relation to another. 

For example, *you can tell it to position the top-left of its child at 15 pixels
to the left of the top-left corner of the container, 
plus move it two thirds of the child's height to the bottom plus 10 pixels.*
Do you even know how to start doing this by composing basic Flutter widgets?
Maybe, but with `AlignPositioned` it's much easier, and it takes a single widget.

The `AlignPositioned` widget is specially helpful for **animations**, 
since you can just calculate the final position and size you want for each frame. 
Without it you may find yourself having to animate a composition of widgets.

## How it works 

Add align_positioned [as a dependency](https://pub.dartlang.org/packages/align_positioned#-installing-tab-) 
in your `pubspec.yaml` file,
then import it:

    import 'package:align_positioned/align_positioned.dart';

Pass the `AlignPositioned` a `child`, and then one or more of the following parameters:
 
    AlignPositioned(
       child: child,           
       alignment: ...,
       dx: ...,
       dy: ...,
       moveByChildWidth: ...,
       moveByChildHeight: ...,
       moveByContainerWidth: ...,
       moveByContainerHeight: ...,
       childWidth: ...,
       childHeight: ...,
       minChildWidth: ...,
       minChildHeight: ...,
       maxChildWidth: ...,
       maxChildHeight: ...,
       childWidthRatio: ...,
       childHeightRatio: ...,
       minChildWidthRatio: ...,
       minChildHeightRatio: ...,
       maxChildWidthRatio: ...,
       maxChildHeightRatio: ...,
       wins: ...,
       touch: ...,       
       ); 
   
Let's study each parameter in detail:
        
## Align and Position parameters

The `alignment` parameter works as expected. For example, 
`Alignment.bottomRight` represents the bottom right of the container, 
and `Alignment(0.0, 0.0)` represents the center of the container. 
The distance from -1.0 to +1.0 is the distance from one side of the rectangle 
to the other side of the rectangle. 

If `touch` is `Touch.inside`, then `alignment` works just like the alignment 
for the `Align` widget, aligning the child inside of the container. 

However, if `touch` is `Touch.outside`, then the alignment happens outside of 
the container. 

As another example, if `touch` is `Touch.inside`, then `Alignment(1.0, 0.0)` makes the child's
right side touch the right side of the container (it touches the container from the **inside**). 

But if `touch` is `Touch.outside`, then `Alignment(1.0, 0.0)` makes the child's 
left side touch the right side of the container (it touches the container from the **outside**).

Parameters `dx` and `dy` can be positive or negative, and move the child horizontally and 
vertically, in pixels.

Parameters `moveByChildWidth` and `moveByChildHeight` can be positive or negative, and move the child 
horizontally and vertically, but the unit here is not pixels, but child widths and heights. 

Parameters `moveByContainerWidth` and `moveByContainerHeight` can be positive or negative, and move the child 
horizontally and vertically, but the unit here is not pixels, but container widths and heights.

## Align and Position Examples

The below image shows the center of the child positioned 15 pixels to the right 
of the top-left corner of the container: 

![alt text](./example/alignPos1.png)
  
    AlignPositioned(
       child: child,        
       alignment: Alignment.topLeft,
       touch: Touch.inside,
       dx: 15.0, // Move 4 pixels to the right. 
       moveByChildWidth: -0.5, // Move half child width to the left.  
       moveByChildHeight: -0.5); // Move half child height to the top.
       
Then, to move the child one container width to the right, and one container height to the bottom: 

![alt text](./example/alignPos2.png)
  
    AlignPositioned(
       child: child,        
       alignment: Alignment.topLeft,
       touch: Touch.inside,
       dx: 15.0, // Move 4 pixels to the right. 
       moveByChildWidth: -0.5, // Move half child width to the left.  
       moveByChildHeight: -0.5, // Move half child height to the top.
       moveByContainerWidth: 1.0, // Move one container width to the right.
       moveByContainerHeight: 1.0); // Move one container height to the bottom.               

Please, check the [example tab](https://pub.dartlang.org/packages/align_positioned#-example-tab-)
for the effects seen below:

![alt text](./example/alignPos3.png)

## Size Parameters

Optionally, you can also define the child size:

- `childWidth` is the child width, in pixels.

- `childHeight` is the child height, in pixels.

- `minChildWidth` is the minimum width, in pixels. It has precedence over `childWidth`.  

- `minChildHeight` is the minimum height, in pixels. It has precedence over `childHeight`.

- `maxChildWidth` is the maximum width, in pixels. It has precedence over `childWidth`.

- `maxChildHeight` is the maximum height, in pixels. It has precedence over `childHeight`.

- `childWidthRatio` is the child width, as a fraction of the container width.
   If between 0.0 and 1.0, the child will be smaller than its container.
   If more than 1.0, the child will be larger than its container. 
   You cannot define both `childWidthRatio` and `childWidth` at the same time.

- `childHeightRatio` is the child height, as a fraction of the container height.
   If between 0.0 and 1.0, the child will be smaller than its container.
   If more than 1.0, the child will be larger than its container. 
   You cannot define both `childHeightRatio` and `childHeight` at the same time.

- `minChildWidthRatio` is the minimum child width, as a fraction of the container width. 
   It has precedence over `childWidth`. If both `minChildWidth` and `minChildWidthRatio` 
   are defined, both will be applied (the minimum will be the larger one). 

- `minChildHeightRatio`. is the minimum child height, as a fraction of the container height. 
   It has precedence over `childHeight`. If both `minChildHeight` and `minChildHeightRatio` 
   are defined, both will be applied (the minimum will be the larger one).

- `maxChildWidthRatio` is the maximum child width, as a fraction of the container width. 
   It has precedence over `childWidth`. If both `maxChildWidth` and `maxChildWidthRatio` 
   are defined, both will be applied (the maximum will be the smaller one). 

- `maxChildHeightRatio` is the maximum child height, as a fraction of the container height. 
   It has precedence over `childHeight`. If both `maxChildHeight` and `maxChildHeightRatio` 
   are defined, both will be applied (the maximum will be the smaller one).

- `wins` decides what happens if the minimum size is larger then the maximum size.
   If `wins` is `Wins.min`, the default, the minimum size will be used.  
   If `wins` is `Wins.max`, the maximum size will be used.




