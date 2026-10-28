# Sprinkle Stencil Maker

A small browser tool for making sprinkle stencils you can 3D print. You give it an SVG, tell it how big the shape should be and how many to tile across the plate, and it cuts them out of a flat piece and exports an STL.

I wanted something like those white stencil plates where you shake sprinkles over the holes and get a neat grid of little shapes on a cake or cookie. Making one in CAD by hand every time I wanted a new shape got old fast.

It's a single HTML file. No build step, no install.

**Try it:** [https://italiansquirel.github.io/Sprinkle-Stencil-Maker/](https://italiansquirel.github.io/Sprinkle-Stencil-Maker/)

## Running it yourself

Use the link above, or download `index.html` and open it in a browser. It pulls three.js from a CDN, so you need to be online.

To host your own copy, fork this repo, then go to Settings, Pages, and set the source to the main branch. GitHub gives you a link a minute or two later.

## Using it

1. Upload an SVG, or just play with the heart that loads by default.
2. Set the shape width in mm. Height follows the proportions.
3. Pick columns and rows, and the gap between shapes.
4. Choose a layout. "Staggered (n / n+1)" gives the offset rows you see on most store-bought plates. "Straight grid" is exactly what it sounds like.
5. Set plate thickness and corner radius. Leave auto-size on and it wraps the plate around the array with a margin. Turn it off if you want a fixed plate size.
6. Hit Export STL.

The preview is a normal orbit view, so drag to rotate and scroll to zoom.

## Which SVGs work

Anything with filled shapes. Simple, chunky silhouettes are best: hearts, stars, fish, tails, little animals.

A few things to know:

- Only the outer outline of each shape gets cut. If your SVG has holes inside it (the middle of an "O", say), those holes get filled in.
- Strokes with no fill can behave oddly. Convert strokes to outlines first if you can.
- Cutouts that would run off the edge of the plate are skipped, and the tool tells you how many.
- Very thin points will be fragile and may not print cleanly. If the tips of your shape are narrower than your nozzle, make the shape bigger.

## Printing

I'd print it flat, no supports. About 1.5 to 2 mm thick is stiff enough to press down without bending but not so thick that sprinkles get stuck in the holes. Go lower if your sprinkles are small.

One honest note on food: 3D prints have tiny layer lines that can hold onto moisture and bacteria. For dry sprinkles on top of a cake this is generally fine, but don't treat a printed plate as food safe in the way a steel cutter is. Use filament rated for food contact if you can, wash it by hand, dry it fully, and don't put PLA in the dishwasher.

## How it works

The plate is a rounded rectangle extruded to the thickness you pick. Each tiled copy of your shape is added to it as a hole, and three.js extrudes the whole thing in one go, so the cutouts are real geometry and not a boolean subtraction. The SVG is read with three's SVGLoader. The STL is written as plain ASCII text.

Because of that, overlapping cutouts can break the mesh. Keep the gap positive.

## Credits

Built with [three.js](https://threejs.org). The sprinkle background is an inline SVG pattern.

## License

MIT. See the `LICENSE` file.
