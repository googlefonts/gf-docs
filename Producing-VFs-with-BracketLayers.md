# Producing VFs with "Bracket Layers"

*This workflow is only a temporary solution for typefaces where a glyph has more than one design across different ranges of the design space. It is intended to be used until fontmake has support for such designs.*

*See @m4rc1e’s [document](https://docs.google.com/document/d/1tba8iD40Mu-b1H15pUlFcI0sY5Lwdp8mOyxaR8q50qw) for the standard VF workflow, info on goals, related tools/docs, and known issues.*

<br>

## Tools/Scripts/Docs

### [Glyphs App VF Tutorial](https://glyphsapp.com/tutorials/creating-a-variable-font)
Useful tutorial on other aspects of exporting a variable font from Glyphs App

### [Bracket Layer Intro](https://glyphsapp.com/tutorials/alternating-glyph-shapes)
The Glyphs App documentation on bracket layers, sans info on use in a VF export. Contrary to what is said in the tutorial, in testing bracket layers [#] are active when *greater than *the number in brackets, and reverse bracket layers ]#] are active when *less than or equal to *the number in brackets

### [Check Brackets Script](https://github.com/mjlagattuta/Hepta-Slab/blob/master/sources/tools/Check-VF-Bracket-Layer-Setup.py)
A script to run on your source file to check that each master layer has a corresponding bracket layer

### [Generate Brackets Script](https://github.com/mjlagattuta/Hepta-Slab/blob/master/sources/tools/Add-VF-Bracket-Layers.py)
Script for adding bracket layers to glyphs with a component whose referenced glyph uses bracket layers

### [Fonttools](https://github.com/fonttools/fonttools)
Used to convert exported .ttf files to .ttx for manual addition of the avar table

### [OpenType Spec ‘avar’ Table](https://docs.microsoft.com/en-us/typography/opentype/spec/avar)
Documentation on the purpose of the ‘avar’ table and how it maps axes of multiple scales. The language around the mapping can be a bit confusing as with the "from" and “to” coordinates. “From” refers to the final intended input value and “to” refers to the value on the original scale that you want as output (i.e. a mapping of  from="0.0" to="-0.5"  will result in the outlines interpolating to 25% along the original scale but occurring at 50% along the user scale). Also worth noting, 0 is not an equal distance between -1 and 1, it instead refers to the default value described in the fvar table.

### [Fonttools Example ‘avar’ in .ttx](https://github.com/fonttools/fonttools/blob/master/Tests/varLib/data/test_results/BuildAvarSingleAxis.ttx)
Reference of xml structure for the avar table

### [Add ‘avar’ Script](https://gist.github.com/m4rc1e/6bce4997bf160938adf67486f46fcebe) (link may change)
@m4rc1e’s script for adding an ‘avar’ table based on .glyphs file and a variable font .ttf

### [Generate avar xml macro](https://github.com/googlefonts/robotoslab/blob/master/sources/tools/macros.txt)
A script for use in the Glyphs App macro panel to get an ‘avar’ xml patch

<br>

## Overview

A) Set up axes and custom parameters

B) For glyphs using the bracket technique, set up bracket layers for each master layer

C) On a duplicated file, run scripts to add bracket layers for components. Export the VF

D) In .ttx, correct fvar values, calculate avar mappings, and convert back to .ttf

F) Recommended post processing steps/scripts

G) Known issues and STAT patch for italic fonts

<br>

## Workflow

### A) Axes Setup

1. Add the custom parameter "Axis Location" on the lightest and boldest masters based on their intended css font weight. For the lightest this will most likely be “100” and for the boldest “900”

2. If you have 1–9 instance,  double check that their css weight values and names correspond to Google Fonts canonical naming. If you have more than 9 instances, the extra weights can be included in the VF as long as they fall on the scale in the OT spec (1-1000)

### B) Bracket Setup

1. The master layers of a glyph should represent the intended design at that point in the design space, even if the outlines are not compatible

2. If possible, on glyphs that use a bracket layer, but have one design (i.e. the bracket layer and master layers are all compatible), it is a good idea to use a brace layer instead. In the case of variable fonts, since changes are smooth, it is advisable to keep outlines from jumping unless necessary (as in the case of switching between two designs). Doing so also lowers file size as a brace layer adds more deltas but a bracket setup adds a new glyph with multiple sets of deltas.

