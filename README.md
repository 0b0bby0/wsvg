# Description of the wsvg library
wsvg is a light Python wrapper around the SVG (scalable vector graphics) format enabling the scripting of SVG files. There are no external dependancies ecept for Python3. The code has been extended and enhanced from work by Isendrak Skatasmid (http://code.activestate.com/recipes/578123-draw-svg-images-in-python-python-recipe-enhanced-v/), who, in turn, based the work on Rick Muller's Code (http://code.activestate.com/recipes/325823-draw-svg-images-in-python/).

## Installation
Download repository and unzip (alternatively fork or clone), cd to the project base folder and execute the command below:

```bash
>>> pip3 install -e .
```

__If using an anaconda environment__ you may have to first locate the anaconda pip using whereis.
```bash
>>> whereis pip
```

Locate the appropriate file path (the one that has anaconda and the correct environment in the filepath) and run the modified command. For example (where username and env_name should be modified):

```bash
>>> /home/username/anaconda3/envs/env_name/bin/pip install -e .
```

__If _not_ using an anaconda environment__ simply install using pip:

```bash
>>> pip install -e .
```

## Usage
The library works by first creating a scene. Different lines and shapes are then added to this scene. Finally, the data is written to disk as an actual svg file. Colors can be specified as RGB tuples, as HEX strings or using a set of pre-defined color names.

```Python3
>>> from wsvg import svg
>>> scene = svg.Scene("test.svg", size=(400,400))
>>> scene.add(svg.Rectangle((100,100),200,200,(0,255,255),(0,0,0),1))
>>> scene.write_svg()
```


The basic shapes that can be added to a scen include the following:
```Python3
>>> svg.Rectangle(origin=(100,100),
        height=200,
        width=200,
        fill_color=(0,255,255),
        line_color=(0,0,0),
        line_width=1)
>>> svg.Polygon(points=[(5,5),(5,10),(15,10),(20,20)],
        fill_color='slate',
        line_color='pink',
        line_width=1)
>>> svg.PolyLine(points=[(5,5),(5,10),(15,10),(20,20)],
        line_color='#000000',
        closed=False,
        fill_color='none',
        line_width=1,
        linecap = 'butt',
        linejoin='miter',
        lineopacity=1,
        ID='path001')
>>> svg.Line(start=(200,200),
        end=(200,300),
        line_color=(0,0,0),
        line_width=1,
        linecap='butt',
        linejoin='miter',
        lineopacity=1,
        ID='path001')
>>> svg.Circle(center=(200,200),
        radius=30,
        fill_color=(0,0,255),
        line_color=(0,0,0),
        line_width=1)
>>> svg.Text(text="Normal",
          origin=(50,50),
          angle=0,
          size=24,
          color=(0,0,0))
>>> svg.Ellipse(center=(300,300),
          radius_x=40,
          radius_y=25,
          fill_color=(255,0,255),
          line_color=(0,255,0),
          line_width=1)
>>> svg.Arc(origin=(10,10),
          radius=50,
          start_ang=0,
          end_ang=90,
          fill_color=(0,0,0),
          line_color=(255,0,0),
          line_width=3)
>>> svg.DoubleArc(origin=(100,200),
          radius=20,
          line_width=14,
          start_ang=0,
          end_ang=90,
          fill_color=(0,0,0),
          line_color=(255,0,0),
          width=0)
>>> svg.ControlLine(start=(0,150),
          end=(300,300),
          control1=(300,150),
          control2=(0,300),
          line_color=(255,0,0),
          line_width=5,
          ID='path099101')
```

It is also possible to group objects. Groups are added to the scene using scene.add() analogous to what is illustrated in the first example.
```Python3
>>> first_line = svg.Line(start=(0,0), end=(15,10))
>>> second_line = svg.Line(start=(44,1), end=(9,2))
>>> svg.Group(elements=[first_line, second_line],
          ID='group001')
```
