## Basic Responsive Design Principles

1. **FLUID GRIDS AND LAYOUTS**
To allow content to easily adapt to the current viewport width used to browse the website. Uses **%** rather than **px** for all layout-related things.

2. **FLEXIBLE/RESPONSIVE IMAGES**
Images behave differently than text content, and so we need to ensure that they also adapt nicely to the current viewport. Make images flexible by defining their dimensions in percentages rather than fixed units like pixels. Images usually make up the biggest part of our website's size, in terms of megabytes, and so we should optimize the images for different width.

3. **MEDIA QUERIES**
To change styles on certain viewport widths (breakpoints), allowing us to create different version of our website for different widths.

#### LAYOUT TYPES
Three major ways of laying out a webpage or app.
1. **Float Layouts (OLD)**
Simply put a bunch of boxes side by side using floats.
2. **Flexbox**
Offers an amazing way of laying out elements in a one dimensional row.
3. **CSS GRID**
Is perfect for creating the overall layout of a page in a fully-fledged 2D grid.

### CSS Architecture
**7-1 Pattern**: 7 folders and one main SASS file to import all the files that are in these folders.

* **base folder**: Which is where we're going to put our basic projects definitions as project boilerplate.
  * Base partial (_base.scss): This file will be for the real low level basics, such as resets and styles. This file should be a partial. Partial files always start with an underscore.
  * Animations, typography, utilities partials.
* **abstract folder**: We're only going to put code that's not going to output any CSS: Variables, mixins, functions and stuff like that.
* **components folder**: We're going to create one file for each component. Components: Reusable building blocks that make up our website, which are independent and reusable everywhere across our website.
* **layout folder**: For each piece of the global layout of the entire project (global footer, header, etc).
* **page folder**: Specific styles for a specific page.
* **themes folder**: For web apps with different themes.
* **vendors folder**: Where we can put third party CSS (i.e bootstrap, icon system, animation framework).

## Cascade and Specificity
Process of combining different style sheets and resolving conflicts between different CSS rules and declarations, when more than one rule applies to a certain element.

### Author Declarations
CSS that we the developers write, declarations that we put in style sheets are called Author Declarations

### User Declarations
CSS coming from the user, i.e. When the user changes the font size in the browser, then this is User CSS.

### Browser Declarations (User Agent)
Default style in elements, i.e. anchor tag (blue and underline)

### IMPORTANCE > SPECIFICITY > SOURCE ORDER

### IMPORTANCE
1. User !important declarations.

2. Author !important declarations.

3. Author declarations.

4. User declarations.

5. Default browser declarations.

Same importance? ->

### SPECIFICITY
1. Inline styles.

2. IDs.

3. Classes, pseudo-classes, attribute.

4. Elements, pseudo-elements.

Same specificity? ->

### SOURCE ORDER
The last declaration in the code will override all other declarations and will be applied.

Notes:
* Only use !important as a last resource. It's better to use correct specifies - more maintainable code!.
* The universal selector * has no specificity value (0,0,0,0).
* Rely more on specificity than on the order of selectors.
* But, rely on order when using 3rd-party style sheets -- always put your author style sheet last.

## Value Processing
CSS Engine converts relative units to pixels.

REM -> Relative , i.e. 1.5 rem means 1.5 times the default size

|   | Source  | Example(x) | How to convert to pixels | Results in pixel |
| - | --------| -----------| ------------------------ | ---------------- |
| % (fonts)   | 16px | 150% | x% * parent computed font size | 24px |
| % (lengths) | 1000px | 10% | x% -> parent computed font size | 100px |
| em (fonts) | 24px | 3em | x * parent computed font size | (24px*3) = 72px |
| em (length) | 24px | 2em | x * current element computed font size | (24px*2) = 48px |
| rem | 16px  | 10rem | x * root computed font size | (16px*10) = 24px |
| vh  |   | 90vh  | x * 1% of viewport height  | 90% of the current viewport height |
| vw  |   | 80vw  | x * 1% of viewport width   | 90% of the current viewport width |

Notes:
* em - rem are font-based.
* vh (viewport-height) - vw(viewport-width)  are viewport-based.

Why should we actually size stuff with ems and rems if they are based on font-size?
We can build more robust responsive layouts because just by changing font sizes, we will automatically change length since it depend on a font size. That gives us a lot of flexibility.

Notes:
* Each property has an initial value, used if nothing is declared ( and if there is no inheritance).
* Browsers specify a root font-size for each page (usually 16px - user agent definition).
* Percentages and relative values are always converted to pixels.
* Percentages are measured relative to their parent's font-size, if used to specify font-size.
* Percentages are measured relative to their parent's width, if used to specify lengths.
* em are measured relative to their parent font-size, if used to specify font-size.
* em are measured relative to the current font-size, if used to specify lengths.
* rem are always measured relative to the document's root font-size.
* vh and vw are simply percentage measurements of the viewports height and width.

## Inheritance
* Inheritance passes the values for some specific properties from parents to children - more maintainable code.
* Properties related to text are inherited. font-family, font-size, color, etc.
* Inheritance of a property only works if no one declares a value for that property.
* The inherit keyword forces inheritance on a certain property.
* The initial keyword resets a property to its initial value.

## Visual Formatting Model
Algorithm that calculates boxes and determines the layout of theses boxes, for each element in the render tree, in order to determine the final layout of the page.

In order to do this, the algorithm takes into account
* Dimensions of boxes: the box model.
* Box type: inline, block and inline-block.
* Positioning scheme: floats and positioning. (absolute - relative)
* Stacking contexts.
* Other elements in the render tree.
* Viewport size, dimensions of images, etc.

### The Box Model
* Content
* Padding
* Border
* Margin
* Fill area: area that gets filled with background color or background image.

#### Heights and Widths
Total width: right border + right padding + specified width + left padding + left border
Total height: top border + top padding + specified height + bottom padding + bottom border

Solution:
box-sizing: border-box;

#### Box Types: Inline, Block-Level and Inline-Block

#### Block-level Boxes
* Elements formatted visually as blocks.
* 100% of parent's width.
* Vertically, one after another.
* Box-model applies as showed:

i.e. display: block, flex, list-item, table;

#### Inline Boxes
* Content is distributed in lines.
* Occupies only content's space.
* No line-breaks.
* No heights and widths.
* Paddings and margins only horizontal (left and right).

i.e. display: inline;

#### Inline-block Boxes
* A mix of block and inline.
* Occupies only content's space.
* No line-breaks.
* Box-model applies as showed.

i.e. display: inline-block;