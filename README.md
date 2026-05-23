AS3 SVG — ActionScript 3 SVG Rendering Library

AS3 SVG is a pure ActionScript 3 library for parsing and rendering SVG files in Adobe AIR and Flash Player applications. It is built on top of the native Flash Display List and provides asynchronous rendering for smooth performance, even with large SVG documents.

It supports a wide subset of SVG 1.1 along with several SVG 2.0 features.

---

✨ Key Features

Load SVG from:

URL or local file path

Raw SVG string

XML object


Asynchronous parsing (non-blocking rendering)

Full Display List-based rendering (no rasterization required)

Supports major SVG elements:

path, rect, circle, ellipse, line, polygon, polyline

text, tspan, image

g, defs, use, symbol, switch, a


Gradients:

Linear gradients

Radial gradients

Supports spreadMethod and gradientTransform


Filters (limited support):

feGaussianBlur

feColorMatrix


Full transform support:

translate, scale, rotate, skewX, skewY, matrix


viewBox and preserveAspectRatio

CSS support:

Class selectors

Inline styles


Unit support:

px, pt, pc, mm, cm, in, em, rem, vw, vh, %


Runtime style modification

Dynamic element access and manipulation



---

📦 Requirements

Requirement	Version

Adobe AIR SDK	3.0+ (tested up to 51.x)
Flash Player	11.0+
ActionScript	3.0



---

📁 Installation

1. Copy the com/ folder into your project root:



MyProject/
├── MyProject.fla
└── com/
    └── lorentz/

2. Add the project root to your Classpath:



.


---

🚀 Quick Start

> ⚠️ Important: You must initialize ProcessExecutor before using any SVGDocument.



import com.lorentz.SVG.display.SVGDocument;
import com.lorentz.SVG.events.SVGEvent;
import com.lorentz.processing.ProcessExecutor;
import flash.net.URLRequest;

// Initialize async processing engine (once per application)
ProcessExecutor.instance.initialize(stage);

// Create SVG document
var svg:SVGDocument = new SVGDocument();
addChild(svg);

// Listen for events
svg.addEventListener(SVGEvent.PARSE_COMPLETE, onParseComplete);
svg.addEventListener(SVGEvent.RENDERED, onRendered);

// Load SVG
svg.load(new URLRequest("assets/icon.svg"));

function onParseComplete(e:SVGEvent):void {
    trace("SVG parsing completed");
}

function onRendered(e:SVGEvent):void {
    trace("SVG rendered:", svg.width, svg.height);
}


---

📥 Loading Methods

From URL or file path

svg.load("assets/logo.svg");
svg.load(new URLRequest("assets/logo.svg"));

From raw SVG string

var svgString:String =
    '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200">' +
    '  <circle cx="100" cy="100" r="80" fill="#FF6B6B"/>' +
    '</svg>';

svg.parse(svgString);

From XML

var svgXML:XML =
    <svg xmlns="http://www.w3.org/2000/svg" width="200" height="200">
        <rect x="10" y="10" width="180" height="180" fill="#4ECDC4"/>
    </svg>;

svg.parse(svgXML);


---

🎯 Events

Event	Description

PARSE_START	Parsing process begins
PARSE_COMPLETE	SVG tree is fully parsed
RENDERED	First render completed
ELEMENT_ADDED	Element added to document
ELEMENT_REMOVED	Element removed from document



---

⚙️ Core Features

Document scaling

var scale:Number = Math.min(
    stage.stageWidth / svg.width,
    stage.stageHeight / svg.height
);

svg.scaleX = svg.scaleY = scale;


---

Runtime element access

import com.lorentz.SVG.display.base.SVGElement;

var element:SVGElement = svg.getDefinition("myElement");


---

Modify styles dynamically

element.style.setProperty("fill", "#00FF00");
element.invalidateStyle();


---

Apply transforms

element.svgTransform = "translate(50, 20) scale(1.5)";


---

⚡ Performance Optimization

svg.validateWhileParsing = false;

Disables progressive rendering and improves performance for large SVG files.


---

🧹 Cleanup

svg.clear();
removeChild(svg);
svg = null;


---

🖋️ Text Rendering

Available backends

Class	Description

FTESVGTextDrawer	High-quality text rendering (default)
TextFieldSVGTextDrawer	Lightweight alternative


svg.textDrawerClass = TextFieldSVGTextDrawer;


---

Global font override

svg.changeTextFormatFunction = function(fmt:SVGTextFormat):void {
    fmt.font = "MyEmbeddedFont";
};


---

📊 Supported SVG Elements

Shapes: rect, circle, ellipse, line, polygon, polyline, path

Structure: svg, g, defs, use, symbol, switch

Text: text, tspan

Images: image

Paint: gradients & patterns

Filters: basic support

Clipping: clipPath, mask

Metadata: title, desc



---

🎨 Supported CSS Properties

fill, stroke, opacity

stroke-width, stroke-linecap, stroke-linejoin

font-size, font-family, text-anchor

visibility, display

filter, marker



---

⚠️ Limitations

No SMIL animation support

No JavaScript inside SVG

Limited filter support

No <foreignObject> support

No advanced CSS selectors (only class and ID selectors)

