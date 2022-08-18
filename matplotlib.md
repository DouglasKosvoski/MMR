# Matplotlib
Low level graph plotting library in python that serves as a visualization utility.

```python
import matplotlib.pyplot as plt
```

<!-- Plotting -->
<details>
  <summary>Plotting</summary>
  
```python
# plot with line
plt.plot(xpoints, ypoints)

# if no x-point are specified X-axis increase 1-by-1
plt.plot(ypoints)

# plotting without the line
plt.plot(xpoints, ypoints, 'o')

# remember to call, to present the graph to the screen
plt.show()
```
</details>

<!-- Line -->
<details>
  <summary>Line</summary>
  
```python
plt.plot(ypoints, linestyle='dotted')
# linestyle can be written as `ls`

# line color
plt.plot(ypoints, color='r')
# or
plt.plot(ypoints, c='r')

# line width
plt.plot(ypoints, linewidth='20.5')

# multiple lines
y1 = np.array([3, 8, 1, 10])
y2 = np.array([6, 2, 7, 11])

plt.plot(y1)
plt.plot(y2)
```
</details>

<!-- Marker -->
<details>
  <summary>Marker</summary>

```python
# custom marker
plt.plot(ypoints, marker='*')

# marker size
plt.plot(ypoints, marker='o', ms=20)

# markerfacecolor or the shorter mfc to set the color inside the edge of the markers
plt.plot(ypoints, marker='o', mfc='r')

# Set the color of both the edge and the face to red
plt.plot(ypoints, marker='o', mec='r', mfc='r')

# hex-code can also be used to color
plt.plot(ypoints, marker='o', mec='#4CAF50', mfc='#4CAF50')

# even HTML color names are supported
plt.plot(ypoints, marker='o', mec='hotpink', mfc='hotpink')

```
</details>

<!-- Title and Labels -->
<details>
  <summary>Title & Labels</summary>
  
```python
# main title
plt.title("Sports Watch Data")
# x-axis label
plt.xlabel("Average Pulse")
# y-axis label
plt.ylabel("Calorie Burnage")

# font properties
font1 = {'family':'serif','color':'blue','size':20}
font2 = {'family':'serif','color':'darkred','size':15}

plt.title("Sports Watch Data", fontdict=font1)
plt.xlabel("Average Pulse", fontdict=font2)
plt.ylabel("Calorie Burnage", fontdict=font2)

# title positioning
plt.title("Sports Watch Data", loc='left')
```
</details>

<!-- Others -->
<details>
  <summary>Others</summary>

  ```python
# marker|line|color
plt.plot(ypoints, '+:b')
```
</details>

<!-- Grid -->
<details>
  <summary>Grid</summary>

  ```python
# enable grid
plt.grid()

# specify which axis to display
plt.grid(axis = 'x')
plt.grid(axis = 'y')

# line properties
plt.grid(color = 'green', linestyle = '--', linewidth = 0.5)
```
</details>

<!-- Subplot -->
<details>
  <summary>Subplot</summary>
  Function takes three arguments that describes the layout of the figure. <br><br>The layout is organized in rows and columns, which are represented by the first and second argument. <br><br>The third argument represents the index of the current plot.

  ```python
# the figure has 1 row, 2 columns, and this plot is the first plot.
   plt.subplot(1, 2, 1)

# the figure has 1 row, 2 columns, and this plot is the second plot. 
plt.subplot(1, 2, 2)
```

Example

  ```python
  # you can also set individual titles for each graph
# plot 1:
x = np.array([0, 1, 2, 3])
y = np.array([3, 8, 1, 10])

plt.subplot(1, 2, 1)
plt.plot(x,y)
plt.title("SALES")

# plot 2:
x = np.array([0, 1, 2, 3])
y = np.array([10, 20, 30, 40])

plt.subplot(1, 2, 2)
plt.plot(x,y)
plt.title("INCOME")

# and a super title to the "big-picture"
plt.suptitle("MY SHOP")
plt.show()
```
</details>

<!-- Scatter -->
<details>
  <summary>Scatter</summary>