3. Set up necessary bracket and reverse bracket layers. This will depend on the layer and its place in the design space. Weights lighter than or equal to the number in brackets should take regular bracket layers [#] and those bolder than it should take reverse bracket layers ]#]

4. Add interpolatable bracket layers for each master

    1. All glyphs that use the bracket trick to represent more than one form across the design space must have a bracket layer for each master and the groups of corresponding layers must all be compatible. Glyphs will treat each set of compatible layers as its own separate glyph (appending a suffix under the hood i.e. "R.varAlt01") and switch them out at the number specified on the bracket layers. (Even though these extra layers will hopefully not be rendered, I would recommend drawing them at the correct weight rather than copying and pasting from an existing bracket layer at a different weight; this way if the glyph is not switched out when intended, the result is at least the correct weight.)

    2. Script: [Check-VF-Bracket-Layer-Setup.py](https://github.com/mjlagattuta/Hepta-Slab/blob/master/sources/tools/Check-VF-Bracket-Layer-Setup.py)

### C) Export Setup

1. If the "Check-VF-Bracket-Layer-Setup.py" script raises no errors, then duplicate your .glyphs file, give it a sensible name, and use this new file for the rest of the process

2. While the number of glyphs needing bracket layers may be low and manageable, the current state of Glyphs App (as of 8/8/18) will not properly export components of these glyphs. To get the intended behavior, any components of glyphs using the bracket trick must have an identical bracket setup. Duplicate each master layer and set the proper value in the correct type of bracket layer (the components will update themselves and be representative of the glyph at the specified point in the design space). Failing to do this will not prevent an export, but it will prevent the glyph from switching to its alternate intended form (which is why it is a good idea to properly design the "unnecessary" bracket layers as mentioned in B.4.a)

    1. Script: [Add-VF-Bracket-Layers.py ](https://github.com/mjlagattuta/Hepta-Slab/blob/master/sources/tools/Add-VF-Bracket-Layers.py)(Use only on a copy of your source file) (May take a while to run, cycles through all glyphs and all components multiple times)

3. If everything was done correctly thus far, Glyphs App should be able to successfully generate the variable font and all glyphs with components should behave like the glyph they reference

4. If your design does not export from Glyphs App due to a subtable overflow, there may be too many kerns. Add the font-level custom parameter for an extended kerning lookup.

5. You will need to use Glyphs Cutting Edge to export the font, as Glyphs does not support the extended lookup parameter yet. 
	1. When opening your file in the Cutting Edge version, you may be prompted to update the position of glyphs or components, to prevent modifications to your design make sure to click the “select all“ button and then click “keep selected”

### D) Avar mapping

1. Convert the exported variable font to a ttx via the command line

    1. Tool: [Fonttools](https://github.com/fonttools/fonttools)

2. Run "find" and search for fvar in the .ttx. Change the axis values to the appropriate css value with one decimal place afterwards (23.0 → 200.0), do the same for the STAT table

    2. These values correspond to locations on the post-avar-mapped scale (user scale). Changing these values does not change anything in the font, their only purpose is to mark locations and the original values will be of no use once we add the avar table

3. Copy the avar table from the Fonttools repo and paste into the .ttx file  before the fvar table.

    3. Xml structure: [Fonttools ‘avar’](https://github.com/fonttools/fonttools/blob/master/Tests/varLib/data/test_results/BuildAvarSingleAxis.ttx)

    4. Alternatively you can try my avar [macro](https://github.com/googlefonts/robotoslab/blob/master/sources/tools/macros.txt) and check the results. I have not yet gotten @m4rc1e’s script to work, but detailed below is my workflow for calculating the avar values.

4. Calculate "from" and “to” values and update the avar table in your .ttx file (or check them  against the macro result)

    5. "to" values are based on the original scale

        1. If the instance is lighter than your default, then the to value is `((instanceWeight - axisMin) / (default - axisMin)) -1`

        2. If heavier than the default, then the value is
 `((instanceWeight - default) / (axisMax - default))`

	6. "from" values are based on the intended location on the user scale

        3. If the instance is lighter than your default, then the to value is 
`((cssWeight - axisMin) / (defaultCss - axisMin)) -1`  

        4. If heavier than the default, then the value is
 `((cssWeight - defaultCss) / (axisMax - defaultCss))`

    7. For families where the lightest weight is also the default weight, the mapping will only occur on the range of 0 to 1 (-1 → -1, 0 → 0, instances mappings here, 1 → 1)

5. Use fonttools to convert the file back to .ttf

6. Test to make sure the static instances match up to the variable font

### E) Post Processing
Post processing should be done as needed depending on the specific project, but I usually run these three on every project, especially those coming from a Glyphs App export.

1. Run gftools fix-nonhinting

2. Run gftools fix-dsig

3. Run gftools fix-gasp

### F) Issues

1. Variable fonts exported from Glyphs App lack hinting data

2. Fails Font Bakery MS FontVal: [invalid delta format](https://github.com/googlei18n/fontmake/issues/229) (Fontmake does the same)

3. For families with italics additional patches will be needed (primarily) in the `name`, `STAT`, and `fvar` tables, see doc [here](https://github.com/googlefonts/gf-docs/blob/master/Fontmake-STAT-patches.md)

