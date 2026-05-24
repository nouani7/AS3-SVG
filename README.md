
**AS3 SVG — ActionScript 3 SVG Rendering Library**

AS3 SVG is a pure ActionScript 3 library for parsing and rendering SVG files in Adobe AIR and Flash Player applications.  
It is built on top of the native Flash Display List and provides asynchronous rendering for smooth performance, even with large SVG documents,


### ✨ Key Features

*It supports a wide subset of SVG 1.1 along with several SVG 2.0 features.*


### 📥 SVG Loading

 - [x] Load SVG from URL or local file path
 - [x] Load SVG from Raw SVG string
 - [x] Load SVG from XML object

### ⚡ Performance
- Asynchronous parsing (non-blocking rendering)
- Full Display List-based rendering (no rasterization required)

### 🎨 SVG Support
- Core elements:
  - `path`, `rect`, `circle`, `ellipse`, `line`, `polygon`, `polyline`
  - `text`, `tspan`, `image`
  - `g`, `defs`, `use`, `symbol`, `switch`, `a`

### 🌈 Gradients
- Linear gradients
- Radial gradients
- Supports `spreadMethod` and `gradientTransform`

### 🎭 Filters (limited support)
- `feGaussianBlur`
- `feColorMatrix`

### 🔄 Transform Support
- `translate`, `scale`, `rotate`, `skewX`, `skewY`, `matrix`

### 📐 Layout Features
- `viewBox`
- `preserveAspectRatio`

### 🎨 Styling Support
- CSS class selectors
- Inline styles

### 📏 Unit Support
- `px`, `pt`, `pc`, `mm`, `cm`, `in`
- `em`, `rem`
- `vw`, `vh`, `%`

### 🧠 Runtime Features

- Dynamic style modification
- Runtime element access and manipulation

---

### 📁 Installation

####  ⚡In Flash/Animate:

File → Publish Settings → ActionScript Settings → Library Path → Add → MXSVGLib.swc

---

### 🚀 Quick Start

### ⚠️ Important: Initialize `SVGDocument.setup(stage);` before using `SVGDocument`.

```actionscript
    import com.mx.SVG.display.SVGDocument;
    import com.mx.SVG.events.SVGEvent;
    
    // Initialize async engine (once per app)
    SVGDocument.setup(stage);
    
    // Create SVG document
    var svg:SVGDocument = new SVGDocument();
    addChild(svg);
    
    // Events
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
```

### 📥Loading Methods

> From URL / File Path
```actionscript
    svg.load("assets/logo.svg");
    svg.load(new URLRequest("assets/logo.svg"));
```
> From Raw SVG String
```actionscript
    var svgString:String =
        '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200">' +
        '  <circle cx="100" cy="100" r="80" fill="#FF6B6B"/>' +
        '</svg>';
    
    svg.parse(svgString);
    
```
> From XML Object
```actionscript
    var svgXML:XML =
        <svg xmlns="http://www.w3.org/2000/svg" width="200" height="200">
            <rect x="10" y="10" width="180" height="180" fill="#4ECDC4"/>
        </svg>;
    
    svg.parse(svgXML);
    
```
---

### 🎯 SVG Events

| Event             | Description                   |
| ----------------- | ----------------------------- |
| `PARSE_START`     | Parsing process begins        |
| `PARSE_COMPLETE`  | SVG tree fully parsed         |
| `RENDERED`        | First render completed        |
| `ELEMENT_ADDED`   | Element added to document     |
| `ELEMENT_REMOVED` | Element removed from document |

> Registering event listeners

```actionscript
svg.addEventListener(SVGEvent.PARSE_START, onParseStart);
svg.addEventListener(SVGEvent.PARSE_COMPLETE, onParseComplete);
svg.addEventListener(SVGEvent.RENDERED, onRendered);
```

> Event handlers

```actionscript
function onParseStart(e: SVGEvent): void
{
	trace("Parsing started...");
}

function onParseComplete(e: SVGEvent): void
{
	trace("Parsing completed — Elements:", svg.numChildren);
}

function onRendered(e: SVGEvent): void
{
	trace("Rendering completed.");
}
```
---

### ⚙️ Core Features

> 📏 Document Scaling
```actionscript
    var scale:Number = Math.min(
        stage.stageWidth / svg.width,
        stage.stageHeight / svg.height
    );
    svg.scaleX = svg.scaleY = scale;
```

---

### 🔎 Runtime Element Access

```actionscript
    import com.lorentz.SVG.display.base.SVGElement;
    var element:SVGElement = svg.getDefinition("myElement");
```

---

### 🎨 Modify Styles Dynamically
```actionscript
    element.style.setProperty("fill", "#00FF00");
    element.invalidateStyle();
```
---

### 🔄 Apply Transforms
```actionscript
    element.svgTransform = "translate(50, 20) scale(1.5)";
```
---

### ⚡ Performance Optimization
```actionscript
    svg.validateWhileParsing = false;
```
> Disables progressive rendering for better performance on large SVG> files.

---

### 🧹 Cleanup

```actionscript
    svg.clear();
    removeChild(svg);
    svg = null;
```
---

### 🖋️ Text Rendering

> FTESVGTextDrawer	→ High-quality rendering (default) 
> TextFieldSVGTextDrawer	→ Lightweight alternative

```actionscript
    svg.textDrawerClass = TextFieldSVGTextDrawer;
```
---

### Global Font Override

```actionscript
    svg.changeTextFormatFunction = function(fmt:SVGTextFormat):void {
        fmt.font = "MyEmbeddedFont";
    };
```
    
---

### 📊 Supported SVG Elements

 - [x] Shapes: rect, circle, ellipse, line, polygon, polyline, path
 - [x] Structure: svg, g, defs, use, symbol, switch
 - [x] Text: text, tspan
 - [x] Images: image
 - [x] Paint: gradients & patterns
 - [x] Filters: basic support
 - [x] Clipping: clipPath, mask
 - [x] Metadata: title, desc
---

### 🎨 Supported CSS Properties

 - [x] fill, stroke, opacity
 - [x] stroke-width, stroke-linecap, stroke-linejoin
 - [x] font-size, font-family, text-anchor
 - [x] visibility, display
 - [x] filter, marker

---

### 📦 Requirements

| Requirement        | Version |
|--------------------|--------|
| Adobe AIR SDK      | 3.0+ (tested up to 51.x) |
| Flash Player       | 11.0+ |
| ActionScript       | 3.0 |

---

### ⚠️ Limitations

 - No SMIL animation support
 - No JavaScript inside SVG
 - Limited filter support
 - No <foreignObject> support
 - No advanced CSS selectors (only class and ID selectors)
