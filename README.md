# FreeForge Batch Mockup Generator

The **FreeForge Batch Mockup Generator** is a desktop tool for quickly creating large batches of apparel mockup images from finished artwork files.

It lets you preview artwork on a mockup, adjust artwork size and placement, save individual adjustments, establish default placement settings, and automatically generate the complete batch.

## Current Features

### Batch Mockup Generation

Select a folder containing your artwork and generate mockups for every supported design in that folder.

Supported artwork formats:

- PNG
- WEBP
- JPG
- JPEG
- SVG

Finished mockups are exported as optimized JPG images.

### Visual Preview

The program includes a large preview window so you can see how each design will appear on the selected mockup before generating the batch.

Use **Previous** and **Next** to move through all artwork in the selected designs folder.

## Artwork Adjustment Controls

Each design can be adjusted independently.

### Scale Multiplier

Controls the overall size of the artwork.

Current adjustment range: **0.25x to 3.00x**

The displayed scale value uses three decimal places for precise sizing.

### Horizontal Offset

Moves the artwork left or right across the mockup.

Current range: **-1000 px to +1500 px**

### Vertical Offset

Moves the artwork up or down on the mockup.

Current range: **-1000 px to +2000 px**

These expanded positioning ranges are useful when working with different mockup photographs, garment styles, models, and artwork proportions.

## Saved Default Positioning

Once you find placement settings that work well for most designs, click **Save current settings as default**.

The generator saves:

- Scale multiplier
- Horizontal offset
- Vertical offset
- Automatic white-background removal setting

These values are stored in `mockup_defaults.json`.

New designs without their own saved adjustment automatically use these defaults.

## Per-Design Adjustments

Not every design has the same proportions. A wide design may need different placement than a tall design.

After adjusting a particular design, click **Save adjustment for this design**.

The design's individual scale, horizontal position, and vertical position are stored in `mockup_overrides.json`.

Per-design adjustments take priority when the batch is generated.

### Reset a Design

Click **Reset this design to automatic** to remove that design's saved override and reload it using the normal/default positioning behavior.

## Automatic Background Removal

The generator includes **Automatically remove near-white background from opaque images**.

When enabled, artwork that does not already contain real transparency can have near-white pixels made transparent automatically.

The current white threshold is `248`.

Artwork that already contains real alpha transparency is recognized separately and does not go through the same automatic white-removal process.

## Automatic Artwork Trimming

After artwork has been prepared, the generator detects the visible alpha area and crops unused transparent space surrounding the design.

This helps positioning and scaling operate on the visible artwork instead of unnecessary transparent canvas space.

## Automatic Artwork Presets

The generator examines artwork proportions and identifies designs using internal preset categories:

- `standard`
- `tall`
- `opaque-wide`
- `transparent-wide`

The active preset can be seen in the program's status area while previewing artwork.

## SVG Support

SVG artwork is supported through **Inkscape**.

When an SVG is encountered, the generator searches for Inkscape in the system path and standard Windows installation locations. It temporarily renders the SVG as a PNG for processing.

If SVG files will be used, Inkscape must be installed.

## Basic Workflow

1. **Select the Mockup** - Click **Browse** beside **Mockup** and select the garment/model image.
2. **Select the Designs Folder** - Choose the folder containing the artwork. An output folder named `mockups` is automatically proposed inside the designs folder.
3. **Preview Designs** - Use **Previous** and **Next** to move through the artwork.
4. **Establish Default Placement** - Adjust scale, horizontal offset, and vertical offset, then click **Save current settings as default**.
5. **Correct Exceptions** - For designs requiring special positioning, make the adjustment and click **Save adjustment for this design**.
6. **Generate Everything** - Click **GENERATE ALL MOCKUPS** to process the complete artwork folder.

## Output Files

Generated mockups use this naming format:

```text
DESIGNNAME_mockup_black.jpg
```

Examples:

```text
camping-design_mockup_black.jpg
deer-hunting_mockup_black.jpg
patriotic-eagle_mockup_black.jpg
```

JPEG quality is currently configured at **94**.

## Mockup Report

Each completed batch also creates:

```text
mockup_report.json
```

The report records the source filename, output filename, scale, horizontal and vertical offsets, preset, white-removal status, position, and final artwork size used for each mockup.

## Typical Folder Structure

```text
FreeForge Mockup Generator/
|
|-- mockup_generator.py
|-- 09-black.png
|-- mockup_defaults.json
|
|-- Designs/
|   |-- design-001.png
|   |-- design-002.png
|   |-- design-003.svg
|   |-- mockup_overrides.json
|
|-- mockups/
    |-- design-001_mockup_black.jpg
    |-- design-002_mockup_black.jpg
    |-- design-003_mockup_black.jpg
    |-- mockup_report.json
```

The default mockup filename referenced by the program is `09-black.png`.

## Requirements

### Python

A working Python installation is required when running the Python script directly.

### Pillow

The program uses Pillow for image loading, resizing, compositing, transparency handling, previews, and JPEG output.

Install Pillow with:

```bash
pip install pillow
```

### Tkinter

The desktop interface uses Tkinter and ttk.

### Inkscape

Required when processing SVG artwork.

## Command-Line Batch Mode

The generator also includes a command-line batch mode.

Supported arguments:

```text
--batch
--mockup
--designs
--output
```

When using `--batch`, both `--designs` and `--output` are required.

Example:

```bash
python mockup_generator.py --batch --mockup "09-black.png" --designs "C:\Designs" --output "C:\Designs\mockups"
```

The GUI does not open in batch mode.

## Recommended FreeForge Workflow

For a large DTF artwork collection:

1. Put finished artwork into one designs folder.
2. Open the Mockup Generator.
3. Select the appropriate shirt/model mockup.
4. Select the designs folder.
5. Set scale and placement on a representative design.
6. Save those settings as the default.
7. Move through the remaining designs.
8. Save individual adjustments only for designs needing special positioning.
9. Click **GENERATE ALL MOCKUPS**.
10. Use the generated JPG files for product listings and website images.

## GUI Control Reference

| Control | Purpose |
|---|---|
| Mockup | Select garment/model image |
| Designs folder | Select artwork folder |
| Output folder | Choose finished mockup location |
| Previous / Next | Browse designs |
| Scale multiplier | Resize artwork |
| Horizontal offset | Move artwork left/right |
| Vertical offset | Move artwork up/down |
| Automatically remove near-white background | Remove near-white pixels from qualifying opaque artwork |
| Save adjustment for this design | Store design-specific placement |
| Save current settings as default | Establish placement for designs without their own overrides |
| Reset this design to automatic | Remove saved override |
| GENERATE ALL MOCKUPS | Process the complete artwork folder |

---

## FreeForge Batch Mockup Generator

Built to reduce the repetitive work involved in turning a large DTF artwork library into consistent, ready-to-use apparel mockups.
