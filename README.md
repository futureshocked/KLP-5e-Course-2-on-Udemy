# KLP 5e — Course 2: Real Boards — project files

Companion project files for *KiCad Like a Pro, 5th Edition*, Course 2 ("Real boards"), on Udemy.
Each hands-on project is captured as a series of numbered stages, one per build step in the course,
so you can start from any point or check your own work against a known-good result.

Clone this repository, or download the stage folder you need, and carry on from there. Modules 1
and 2 work in the symbol and footprint editors with no project open, so their stages are library
folders; from Module 3 on, every stage is a complete KiCad project that opens on its own.

## About Tech Explorations

This course is made by [Tech Explorations](https://techexplorations.com). Visit the site to learn
more about Tech Explorations and its other courses.

## Projects

| Folder | Project | Used in |
|---|---|---|
| [`klp5e-c2-m1-drv8833-parts/`](klp5e-c2-m1-drv8833-parts/) | The DRV8833 symbol and footprint, authored from the datasheet, with Activities A1.1 and A2.1 | Modules 1 and 2 |
| [`klp5e-c2-m3-standin-board/`](klp5e-c2-m3-standin-board/) | The DRV8833 stand-in board, set up with net classes, sizes, custom rules and severities, with Activity A3.1; then routed and given its copper zones | Modules 3 and 4 |
| [`klp5e-c2-m5-led-matrix/`](klp5e-c2-m5-led-matrix/) | The four-cell MAX7219 LED matrix: one cell built, stamped four times and copied with Repeat Layout, with Activity A5.1 | Module 5 |
| [`klp5e-c2-m6-drv8833/`](klp5e-c2-m6-drv8833/) | The DRV8833 two-motor driver board, the capstone: sheet, board setup, driver stage placed first, routed, poured and finished with its silkscreen, with Activity A6.1; its sourcing fields, a second build and the bills; checked, plotted and ordered; then the recipes for its next revision | Modules 6, 8, 9 and 11 |

Each activity folder also holds the activity's slide deck, `slides.html`. Download it and open it in
a browser (press `F` for fullscreen, arrow keys to move), so you can keep the task on screen
instead of pausing the video.

See each project's own README for what each stage contains.
