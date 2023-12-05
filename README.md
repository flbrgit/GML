# Glorious Markup Language

The Glorious Markup Language is a programming language designed for Pygame Surfaces, originally written for a personal project called 'Glorious City'. Its syntax is similar to html and xml. For that reason, it is simple to write and read. The file extension is *.gml for standard. It was designed to implement surfaces that consist of images and text together (also in one line) what is not possible in pure pygame.



-----------------------------------------------------------------------------------------------------------

## Installation

You can install GML from PyPI:

    pip install glorious-markup-language

GML is supported on Python 3.5 or higher and Pygame 2.0 or higher.


### Implementation

    from GML.gml import PARSER

    parser = PARSER(max_width=500, font_path="fonts")

    code_lines, width, height = parser.init(data, images)

    surface = parser.parse(code_lines, images, background, width, height)

 
The GML-Parser is implemented in a module called TEXT.


The 'txt'-Parameter is the GML-Code as string. 'images' is a dictionary with all image names given in 'src' attributes of img-tags as keys and their corresponding 'pygame.Surface' object. 'background' is a surface that is used to render the code. 'font_path' is the path to the required fonts, named 'italic.ttf', 'bold.ttf', 'bold-italic.ttf' and 'normal.ttf'.

The init-method returns a list of code-lines that can be parsed. That list can be split (like in the example below) and modified.

NOTE: Parsing bigger files can last more than 50 Milliseconds. To avoid lower framerate, it is recommended to use threads.

-----------------------------------------------------------------------------------------------------------

## Features
Example with multiple code elements adopted from Civilization VI:

<img src="https://github.com/flbrgit/GML/assets/92446154/57aecb7a-d26b-4439-af46-a477b85e4f42" width="500" />

**Code:**
```
<p><style size="80" color="black" align="center"/>Ice Hockey Rink</p>
<p><style size="60" color="black" align="center"/>Description</p>
<p><style size="40" color="black"/>
    Unlocks the Builder ability to construct an Ice Hockey Rink, unique to Canada.
</p><p><style size="40" color="black"/>
    +1 <img src="amenity"/> Amenity. +1 <img src="culture"/> Culture for each adjacent Tundra, Tundra Hills, 
    Snow, and Snow Hills tile. Provides <img src="tourism"/> Tourism from Culture once Flight is unlocked. 
    +2 <img src="food"/> Food and <img src="production"/> Production once the Professional 
    Sports civic is unlocked. +4 <img src="culture"/> Culture if adjacent to a Stadium building. Can be built on Tundra, 
    Tundra Hills, Snow, and Snow Hills. One per city. +2 Appeal.
</p>
<p><style size="20" color="black"/></p>
<p><style size="60" color="black" align="center"/>Traits</p>
<p><style size="10" color="black"/></p>
<p><style size="40" color="black"/>Appeal to Adjacent Tiles: 2</p>
<p><style size="40" color="black"/>+2 <img src="production"/> Production (requires Professional Sports)</p>
<p><style size="40" color="black"/>+2 <img src="food"/> Food (requires Professional Sports)</p>
<p><style size="10" color="black"/></p>
<p><style size="50" color="black"/>Adjacency Bonus</p>
<p><style size="10" color="black"/></p>
<p><style size="40" color="black"/>+1 <img src="culture"/> Culture from each adjacent Tundra tile.</p>
<p><style size="40" color="black"/>+1 <img src="science"/> Science from each adjacent Tundra (Hills) tile.</p>
<p><style size="40" color="black"/>+1 <img src="faith"/> Faith from each adjacent Snow tile.</p>
<p><style size="40" color="black"/>+3 <img src="food"/> Food if adjacent to a city center.</p>
<p><style size="40" color="black"/>+3 <img src="production"/> Production if adjacent to a city center.</p>
<p><style size="10" color="black"/></p>
```


___________________________

#### Programming GML

GML can parse seven different tag names. Five of them are line-tags, which mean tags that display a line, and two style-tags that can change the style of a given line. The five line-tags are:

-    `h3`: Tag for headlines, with the biggest size (usually 30 pixels)

-    `h2`: Tag for headlines with the second biggest size                       (usually 25 pixels)

-    `h1`: Tag for the smallest headline, usually 20 pixels.

-    `p`: Tag for a simple line

-    `li`: Tag for an enumeration

The advantage of headlines is that they are automatically underlined. Of course, all tags can be modified with style-tags, which are:

-    `<img>`  : Tag representing an image

-    `<style>`: Tag containing explicit style attributes for the given line

NOTE: Style-tags are written inside of line-tags.

 

The Style-Tag can have several attributes:

- **color**  :  Sets the color of a line. This can either be a name (e.g. “white”) or an RGB-Value (e.g. (0,1,2)).

    **NOTE**: The RGB-Values have to be written without any spaces; else a Syntax Error is raised.

    `Example: <style color="white"/>`

-  **type**  : Sets the displayed text to italic, normal, bold or bold-italic.


    `Example: <style type="bold"/>`

-  **align**  : Sets align of the displayed text to left, right or center.

    `Example: <style align="center"/>`

-   **size**  : Sets the size of the displayed text in pixels.

    `Example: <style size="50"/>`

-  **antialias**  : Sets the antialiasing property of the text (Rarely used).

    `Example: <style antialias="True"/>`

-  **display**  : Displays the text either 'underline' or 'standard'.

    `Example: <style display="underline"/>`

-  **marked**  : Marks the text with the specified color.

    `Example: <style marked="(0,0,0)"/>`


----------------------------------------------------


**Example:**

Example with multiple code elements

<img src="https://user-images.githubusercontent.com/92446154/137142744-886e0dd3-25bc-46a8-bdb1-ba594bfcb0d7.png" width="600"/>


**Code:**

```
<p><style size="40" color="black" align="center"/>City Center</p>
<p><style size="30" color="black" align="center"/>Description</p>
<p><style size="20" color="black"/>
    This is the center of the city.
</p>
<p><style size="20" color="black"/>
    +1 <img src="science"/> Science and 
    <img src="culture"/> Culture. Condition for all other 
    buildings in the city. Can only be build by a
    <img src="settler"/>Settler. Increases population 
    limit by 20 <img src="people"/> Inhabitants. 
    +1 <img src="faith"/> Faith for each adjacent 
    mountain. +1 <img src="science"/> Science and 
    <img src="culture"/> Culture for every age since 
    antiquity. +10 <img src="economy"/> Coins 
    with Goetz the Niggard as leader. Can produce simple 
    units. +1 <img src="power"/> power per turn.
</p>
<p><style size="10" color="black"/></p>
<p><style size="30" color="black" align="center"/>Traits</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+1 <img src="culture"/> Culture</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+1 <img src="science"/> Science</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+1 <img src="power"/> Power</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+20 <img src="people"/> limit for Inhabitants</p>
<p><style size="5" color="black"/></p>
<p><style size="25" color="black"/>Adjacency Bonus</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+1 <img src="faith"/> Faith for each adjacent mountain</p>
<p><style size="5" color="black"/></p>
<p><style size="25" color="black"/>Time Bonus</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+1 <img src="science"/>
    Science for every age since antiquity
</p>
<p><style size="5" color="black"/></p>
<p><style size="20" color="black"/>+1 <img src="culture"/>
    Culture for every age since antiquity
</p>
<p><style size="5" color="black"/></p>`
```
________________________________

## Requirements

- Python 3.5 or higher
- Pygame 2.0.0 or higher

## Release Notes

### 1.0.6

Initial release of GML
"# GML" 
"# GML" 
