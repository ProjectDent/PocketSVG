# PocketSVG
An Objective-C class that converts Scalable Vector Graphics (SVG) into:
* CGPaths
* CAShapeLayers
* UIBezierPaths

This makes it easy to create vector-based paths and shapes in your iOS apps. 

Feedback, improvements, and pull requests are welcome.

## Usage
Drop PocketSVG.h, PocketSVG.m, HTMLNode.h, HTMLNode.m, HTMLParser.h and HTMLParser.m into an XCode project.

In the project settings add "/usr/include/libxml2" to the "header search paths" field.

Ctrl Click the Frameworks group choose Add -> Existing Frameworks and from the list choose "libxml2.dylib".

1. Make your drawing in a vector graphics editor such as Illustrator, Inkscape, [Sketch](http://www.bohemiancoding.com/sketch/), etc.
2. Save as an SVG.
3. Drag and drop it into your Xcode project.
4. Follow these easy steps:

```obj-c
    //1: Turn your SVG into a CGPath:
    PocketSVG *pocketSVG = [[PocketSVG alloc] initWithSVGFileNamed:@"BezierCurve1"];

	//2: Scale it by using scale, or the scaleToFitSize: helper method. Add borderPadding to half of your intended lineWidth, so the lineWidth doesn't end in an image bigger than you wanted.
	pocketSVG.borderPadding = 2;
	pocketSVG.scale = [pocketSVG scaleToFitSize:CGSizeMake(100, 100)];
    
    //3: To display it on screen, you can create a CAShapeLayer
    //and set [pocketSVG bezierPath].CGPath as its path property:
    CAShapeLayer *myShapeLayer = [CAShapeLayer layer];
    myShapeLayer.path = [pocketSVG bezierPath].CGPath;
    
    //4: Fiddle with it using CAShapeLayer's properties:
    myShapeLayer.strokeColor = [[UIColor redColor] CGColor];
    myShapeLayer.lineWidth = 4;
    myShapeLayer.fillColor = [[UIColor clearColor] CGColor];

    //5: Display it!
    [self.view.layer addSublayer:myShapeLayer];
```

## Useful Documentation
* [The 'path' element of an SVG](http://www.w3.org/TR/SVG/paths.html#PathElement) – from the SVG specification. PocketSVG uses the data in the SVG's **d=** attribute, which defines the outlines of shapes. 
* [Core Graphics Paths](https://developer.apple.com/library/mac/documentation/graphicsimaging/Conceptual/drawingwithquartz2d/dq_paths/dq_paths.html#//apple_ref/doc/uid/TP30001066-CH211-TPXREF101) – from Apple's Quartz 2D Programming Guide.
* [CGPath](https://developer.apple.com/library/mac/documentation/graphicsimaging/reference/CGPath/Reference/reference.html) - Class Reference.
* [CAShapeLayers](https://developer.apple.com/library/mac/#documentation/GraphicsImaging/Reference/CAShapeLayer_class/Reference/Reference.html) – Class Reference. Tells you which properties of the shape/path can be manipulated. 
* [Drawing Shapes Using Bezier Paths](http://developer.apple.com/library/ios/#documentation/2ddrawing/conceptual/drawingprintingios/BezierPaths/BezierPaths.html) – From Apple's Drawing and Printing Guide for iOS.

## Latest Fixes
* PocketSVG is now on CocoaPods!
* Created factory methods to obtain `CGPaths`.
* Added support for NSBezierPaths (thanks to [mcianni](https://github.com/mcianni)).
* Fixed problem that causes SVGs to render with wrong frame dimensions.
* Fixed problem that causes some SVGs to render incorrectly.
* Fixed parse bug for SVGs with blank spaces in them (thanks to [mindbrix](https://github.com/mindbrix)).
* Simplified PocketSVG's init method (thanks to [johnnyknox](https://github.com/johnnyknox)).

## To Do
* Support for SVG's [Basic Shapes](http://www.w3.org/TR/SVG/shapes.html), outside of Rects.
* Improve parser efficiency.

## Support
Please ask questions and report bugs on [the project's Issues Page](https://github.com/arielelkin/PocketSVG/issues). 

## Contributors
* Martin Haywood (for the original [SVG to bezier path parser](http://ponderwell.net/2011/05/converting-svg-paths-to-objective-c-paths/) PocketSVG is based on).
* [Ariel Elkin](http://www.github.com/arielelkin)
* [Pieter Omvlee](http://www.bohemiancoding.com/)
* Dominic Mortlock
* [mcianni](https://github.com/mcianni)
* [mindbrix](https://github.com/mindbrix)
* [johnnyknox](https://github.com/johnnyknox)
* [JagieChen](https://github.com/JagieChen)

## External Libraries
PocketSVG uses [HTMLParser](https://github.com/zootreeves/Objective-C-HMTL-Parser) to parse SVG strings for rectangles.

## License

Copyright (c) 2013 Ponderwell, Ariel Elkin, and Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

