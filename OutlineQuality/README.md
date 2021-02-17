# Outline Quality Checklist

Make sure your font is ready for mastering by fulfilling this checklist. Design is not particularly judged here, we are talking from the point of view of the technical quality aspect of a font, i.e: preserved legibility at small sizes, proper rendering/displaying on screen, user experience etc.

## Contours
### Segments
- [ ] **Mixed outline type :** the outlines of one font must be either PostScript (OpenType Fonts font with CFF compression / .otf) or TrueType (OpenType Fonts with TrueType compression / .ttf). This problem often occurs in sources from Fontlab 5 allows mixed curve type within the same glyph.

- [ ] **Wrong direction:** For PS outlines, the outer-shape goes counter-clockwise, and the inner-shape (or counter-shape) goes clockwise. It is the reverse for TT outlines: outer-shape goes clockwise and counter-shape goes counter-clockwise. We usually use PS curves for design, and they are then converted to TT when exporting TTF fonts. Whatever the chosen outline type, make sure it is consistent across the entire family.

- [ ] **Almost straight:** if a segment is misaligned of one or two units, it may be a mistake from the designer. This small offset can cause a big misinterpretation from the rasterizer at small ppm sizes.

- [ ] **Missing inflexion point:** It is considered that a curve has a *suspicious inflexion* when it is a single segment going from convex to concave (and vice versa). We need to divide this segment by adding a node at the point where the curve is changing condition, therefore the tangent represented by the two handles crosses the curve.

- [ ] **Collinear:** If two line-segments are connected with the same angle (or almost the same angle), or with a slight offset, it means that the entire line could be made with one segment (two points not more).

- [ ] **Short:** Segments of 1 or 2 units are often used to make ink traps, but they are also sometimes unwanted and, again, can be wildly rendered on some screens.

- [ ] **Open:** A contour can only be considered as such if it has a closed path, otherwise, it won't be rendered at all.

- [ ] **Overlaying :** It disturbs rendering, interpolation and variation.
  
- [ ] **Overlapping:** The crossing of two independent contours is not such a problem in VF and generally merged during the generation of static binaries. If you want to control the result of the merging, it is better to do it yourself. If not, try to keep them in *not too big but not too small* overlapped area. Also try not to overlap more than 2 contours in the same area (contour crossing a contour itself crossing another contour, like asterisk, creates confusion during generation and rendering). Rendering issues in variable fonts also happen when you have two shapes overlaping + overlaying contours. Eg. The top bar of E entering the vertical stem and having a part of their segments above each other: it would be better to merge them, and open the corner.

- [ ] **Self-crossing:** Often known as open-corners, it is very helpful while designing and recommended for nice interpolations. They will be preserved for VF fonts and merged during generation to static binaries. To better control the result, pay attention to the size of it (not too big, not too small) as well as not leaving portions of it outside the main shape like the stem, since it can cause unwanted rendering issues. If you want to control the result of the merging, do it yourself if not, same advises as above.

### On-curve points (nodes)

- [ ] **Overlaying:** Also called "empty segments” because they don't have a length. They are often useless and sometimes confusing for hinting and rendering — except for some rare cases of variations.

- [ ] **Missing on extremes:** Points at X and Y extremes of the paths are required for hinting reasons since they attach hints to the extremum of the stem. Also, having nodes in both in x and y extremes points of the paths will control better the curves and probably reduce the necessity of extra nodes.

- [ ] **Fractional coordinates:** Leads to rounding errors.

- [ ] **Broken smooth connection:** Ensure the right type of node according to the connection, smooth (between two curve segments) or sharp (between a curve and a line segment; or two line segments)

### Off-curve points (handles)
- [ ] **Almost straight:**
- [ ] **Broken smooth connection:**
- [ ] **Inside the node:** Also known as "zero handle" because its coordinates from the node is (0,0). Off-curve points should either have different coordinates from the node or should be removed. They can be misinterpeted by the rasterizer otherwise.


## Compounds, components, composites
- [ ] **Missing:**
- [ ] **empty:**
- [ ] **nested:**
- [ ] **transformed:**
- [ ] **overlaying:**
- [ ] **overlapping:**
- [ ] **Mixed composite-glyph:**
- [ ] **Fractional coordinates** (nodes, handles, components translation distances):

## Hinting
- [ ] **Alignment zones – Overshoots**
- [ ] **Standard stem values**

## More explanations
- Segment
- Hinting
- PS/TT outlines
- Bracket and brace layers: fontmake support them but doesn't process them as Glyphs.
