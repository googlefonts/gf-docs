# Fontmake STAT Patch Process
*This is the process as of 8/8/18 since the current fix-vf-meta.py script does not work on fonts with more than one axis.*


## Process
0. Change `STAT` minor version number to 1. In `name` table, check that all entries and variations of the font name are “Font Italic” or “Font Regular”, and not some odd combo like “Font Regular Italic”
1. **OPTIONAL** (Fonts are fine without this step) Copy Windows name records 1–14 to Mac name records, change all IDs after nameID to: `platformID="1" platEncID="0" langID="0x0" unicode="True"`
2. If the family has italic styles, add a `name` table entry “Italic” if there is not already one present
3. If the family has a width axis, add the `name` table entries to address the different widths of instances. Entries should address only one axis
	1. *Example: “Condensed” and “Normal”*
	2. *For a script, perhaps this could look to the values of instances on the `fvar` table and generate a canonical width string accordingly*
4. Repeat step three for as many additional axes the family has
5. In the `STAT` table, add an `<Axis>` for Italic (using the same nameID in step3) to the `<DesignAxisRecord>` (be sure to update `Axis index` and `AxisOrdering value`). Also remove the italic axis from `fvar` table if it is present, and remove all coordinate values for that axis.
	1. *The Italic axis does not need to be added to the `fvar` table in families that have separate roman and italic forms. The OT spec acknowledges the axis count of the `STAT` table relative to the `fvar` table: “In a font with an 'fvar' table, this value must be greater than or equal to the axisCount value in the 'fvar' table”*
	2. ***Be Careful when removing an axis from the fvar table, you must also remove the respective `VarRegionAxis` in the `HVAR`, `MVAR`, `GDEF`, `VVAR`, and `BASE` tables***
	3. It appears the fonts operate properly on Windows even if the axes do not match up in the `fvar` tables between fonts (i.e. if romans have a widths axis and italics do not)
6. Add `<AxisValueArray>` table to `STAT` table and add `AxisValue`’s for all weights these can be format1 or format2
	1.  *This can be pulled from the `fvar` table, using both the `subfamilyNameID` as the `ValueNameID value` and the `“wght”` value as the `Value value`*
2.  Add `AxisValue`’s to the `STAT` table for the additional axes. Width for example would have an entry for Condensed and one for Normal. Can be either format1 or format2
	3.  Remember to set the appropriate flags for these entries to mark some as default, otherwise the names of instances on Windows will be messed up.
7. For the roman VF add `AxisValue` `Format="3"` with the string `Regular` on the Italic axis. The `value` will be `0.0` and the `linkedValue` will be `1.0`. This should link the Regular VF to the Italic VF
	1. *For the `nameID` I like to use the Regular from `nameId` 2 since that one is for the family rather than referring to a single style, even though it really makes no difference, a string is a string :)*
	2. *Remember to set `<Flags value="2"/>` if this is the roman font*
8. For the italic VF ad an `Axis value` `Format=1` to the `STAT` table, set it to `1.0` and have the flag set to `0` since the italic style is not the default and should be visible in the name of the font


## Example ttx from Cabin Roman VF
```
  <STAT>
    <Version value="0x00010001"/>
    <DesignAxisRecordSize value="8"/>
    <!-- DesignAxisCount=3 -->
    <DesignAxisRecord>
      <Axis index="0">
        <AxisTag value="wght"/>
        <AxisNameID value="256"/>  <!-- Weight -->
        <AxisOrdering value="0"/>
      </Axis>
      <Axis index="1">
        <AxisTag value="wdth"/>
        <AxisNameID value="257"/>  <!-- Width -->
        <AxisOrdering value="1"/>
      </Axis>
      <Axis index="2">
        <AxisTag value="wdth"/>
        <AxisNameID value="266"/>  <!-- Italic -->
        <AxisOrdering value="2"/>
      </Axis>
    </DesignAxisRecord>
    <!-- AxisValueCount=7 -->
    <AxisValueArray>
      <AxisValue index="0" Format="1">
        <AxisIndex value="0"/>
        <Flags value="0"/>
        <ValueNameID value="258"/>  <!-- Regular -->
        <Value value="400.0"/>
      </AxisValue>
      <AxisValue index="1" Format="1">
        <AxisIndex value="0"/>
        <Flags value="0"/>
        <ValueNameID value="259"/>  <!-- Medium -->
        <Value value="500.0"/>
      </AxisValue>
      <AxisValue index="2" Format="1">
        <AxisIndex value="0"/>
        <Flags value="0"/>
        <ValueNameID value="260"/>  <!-- SemiBold -->
        <Value value="600.0"/>
      </AxisValue>
      <AxisValue index="3" Format="1">
        <AxisIndex value="0"/>
        <Flags value="0"/>
        <ValueNameID value="261"/>  <!-- Bold -->
        <Value value="700.0"/>
      </AxisValue>
      <AxisValue index="4" Format="3">
        <AxisIndex value="2"/>
        <Flags value="2"/>
        <ValueNameID value="2"/>  <!-- Regular -->
        <Value value="0.0"/>
        <LinkedValue value="1.0"/>
      </AxisValue>
      <AxisValue index="5" Format="1">
        <AxisIndex value="1"/>
        <Flags value="0"/>
        <ValueNameID value="267"/>  <!-- Condensed -->
        <Value value="50.0"/>
      </AxisValue>
      <AxisValue index="6" Format="1">
        <AxisIndex value="1"/>
        <Flags value="2"/>
        <ValueNameID value="268"/>  <!-- Normal -->
        <Value value="100.0"/>
      </AxisValue>
    </AxisValueArray>
    <ElidedFallbackNameID value="2"/>  <!-- Regular -->
  </STAT>
```
