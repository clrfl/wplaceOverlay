# wplaceOverlay
- This is an overlay for [wplace](https://wplace.live/)
- It reads blueprint files and will display the difference if the canvas is out of sync.
- This can be used to protect your artworks against vandalism, by making it easy to fix them.
- I am not associated with wplace. If you use this code to violate the terms of use, do so at your own risk

## Usage ([tldr](https://github.com/clrfl/wplaceOverlay/tree/main#tldr-for-tech-savvy-people))
### Setup config.json
- The config.json defines which areas you want to include in the overlay
- To obtain the path of the wplace tiles in which your artwork is located, open the network tab of your browser (F12, »Network«), and navigate to the respective area on the map in your browser.
- Your canvas area will show up as one of the .png files. Find yours, and look at the path.
- Add the last 2 numbers of the .png path **as one separate entry** to your config.json
- Example: `https://backend.wplace.live/files/s0/tiles/1100/670.png` => `[ ["1100","670"], ... ]`

### Run server
- Execute main.py in python
- It will calculate the overlay and start an http server, which serves it to your browser
- Keep this running while you want to use the overlay

> [!TIP]
> If you don't have any experience with programming, and struggle to get the python script running:
> You can download python from [Python.org](https://www.python.org/), and install the required packages using `pip install -r requirements.txt`.
> There are guides on the internet that will help you with that.

### Adjust blueprints
- In the ./blueprints folder there will be a copy of the canvas, created when you initially added its path to the config
- Edit this (e.g. in GIMP) to only keep pixels you want to include in your overlay
- These blueprints will only be *read* by the script, and *not manipulated automatically* after creation. Use them to set up your overlay by deleting everything you don't care about.

### Patch browser
- The javascript browser patch is inspired by [cfp](https://github.com/cfpwastaken/wplace-overlay)
- **EITHER** paste the contents of `browserpatch.js` into your browser console every time you want to activate the overlay,
- **OR** add a bookmark to your browser, make it point to `javascript:` and paste the browserpatch.js file contents there. This only needs to be clicked then to activate the overlay.

### Results
- After you run the browserpatch in console or by clicking the bookmark, the next time the browser updates the resources (few seconds at max.) it will be rerouted to your python server.
- Pixels that don't satisfy your blueprint will be outlined with a thick and transparent pink border, and the desired pixel from the blueprint will be displayed with a light transparency.
- Paint over it with the same color to fix.
- The overlay should update automatically in a few seconds.

## TLDR for tech-savvy people
> [!NOTE]
> 1. write tile IDs into `config.json`
> 2. run `main.py`, keep running
> 3. update blueprints in /blueprints/
> 4. run `browserpatch.js` in console
