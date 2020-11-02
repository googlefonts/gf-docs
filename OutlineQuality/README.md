# Outline Quality Checklist

Make sure your font is ready for mastering by fulfilling this checklist. Design is not particularly judged here, we are talking from the point of view of the technical quality aspect of a font, i.e: what you see in your font editor is what will everyone see on their own screen or printed matter.

## Contours
### Segments

- [ ] **Mixed outline type :** The outlines of one font must be either PostScript (OpenType Fonts font with CFF compression / .otf) or TrueType (OpenType Fonts with TrueType compression / .ttf). Fontlab 5 allows mixed curve type within the same glyph.
- [ ] **Wrong direction :** For PS outlines, the outer-shape goes counter counter-clockwise, and the inner-shape (or counter-shape) goes clockwise. It is the reverse for TT outlines: outer-shape goes clockwise and counter-shape goes counter-clockwise. We usually use PS curves for design, and they are then converted to TT when exporting TTF fonts. Whatever the chosen outlines, make sure it is consistent across the entire family.
- [ ] **Almost straight :** If a segment is misaligned of one or two units, it may be a mistake from the designer. This small offset can cause a big misinterpretation form the rasterizer at small ppm sizes.
- [ ] **Missing inflexion point :** It is considered that a curve has a *suspicious inflexion* when it is a single segment going from convex to concave (and vice versa). We need to divide this segment by adding a node at the point where the curve is changing condition, therefore the tangent represented by the two handles crosses the curve.
- [ ] **Collinear :** If two line-segments are connected with the same angle (or almost the same angle), or with a slight offset, it means that the entire line could be made with one segment (two points not more).
- [ ] **Short :** Segments of 1 or 2 units are often used to make ink traps, but they are also sometimes unwanted and, again, can be wildly rendered on some screens.
- [ ] **Open :** A contour can only be considered as such if it has a closed path, otherwise it won't be rendered at all.
- [ ] **Overlaying :** It disturbs rendering, interpolation and variation.
- [ ] **Overlapping :** The crossing of two independent contours is not such a problem in VF (although small overlaps are preferred), and generally merged during generation of static binaries. If you want to control the result of the merging, it is better to do it yourself. If not, try to keep them in a small overlapped area. Also try not to overlap more than 2 contours in the same area (contour crossing a contour itself crossing another contour, like an asterisk, creates confusion during generation and rendering). In any case, try to avoid overlapping shapes which cross a plain shape and a closed counter-shape (typically, Oslash should be manually merged for example).
- [ ] **Self-crossing :** Often known as open-corners, it is very helpful while designing and recommended for nice interpolations. They will be preserved for VF fonts and merged during generation to static binaries. To better control the result, pay attention to the size of it (not too big, not too small) as well as not leaving portions of it outside the main shape like the stem, since it can cause unwanted rendering issues. If you want to control the result of the merging, do it yourself, if not, same advises as above.

### On-curve points (nodes)

- [ ] **Overlaying :** Also called "empty segments" because they don't have a length. They are often useless and sometimes confusing for hinting and rendering — except for some rare cases of variations.
- [ ] **Missing on extremes :** Points at X and Y extremes of the paths are required for hinting reasons since they attach hints to the extremum of the stem. Also, by having them you could control better the curves and probably reduce the necessity of extra nodes.
- [ ] **Fractional coordinates :**

### Off-curve points (handles)
- [ ] **Almost straight :**
- [ ] **Broken smooth connection :** Ensure the right type of node according to the connection, smooth (between to curve segments) or sharp (between a curve and a line segment; or two line segments)
- [ ] **Inside node :**

## Components




## Resources
- Glyphs Tuto
- Red Arrows

## More explanations
- Segment
- Hinting
- PS/TT outlines
- Bracket and brace layers: fontmake support them but doesn't process them as Glyphs.