The scatter() function plots one dot for each observation. It needs two arrays of the same length, one for the values of the x-axis, and one for values on the y-axis

  ```python
  x = np.array([5,7,8,7,2,17,2,9,4,11,12,9,6])
y = np.array([99,86,87,88,111,86,103,87,94,78,77,85,86])

plt.scatter(x, y)
```
> `plt.scatter(x, y)` can be called multiple times that it's color will change accordingly. <br> Otherwise a color parameter can be set manually `plt.scatter(x, y, color='#88c999')`. <br><br> A color array can be passed via argument
```python
colors = [
    "red", "green", "blue", "yellow", "pink",
    "black", "orange", "purple", "beige",
    "brown", "gray", "cyan", "magenta"
    ]

# aswell as sizes
sizes = [
    20,50,100,200,500,1000,
    60,90,10,300,600,800,75
    ]

plt.scatter(x, y, c=colors, s=sizes)

# and alpha
plt.scatter(x, y, s=sizes, alpha=0.5)
```
</details>

<!-- ColorMap -->
<details>
  <summary>ColorMap</summary>
    A colormap is like a list of colors, where each color has a value that ranges from 0 to 100. <br><br>
    This colormap is called 'viridis' and as you can see it ranges from 0, which is a purple color, and up to 100, which is a yellow color.
    
  ```python
  # how to use colormap
  plt.scatter(x, y, c=colors, cmap='viridis')
```

> You can include the colormap in the drawing by including the `plt.colorbar()` statement

```python
plt.scatter(x, y, c=colors, cmap='viridis')

plt.colorbar()
```

</details>

<!-- Bar graph -->
<details>
  <summary>Bar graph</summary>

  ```python
# labels and heights
x = np.array(["A", "B", "C", "D"])
y = np.array([3, 8, 1, 10])

# plot as vertical bars
plt.bar(x,y)

# horizontal bars
plt.barh(x, y)

### bar customization, same as usual (default height is 0.8)

# width for vertical
plt.bar(x, y, color="red", width=0.45)

# height for horizontal
plt.barh(x, y, color="red", height=0.45)
```
</details>

<!-- Histogram -->
<details>
  <summary>Histogram</summary>
A histogram is a graph showing frequency distributions.

  ```python
  # create a normal distribution
  x = np.random.normal(170, 10, 250)

  # and call `hist()`
  plt.hist(x)
```
</details>

<!-- Pie charts -->
<details>
  <summary>Pie charts</summary>
By default the plotting of the first wedge starts from the x-axis and move counterclockwise.

  ```python
  y = np.array([35, 25, 25, 15])

mylabels = ["Apples", "Bananas", "Cherries", "Dates"]

plt.pie(y, labels=mylabels)
```
<br>

> As mentioned the default start angle is at the x-axis, but you can change the start angle by specifying a `startangle` parameter.
```python
plt.pie(y, labels=mylabels, startangle=90)
```
<br>

> Pull the "Apples" wedge 0.2 from the center of the pie.
```python
myexplode = [0.2, 0, 0, 0]

plt.pie(y, labels=mylabels, explode=myexplode)

# optionally you can enable shadows
plt.pie(y, labels=mylabels, explode=myexplode, shadow=True)

# and of course manually modify which slice color
mycolors = ["black", "hotpink", "b", "#4CAF50"]

plt.pie(y, labels = mylabels, colors = mycolors)
```
<br>

> To add a list of explanation for each wedge, use the `legend()` function.

```python
plt.pie(y, labels = mylabels)

# legend for color and labels
plt.legend()

# add a legend with a header
plt.legend(title = "Four Fruits:")

plt.show()
```
</details>



<!-- Possible markers -->
<details>
  <summary>All possible markers</summary>

|  Syntax | Description    |
|---------|----------------|
|   'o'   | Circle         |
|   '*'   | Star           |
|   '.'   | Point          |
|   ','   | Pixel          |
|   'x'   | X              |
|   'X'   | X (filled)     |
|   '+'   | Plus           |
|   'P'   | Plus (filled)  |
|   's'   | Square         |
|   'D'   | Diamond        |
|   'd'   | Diamond (thin) |
|   'p'   | Pentagon       |
|   'H'   | Hexagon        |
|   'h'   | Hexagon        |
|   'v'   | Triangle Down  |
|   '^'   | Triangle Up    |
|   '<'   | Triangle Left  |
|   '>'   | Triangle Right |
|   '1'   | Tri Down       |
|   '2'   | Tri Up         |
|   '3'   | Tri Left       |
|   '4'   | Tri Right      |
|   '|'   | Vline          |
|   '_'   | Hlin           |
</details>

