---
layout: post
title:  "Matplotlib(1)"
date:   2018--2-16
excerpt: "matplotlib.pyplot is a collection of command style functions that make matplotlib work like MATLAB, In this post, we'll learn how to plot lines with pyplot."
tag:
- Matplotlib 
- Pyplot
comments: true
---
# Pyplot tutorial
This tutorial is a copy of pyplot [official tutorial](https://matplotlib.org/tutorials/introductory/pyplot.html#sphx-glr-tutorials-introductory-pyplot-py).

## Intro to pyplot

Pyplot is a collection of command style functions that make matplotlib work like MATLIB and make it quite easy to create figures.Each pyplot function makes some change to a figure: e.g., creates a figure, creates a plotting area in a figure, plots some lines in a plotting area, decorates the plot with labels, etc.
Generating visualizations with pyplot is quickly:

```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.ylabel('some numbers')
plt.show()
```

![2](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802162.png)

You may be wondering why the x-axis ranges from 0-3 and the y-axis from 1-4. **If you provide a single list or array to the plot() command, matplotlib assumes it is a sequence of y values, and automatically generates the x values for you.** Since python ranges start with 0, the default x vector has the same length as y but starts with 0. Hence the x data are [0,1,2,3].
  
plot() is a versatile command, and will take an arbitrary number of arguments. For example, to plot x versus y, you can issue the command:  

```python
plt.plot([1, 2, 3, 4], [1, 4, 9, 16])
plt.show()
```

![3](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802163.png)


## Formatting the style of your plot
For every x, y pair of arguments, there is an optional third argument which is the format string that indicates the color and line type of the plot. The letters and symbols of the format string are from MATLAB, and you concatenate a color string with a line style string. The default format string is ‘b-‘, which is a solid blue line. For example, to plot the above with red circles, you would issue  

```python
plt.plot([1, 2, 3, 4], [1, 4, 9, 16], 'ro')
plt.axis([0, 6, 0, 20])
plt.show()
```

![4](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802164.png)

The following format string characters are accepted to control the line style or marker:

character|description  
-|-  
'-'|solid line style  
'--'|dashed line style  
'-.'|dash-dot line style  
':'|dotted line style  
'.'|point marker  
','|pixel marker  
'o'|circle marker  
'v'|triangle_down marker  
'^'|triangle_up marker  
'<'|triangle_left marker  
'>'|triangle_right marker  
'1'|tri_down marker  
'2'|tri_up marker  
'3'|tri_left marker  
'4'|tri_right marker  
's'|square marker  
'p'|pentagon marker  
'*'|star marker  
'h'|hexagon1 marker  
'H'|hexagon2 marker  
'+'|plus marker  
'x'|x marker  
'D'|diamond marker  
'd'|thin_diamond marker  
'|'|vline marker  
'_'|hline marker  
  
The following color abbreviations are supported:

character|color  
-|-  
‘b’|blue  
‘g’|green  
‘r’|red  
‘c’|cyan   
‘m’|magenta  
‘y’|yellow  
‘k’|black  
‘w’|white  

To know more about *pyplot*, click [here](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot).

The *axis()* command in the example above takes a list of [xmin, xmax, ymin, ymax] and specifies the viewport of the axes. [see also](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.axis.html#matplotlib.pyplot.axis).


If matplotlib were limited to working with lists, it would be fairly useless for numeric processing. Generally, you will use numpy arrays. **In fact, all sequences are converted to numpy arrays internally.** The example below illustrates a plotting several lines with different format styles in one command using arrays.  

```python
import numpy as np

# evenly sampled time at 200ms intervals
t = np.arange(0., 5., 0.2)

# red dashes, blue squares and green triangles
plt.plot(t, t, 'r--', t, t**2, 'bs', t, t**3, 'g^')
plt.show()
```

![5](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802165.png)

## Plotting with keyword strings

There are some instances where you have data in a format that lets you access particular variables with strings. For example, with numpy.recarray or pandas.DataFrame.  
  
Matplotlib allows you provide such an object with the data keyword argument. If provided, then you may generate plots with the strings corresponding to these variables.

```python
data = {'a': np.arange(50),
        'c': np.random.randint(0, 50, 50),
        'd': np.random.randn(50)}
data['b'] = data['a'] + 10 * np.random.randn(50)
data['d'] = np.abs(data['d']) * 100

plt.scatter('a', 'b', c='c', s='d', data=data)
plt.xlabel('entry a')
plt.ylabel('entry b')
plt.show()
```

![6](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802166.png)

## Plotting with categorical variables

It is also possible to create a plot using categorical variables. Matplotlib allows you to pass categorical variables directly to many plotting functions. For example:

```python
names = ['group_a', 'group_b', 'group_c']
values = [1, 10, 100]

plt.figure(1, figsize=(9, 3))

plt.subplot(131)
plt.bar(names, values)
plt.subplot(132)
plt.scatter(names, values)
plt.subplot(133)
plt.plot(names, values)
plt.suptitle('Categorical Plotting')
plt.show()
```

![7](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802167.png)

## Controlling line properties
Lines have many attributes that you can set: linewidth, dash style, antialiased, etc; see matplotlib.lines.Line2D. There are several ways to set line properties
* Use keyword args:

```python
plt.plot(x, y, linewidth=2.0)
```

* Use the setter methods of a Line2D instance. plot returns a list of Line2D objects; e.g., line1, line2 = plot(x1, y1, x2, y2). In the code below we will suppose that we have only one line so that the list returned is of length 1. We use tuple unpacking with line, to get the first element of that list:

```python
line, = plt.plot(x, y, '-')
line.set_antialiased(False) # turn off antialising
```

* Use the setp() command. The example below uses a MATLAB-style command to set multiple properties on a list of lines. setp works transparently with a list of objects or a single object. You can either use python keyword arguments or MATLAB-style string/value pairs:

```python
lines = plt.plot(x1, y1, x2, y2)
# use keyword args
plt.setp(lines, color='r', linewidth=2.0)
# or MATLAB style string value pairs
plt.setp(lines, 'color', 'r', 'linewidth', 2.0)
```


Here are the available [Line2D](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D) properties.
    
To get a list of settable line properties, call the setp() function with a line or lines as argument

```python
In [69]: lines = plt.plot([1, 2, 3])

In [70]: plt.setp(lines)
  alpha: float
  animated: [True | False]
  antialiased or aa: [True | False]
  ...snip
```


## Working with multiple figures and axes

MATLAB, and pyplot, have the concept of the current figure and the current axes. All plotting commands apply to the current axes. The function gca() returns the current axes (a matplotlib.axes.Axes instance), and gcf() returns the current figure (matplotlib.figure.Figure instance). Normally, you don’t have to worry about this, because it is all taken care of behind the scenes. Below is a script to create two subplots.

```python
def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)

t1 = np.arange(0.0, 5.0, 0.1)
t2 = np.arange(0.0, 5.0, 0.02)

plt.figure(1)
plt.subplot(211)
plt.plot(t1, f(t1), 'bo', t2, f(t2), 'k')

plt.subplot(212)
plt.plot(t2, np.cos(2*np.pi*t2), 'r--')
plt.show()
```

![8](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802168.png)

**The figure() command here is optional because figure(1) will be created by default**, just as a subplot(111) will be created by default if you don’t manually specify any axes. The subplot() command specifies numrows, numcols, plot_number where plot_number ranges from 1 to numrows*numcols. The commas in the subplot command are optional if numrows*numcols<10. So subplot(211) is identical to subplot(2, 1, 1).  
  
You can create an arbitrary number of subplots and axes. If you want to place an axes manually, i.e., not on a rectangular grid, use the axes() command, which allows you to specify the location as axes([left, bottom, width, height]) where all values are in fractional (0 to 1) coordinates. See Axes Demo for an example of placing axes manually and Basic Subplot Demo for an example with lots of subplots.  
  
You can create multiple figures by using multiple figure() calls with an increasing figure number. Of course, each figure can contain as many axes and subplots as your heart desires:
    
```python
import matplotlib.pyplot as plt
plt.figure(1)                # the first figure
plt.subplot(211)             # the first subplot in the first figure
plt.plot([1, 2, 3])
plt.subplot(212)             # the second subplot in the first figure
plt.plot([4, 5, 6])


plt.figure(2)                # a second figure
plt.plot([4, 5, 6])          # creates a subplot(111) by default

plt.figure(1)                # figure 1 current; subplot(212) still current
plt.subplot(211)             # make subplot(211) in figure1 current
plt.title('Easy as 1, 2, 3') # subplot 211 title
```

You can clear the current figure with clf() and the current axes with cla(). If you find it annoying that states (specifically the current image, figure and axes) are being maintained for you behind the scenes, don’t despair: this is just a thin stateful wrapper around an object oriented API, which you can use instead (see Artist tutorial)  
  
If you are making lots of figures, you need to be aware of one more thing: the memory required for a figure is not completely released until the figure is explicitly closed with close(). Deleting all references to the figure, and/or using the window manager to kill the  window in which the figure appears on the screen, is not enough, because pyplot maintains internal references until close() is called.  


## Working with text
The text() command can be used to add text in an arbitrary location, and the xlabel(), ylabel() and title() are used to add text in the indicated locations (see Text introduction for a more detailed example)

```python
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

# the histogram of the data
n, bins, patches = plt.hist(x, 50, normed=1, facecolor='g', alpha=0.75)


plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title('Histogram of IQ')
plt.text(60, .025, r'$\mu=100,\ \sigma=15$')
plt.axis([40, 160, 0, 0.03])
plt.grid(True)
plt.show()
```

![9](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/201802169.png)

All of the text() commands return an matplotlib.text.Text instance. Just as with with lines above, you can customize the properties by passing keyword arguments into the text functions or using setp():  

```python
t = plt.xlabel('my data', fontsize=14, color='red')
```

These properties are covered in more detail in [Text properties and layout](https://matplotlib.org/tutorials/text/text_props.html#sphx-glr-tutorials-text-text-props-py).

### Using mathematical expressions in text

matplotlib accepts TeX equation expressions in any text expression.

```python
plt.title(r'$\sigma_i=15$')
```

The r preceding the title string is important – it signifies that the string is a raw string and not to treat backslashes as python escapes. matplotlib has a built-in TeX expression parser and layout engine, and ships its own math fonts – for details see [Writing mathematical expressions](https://matplotlib.org/tutorials/text/mathtext.html#sphx-glr-tutorials-text-mathtext-py). Thus you can use mathematical text across platforms without requiring a TeX installation. For those who have LaTeX and dvipng installed, you can also use LaTeX to format your text and incorporate the output directly into your display figures or saved postscript – see [Text rendering With LaTeX](https://matplotlib.org/tutorials/text/usetex.html#sphx-glr-tutorials-text-usetex-py).


### Annotating text

The uses of the basic [text()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.text.html#matplotlib.pyplot.text) command above place text at an arbitrary position on the Axes. A common use for text is to annotate some feature of the plot, and the [annotate()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.annotate.html#matplotlib.pyplot.annotate) method provides helper functionality to make annotations easy. In an annotation, there are two points to consider: the location being annotated represented by the argument xy and the location of the text xytext. Both of these arguments are (x,y) tuples.  

```python
ax = plt.subplot(111)

t = np.arange(0.0, 5.0, 0.01)
s = np.cos(2*np.pi*t)
line, = plt.plot(t, s, lw=2)

plt.annotate('local max', xy=(2, 1), xytext=(3, 1.5),
             arrowprops=dict(facecolor='black', shrink=0.05),
             )

plt.ylim(-2, 2)
plt.show()
```

![10](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/2018021610.png)

In this basic example, both the xy (arrow tip) and xytext locations (text location) are in data coordinates. There are a variety of other coordinate systems one can choose – see [Basic annotation](https://matplotlib.org/tutorials/text/annotations.html#annotations-tutorial) and [Advanced Annotation](https://matplotlib.org/tutorials/text/annotations.html#plotting-guide-annotation) for details. More examples can be found in [Annotating Plots](https://matplotlib.org/gallery/text_labels_and_annotations/annotation_demo.html#sphx-glr-gallery-text-labels-and-annotations-annotation-demo-py).  


## Logarithmic and other nonlinear axes

matplotlib.pyplot supports not only linear axis scales, but also logarithmic and logit scales. This is commonly used if data spans many orders of magnitude. Changing the scale of an axis is easy:

```python
plt.xscale(‘log’)
```

An example of four plots with the same data and different scales for the y axis is shown below.

```python
from matplotlib.ticker import NullFormatter  # useful for `logit` scale

# Fixing random state for reproducibility
np.random.seed(19680801)

# make up some data in the interval ]0, 1[
y = np.random.normal(loc=0.5, scale=0.4, size=1000)
y = y[(y > 0) & (y < 1)]
y.sort()
x = np.arange(len(y))

# plot with various axes scales
plt.figure(1)

# linear
plt.subplot(221)
plt.plot(x, y)
plt.yscale('linear')
plt.title('linear')
plt.grid(True)


# log
plt.subplot(222)
plt.plot(x, y)
plt.yscale('log')
plt.title('log')
plt.grid(True)


# symmetric log
plt.subplot(223)
plt.plot(x, y - y.mean())
plt.yscale('symlog', linthreshy=0.01)
plt.title('symlog')
plt.grid(True)

# logit
plt.subplot(224)
plt.plot(x, y)
plt.yscale('logit')
plt.title('logit')
plt.grid(True)
# Format the minor tick labels of the y-axis into empty strings with
# `NullFormatter`, to avoid cumbering the axis with too many labels.
plt.gca().yaxis.set_minor_formatter(NullFormatter())
# Adjust the subplot layout, because the logit one may take more space
# than usual, due to y-tick labels like "1 - 10^{-3}"
plt.subplots_adjust(top=0.92, bottom=0.08, left=0.10, right=0.95, hspace=0.25,
                    wspace=0.35)

plt.show()
```

![11](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/2018021611.png)

It is also possible to add your own scale, see [Developer’s guide for creating scales and transformations](https://matplotlib.org/devel/add_new_projection.html#adding-new-scales) for details.
