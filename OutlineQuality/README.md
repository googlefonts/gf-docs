# Outline Quality Checklist

Design is not particularly judged here, we are talking from the point of view of the technical aspects of a font, i.e: preserved legibility at small sizes, proper rendering/displaying on screen, user experience etc. Since Google Fonts takes backward compatibility seriously this is a quite conservative approach; you wouldn't need all of that if your font is used in a recent environment.

- OTF-CFF fonts compression: doesn't support components. All contours overlapping another will be considered as counter-shapes, resulting is very bad rendering of the font. All outlines get decomposed and merged during export.
- OTF-TFF font compression: support components, supposedly overlapping outlines and nested components (until 4 degrees of nesting). 

Below are some notes about famous outline issues, we ticked the cases that `gftools builder` handles for you.

## Contours

A segment is made of 2 on-curve points which indicates where the segment starts and where it ends. For PostScript contours, each on-curve point of a segment, has an off-curve point which conctrols the curvature of this segment. 

The on-curve points are connecting segments together, hence we call them nodes. Therefore each node is the start or the end of a segment; it works like a door in which a segment is entering, and from which an another one is exiting. We tend to call the 2 off-curve points attached to the same node: the handles. This connection can be sharp (handles are unaligned) creating an angle, or smooth (handles aligned and inter-dependant) creating a curve.


### Segments
- [x] **Mixed outline type :** the outlines of one font must be either PostScript (OpenType Fonts font with CFF compression / .otf) or TrueType (OpenType Fonts with TrueType compression / .ttf). This problem occurs in sources from Fontlab 5.

- [ ] **Wrong direction:** For PS outlines, the outer-shape goes counter-clockwise, and the inner-shape (or counter-shape) goes clockwise. It is the reverse for TT outlines: outer-shape goes clockwise and counter-shape goes counter-clockwise. We usually use PS curves for design, and they are then converted to TT when exporting TTF fonts. Whatever the chosen outline type, make sure it is consistent across the entire family otherwise you would risk a bad interpretation from the rasterizer.

- [ ] **Almost straight:** if a segment is misaligned of one or two units, it may be a mistake from the designer. This small offset can cause a big misinterpretation from the rasterizer at small ppm sizes.

- [ ] **Missing inflexion point:** It is considered that a curve has a *suspicious inflexion* when it is a single segment going from convex to concave (and vice versa). We need to divide this segment by adding a node at the point where the curve is changing condition, therefore the tangent represented by the two handles crosses the curve.

- [ ] **Collinear:** If two line-segments are connected with the same angle (or almost the same angle), or with a slight offset, it means that the entire line could be made with one segment (two points not more). Compatible outlines may need collinear vectors on some sources' masters though.

- [ ] **Short:** Segments of 1 or 2 units are often used to make ink traps, but they are also sometimes unwanted and, again, can be badly rendered on some screens.

- [ ] **Open:** A contour can only be considered as such if it has a closed path, otherwise, it won't be rendered at all.

- [ ] **Overlaying :** overlaying horizontal segments mostly disturb rendering. 
  
- [ ] **Overlapping:** A lot of OS and apps still don't display correctly overlapping contours of static TTF fonts. To preserve your design, we recomend to merge the decomposed contours during the export. If you want to control the result of the merging, it is better to do it yourself. If not, try to keep them in *not too big but not too small* overlapped area. Also try not to overlap more than 2 contours in the same area (contour crossing a contour itself crossing another contour, like asterisk, creates confusion during generation and rendering).

- [ ] **Self-crossing:** Often known as open-corners, it is very helpful while designing and recommended for nice interpolations. They will be preserved for VF fonts and merged during generation to static binaries. To better control the result, pay attention to the size of it (not too big, not too small) as well as not leaving portions of it outside the main shape like the stem, since it can cause unwanted rendering issues. If you want to control the result of the merging, do it yourself if not, same advises as above.

### On-curve points (nodes)

- [ ] **Overlaying:** Also called "empty segments” because they don't have a length. They are often useless and sometimes confusing for hinting and rendering — except for some rare cases of outline compatibility in complicated VF.

- [ ] **Missing on extremes:** Points at X and Y extremes of the paths are required for hinting reasons since they attach hints to the extremum of the stem. Also, having nodes in both in x and y extremes points of the paths will control better the curves and probably reduce the necessity of extra nodes.

- [ ] **Fractional coordinates:** Leads to rounding errors. Also hints can only be linked to integer coordinates, so it can happen that you point's coordinates get rounded, and the hint lays on another pixel.

- [ ] **Broken smooth connection:** Ensure the right type of node according to the connection, smooth (between two curve segments) or sharp (between a curve and a line segment; or two line segments)

### Off-curve points (handles)
- [ ] **Almost straight:** when the connection created by the on-curve point and the off-curve point is almost orthogonal (from 1 or 2 units). 
- [ ] **Broken smooth connection:** Since a curve has an on-curve point at their extremum, it is important for the two off-curve points controlling this curve to be perfectly aligned to not break the curve into an angle.   
- [ ] **Inside the node:** Also known as "zero handle" because its coordinates from the node is (0,0). Off-curve points should either have different coordinates from the node or should be removed. They can be misinterpeted by the rasterizer otherwise.


## Components
- [ ] **Missing:** Component referring to a missing glyphs. Then the component can be displayed.
- [ ] **empty:** Component referring to an empty glyphs.Then the component can be displayed.
- [x] **nested:** Component referring to another component. Post pscript printers tend to not decompose nested components correctly. Therefore components will be flatten during export to make sure the component refers to a glyphs with decomposed outlines.
- [x] **transformed:** Scaled, Rotated and Mirrored components can result in bad rendering. We strongly advise to decompose them.
- [ ] **overlaying:** Same components over each other. If it doesn't get merged, this can result in bad rendering (one component considered as the counter shape of the other). If it gets decomposed and merged, it can result in very weird punky outlines.
- [ ] **overlapping:** Since static TTF support components, only decomposed contours get merged during export. But, still, lots of environment doesn't display overallaping outlines correclty! Therefore we advise to decompose at least one of the components of the glyphs to be sure it gets decomposed and merged during export.
- [x] **Mixed composite:** Glyphs containing components and decomposed outlines. Be aware that a glyphs has to be one of the other, therefore the entire glyphs will be decomposed during export.
- [ ] **Fractional translation coordinates**: The coordinates of the shifted component are not integer is sources, and will be rounded during export, maybe with some errors ending up in bad hinting.