<!-- possible lines -->
<details>
  <summary>All possible lines</summary>

|  Syntax | Description |
|---------|-------------|
|   '-'   | Solid line  |
|   ':'   | Dotted line |
|   '--'  | Dashed line |
|   '-.'  | Dotted line |
</details>

<!-- possible Colors -->
<details>
  <summary>All possible Colors</summary>

| Syntax | Description|
|--------|------------|
|  'r'   | Red        |
|  'g'   | Green      |
|  'b'   | Blue       |
|  'c'   | Cyan       |
|  'm'   | Magenta    |
|  'y'   | Yellow     |
|  'k'   | Black      |
|  'w'   | White      |
</details>

<details>
  <summary> All possible ColorMaps   </summary>

|      Name         |       Reverse      |
|-------------------|--------------------|
| Accent            | Accent_r           |
| Blues             | Blues_r            |
| BrBG              | BrBG_r             |
| BuGn              | BuGn_r             |
| BuPu              | BuPu_r             |
| CMRmap            | CMRmap_r           |
| Dark2             | Dark2_r            |
| GnBu              | GnBu_r             |
| Greens            | Greens_r           |
| Greys             | Greys_r            |
| OrRd              | OrRd_r             |
| Oranges           | Oranges_r          |
| PRGn              | PRGn_r             |
| Paired            | Paired_r           |
| Pastel1           | Pastel1_r          |
| Pastel2           | Pastel2_r          |
| PiYG              | PiYG_r             |
| PuBu              | PuBu_r             |
| PuBuGn            | PuBuGn_r           |
| PuOr              | PuOr_r             |
| PuRd              | PuRd_r             |
| Purples           | Purples_r          |
| RdBu              | RdBu_r             |
| RdGy              | RdGy_r             |
| RdPu              | RdPu_r             |
| RdYlBu            | RdYlBu_r           |
| RdYlGn            | RdYlGn_r           |
| Reds              | Reds_r             |
| Set1              | Set1_r             |
| Set2              | Set2_r             |
| Set3              | Set3_r             |
| Spectral          | Spectral_r         |
| Wistia            | Wistia_r           |
| YlGn              | YlGn_r             |
| YlGnBu            | YlGnBu_r           |
| YlOrBr            | YlOrBr_r           |
| YlOrRd            | YlOrRd_r           |
| afmhot            | afmhot_r           |
| autumn            | autumn_r           |
| binary            | binary_r           |
| bone              | bone_r             |
| brg               | brg_r              |
| bwr               | bwr_r              |
| cividis           | cividis_r          |
| cool              | cool_r             |
| coolwarm          | coolwarm_r         |
| copper            | copper_r           |
| cubehelix         | cubehelix_r        |
| flag              | flag_r             |
| gist_earth        | gist_earth_r       |
| gist_gray         | gist_gray_r        |
| gist_heat         | gist_heat_r        |
| gist_ncar         | gist_ncar_r        |
| gist_rainbow      | gist_rainbow_r     |
| gist_stern        | gist_stern_r       |
| gist_yarg         | gist_yarg_r        |
| gnuplot           | gnuplot_r          |
| gnuplot2          | gnuplot2_r         |
| gray              | gray_r             |
| hot               | hot_r              |
| hsv               | hsv_r              |
| inferno           | inferno_r          |
| jet               | jet_r              |
| magma             | magma_r            |
| nipy_spectral     | nipy_spectral_r    |
| ocean             | ocean_r            |
| pink              | pink_r             |
| plasma            | plasma_r           |
| prism             | prism_r            |
| rainbow           | rainbow_r          |
| seismic           | seismic_r          |
| spring            | spring_r           |
| summer            | summer_r           |
| tab10             | tab10_r            |
| tab20             | tab20_r            |
| tab20b            | tab20b_r           |
| tab20c            | tab20c_r           |
| terrain           | terrain_r          |
| twilight          | twilight_r         |
| twilight_shifted  | twilight_shifted_r |
| viridis           | viridis_r          |
| winter            | winter_r           |
</details>