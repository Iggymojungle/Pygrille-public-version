# Pygrille

Pygrille is a Python library that uses Pygame to make it easier to do many things involving a square grid.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install Pygrille.

```bash
pip install pygrille
```

## Usage

```python
import pygrille

PIXEL_SIZE = 40 # The size of each square in the grid.
GRID_DIMENSIONS = (6, 5) # The number of squares in the x and y directions in the grid.

# Initiate the grid. PIXEL_SIZE and GRID_DIMENSIONS are required and everything else is optional. 
# The extras variable is a list of values that you want contained in each pixel - for example a temporary distance in Dijkstra's algorithm.
grid = pygrille.Grid(PIXEL_SIZE, GRID_DIMENSIONS, extras = ["Hello", "World"], framerate = 60, default_colour = pygrille.random_colour(), border_width = 10)

# Ensures the grid has not been closed each frame. 
# Also updates the newclick and newkey variables (booleans - True if there is a new click or key press) 
# And the lastclick (tuple - grid location of most recent click) and lastkey (string - name of most recent key pressed) variables.
while grid.check_open():

    # If the user clicks on a square, set it to a random colour and set the border to a random colour.
    if grid.new_mouse_up:
        grid[grid.last_mouse_up[0]][grid.last_mouse_up[1]].colour = pygrille.random_colour()
        grid[grid.last_mouse_up[0]][grid.last_mouse_up[1]].extras["Hello"] = "Clicked"
        grid.border_colour = pygrille.random_colour()

    # If the spacebar is pressed, print the status of the extra value "Hello" in the top left pixel.
    if grid.newkey:
        if grid.lastkey == "space":
            print(grid[0][0].extras["Hello"])

    # Draw the grid to the screen
    grid.draw()

    # Keep the grid running.
    grid.tick()

# Once pygrille is closed, finish quitting it.
grid.quit()

```

## Updates

### 0.3.2
* Fixed bug with image sizes when images were used multiple times.

### 0.3.1
* Fixed bug with mouse-down on UI elements.

### 0.3.0
* Added support for border size overrides - this allows for certain border lines to be wider than others.
* Added mouse-down and mouse-over support. Replaced "lastclick" and "newclick" with "last_mouse_up" and "new_mouse_up". Please update any past code that used these attributes to reflect this.

### 0.2.1
* Added a check for clicking UI elements via the Grid.newclick_ui and Grid.clicked_ui attributes.
* Fixed an error in the example code in this README.
* Other minor changes.

### 0.2.0.1
* Reupload due to issue with first upload of 0.2.0.

### 0.2.0  
* Updated grid initialisation.
* Added text as a UI option.
* Added image caching to speed up programs.
* Other code refactoring and minor changes.

### 0.1.0 (Mistakenly uploaded to PyPI as 0.1.1)
* Added the ability to force a window size and set the position of the grid in relation to this as desired.
* Added the possibility for UI elements.
* Added methods to Grid to get global coordinates from grid coordinates or vice-versa
* Other minor changes