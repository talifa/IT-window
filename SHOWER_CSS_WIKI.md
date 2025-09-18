# Shower Presentation Engine - CSS Classes & Structure Wiki

## Table of Contents
- [Core Architecture](#core-architecture)
- [Main Container Classes](#main-container-classes)
- [Slide Structure](#slide-structure)
- [Content Elements](#content-elements)
- [Layout Components](#layout-components)
- [Interactive Elements](#interactive-elements)
- [Modifiers & States](#modifiers--states)
- [Theme-Specific Elements](#theme-specific-elements)
- [CSS Custom Properties](#css-custom-properties)

## Core Architecture

### Main HTML Structure
```html
<body class="shower list">
  <header class="caption">...</header>
  <section class="slide" id="unique-id">...</section>
  <footer class="badge">...</footer>
  <div class="progress"></div>
  <script src="shower.js"></script>
</body>
```

## Main Container Classes

### `.shower`
The root container class that wraps the entire presentation.

**States:**
- `.shower.list` - Grid view showing all slides as thumbnails
- `.shower.full` - Fullscreen presentation mode
- `.shower.pointless` - Hides mouse cursor during presentation
- `.shower.grid` - Shows grid overlay in fullscreen (debug mode)

**Key Properties:**
- Defines CSS custom properties for slide dimensions
- Sets up color scheme variables
- Controls font family and text sizing

## Slide Structure

### `.slide`
The fundamental building block - each slide is a `<section>` with this class.

**Core Properties:**
- Fixed dimensions: 1024px × 576px (16:9 ratio by default)
- Padding: 75px on sides, 0 on top
- White background
- Automatic numbering via CSS counters

**Common Pattern:**
```html
<section class="slide" id="unique-slide-id">
  <h2>Slide Title</h2>
  <p>Content...</p>
</section>
```

### Slide States
- `.slide.active` - Currently visible slide in fullscreen
- `.slide:hover` - Hovered slide in list view
- `.slide.clear` - Removes slide number and progress bar

## Content Elements

### Text Content Classes

#### `.shout`
Large, centered text for emphasis.
```html
<h2 class="shout">Big Statement</h2>
<h2 class="shout shrink">Animated shrink effect</h2>
<h2 class="shout grow">Animated grow effect</h2>
```
**Properties:**
- 150px font size
- Absolute positioning, centered
- Animation support for grow/shrink effects

#### `.note`
Small annotation text, typically used for footnotes or additional info.

### Code Elements

#### Code Block Structure
```html
<pre>
  <code>Line 1 of code</code>
  <code class="mark">Highlighted line</code>
  <code class="mark next">Progressive reveal line</code>
</pre>
```

**Code Modifiers:**
- `.mark` - Highlights code line with yellow background
- `.mark.important` - Red background for critical code
- `.mark.next` - Progressive disclosure for code lines
- `.comment` - Gray text for code comments

### Media Elements

#### `.cover`
Full-slide background images or videos.
```html
<img class="cover" src="image.jpg" alt="Description">
<img class="cover w" src="image.jpg" alt="Full width">
<img class="cover h" src="image.jpg" alt="Full height">
```

**Cover Modifiers:**
- `.cover.w` or `.cover.width` - Force full width
- `.cover.h` or `.cover.height` - Force full height

#### `.copyright`
Image attribution positioned in corners.
```html
<figcaption class="copyright right white">
  <a href="source">© Author Name</a>
</figcaption>
```

**Copyright Positions:**
- `.copyright` - Default: bottom-right, rotated
- `.copyright.top` - Top-left corner
- `.copyright.bottom` - Bottom-left corner
- `.copyright.right` - Bottom-right corner
- `.copyright.white` - White text for dark backgrounds

## Layout Components

### `.columns`
Grid-based column layouts.
```html
<div class="columns two">
  <p>Left column</p>
  <p>Right column</p>
</div>
```

**Column Options:**
- `.columns.two` - 2-column grid
- `.columns.three` - 3-column grid  
- `.columns.four` - 4-column grid

### `.caption`
Presentation title and metadata, visible only in list view.
```html
<header class="caption">
  <h1>Presentation Title</h1>
  <p>Author Name, Company</p>
</header>
```

### `.badge`
"Fork me on GitHub" style badge, bottom-right corner.
```html
<footer class="badge">
  <a href="https://github.com/user/repo">Fork me on GitHub</a>
</footer>
```

### `.progress`
Animated progress bar showing presentation progress.
```html
<div class="progress"></div>
```
**Behavior:**
- Hidden in list view
- Visible in fullscreen mode
- Width changes based on slide progress
- Blue color with skewed design

## Interactive Elements

### `.next`
Progressive disclosure - elements appear one by one during presentation.
```html
<ul>
  <li>Always visible</li>
  <li class="next">Appears on first click</li>
  <li class="next">Appears on second click</li>
</ul>
```

**States:**
- `.next` - Hidden until activated
- `.next.active` - Currently being revealed
- `.next.visited` - Previously revealed, now visible

## Modifiers & States

### Slide Background Modifiers
- `.slide.black` - Black background
- `.slide.gray` - Gray background
- `.slide.clear` - Removes slide number and progress

### Animation States
- `.active` - Currently active/visible element
- `.visited` - Previously activated element
- `.grow` - Grow animation for shout elements
- `.shrink` - Shrink animation for shout elements

### List vs Full Mode Behavior
Many elements behave differently based on presentation mode:

**List Mode (`.shower.list`)**:
- Shows all slides in grid
- Caption and badge visible
- Progress bar hidden
- Slides scaled down (25%, 50%, or 100% based on viewport)

**Full Mode (`.shower.full`)**:
- Single slide centered and scaled
- Caption and badge hidden
- Progress bar visible
- Interactive animations enabled

## Theme-Specific Elements

### Ribbon Theme Specifics
- Blue color scheme (`--color-blue: #4b86c2`)
- Ribbon-style slide numbers with SVG background
- PT Sans font family
- Skewed progress bar design

### CSS Custom Properties (Variables)
```css
.shower {
  --slide-ratio: calc(16 / 9);
  --slide-width: 1024px;
  --slide-height: calc(var(--slide-width) / var(--slide-ratio));
  --slide-side: 100px;
  --slide-gap: 100px;
  
  --color-blue: #4b86c2;
  --color-blue-lighter: #6799cb;
  --color-red: #cc0000;
  --color-yellow: #fafaa2;
  --color-grey: #585a5e;
  
  --ribbon-size: 50px;
  --progress-size: 10px;
}
```

## Responsive Behavior

### Breakpoints
- **Small screens** (`< 1174px`): `--slide-scale: 0.25`
- **Medium screens** (`1174px - 2347px`): `--slide-scale: 0.5` 
- **Large screens** (`≥ 2348px`): `--slide-scale: 1`

### Print Styles
- Hides progress bar, caption, and badge
- Optimizes for PDF export
- Maintains slide aspect ratio

## Usage Patterns

### Basic Slide Template
```html
<section class="slide">
  <h2>Slide Title</h2>
  <p>Regular paragraph content</p>
  <ul>
    <li>List item</li>
    <li class="next">Progressive item</li>
  </ul>
</section>
```

### Cover Slide Template
```html
<section class="slide" id="cover">
  <h2>Presentation Title</h2>
  <p>Subtitle or author</p>
  <figure>
    <img class="cover" src="background.jpg" alt="Background">
    <figcaption class="copyright right white">
      <a href="#">© Photo Credit</a>
    </figcaption>
  </figure>
</section>
```

### Code Slide Template
```html
<section class="slide">
  <h2>Code Example</h2>
  <pre>
    <code>&lt;!DOCTYPE html&gt;</code>
    <code class="mark">&lt;html lang="en"&gt;</code>
    <code class="mark next">&lt;head&gt;</code>
    <code>  &lt;title&gt;Title&lt;/title&gt;</code>
    <code class="mark next">&lt;/head&gt;</code>
  </pre>
</section>
```

This wiki serves as a comprehensive reference for all CSS classes and structural elements used in the Shower presentation engine. Use it to understand how to properly structure slides and apply styling classes for optimal presentation rendering.
