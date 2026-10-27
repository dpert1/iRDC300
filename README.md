# NE300-iRDC
 Interactive Reference Data Card for NE300

General workflow to create it:
take the RDC image as an svg and add boxes to it in inkscape which are invisible but callable by html
The main page is the index.html (static website). It loads img/rdc_both.svg and equations.json and makes every box whose id starts with `prc-` clickable.
Each entry in equations.json is keyed by the box id and holds the popup content (title, equations, variables, description) and an orientation (left, middle or right) based on position in the RDC.
Then when you click on a box, it builds the little callout from that entry.

To add a new equation card:
1. Draw a box over the equation in inkscape and give it an id starting with `prc-` (e.g. `prc-53`).
2. Add an entry with the same `id` to equations.json.

Embedded images in the svg are stored at roughly 4x their displayed size to keep the page small. If you re-export the card from inkscape, check the file size (it should be well under 1 MB).
