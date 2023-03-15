Algorithmic trading

Implementation of the Algorithmic trading project.

The russian version of the task can be found in the repository.


## Contents

1. [Chapter I](#chapter-i) 
    
    1.1. [Introduction](#introduction)
2. [Chapter II](#chapter-ii) 
    
    2.1. [Interpolation](#interpolation)  
    2.2. [Newton interpolation polynomial](#newton-interpolation-polynomial)  
    2.3. [Cubic spline interpolation](#cubic-spline-interpolation)  
    2.4. [Approximation](#approximation)  
    2.5. [Least Squares Method](#least-squares-method)
3. [Chapter III](#chapter-iii) 
    
    3.1. [Part 1](#part-1-interpolation-of-tabulated-functions)  
    3.2. [Part 2](#part-2-approximation-of-tabulated-functions )  
    3.3. [Part 3](#part-3-bonus-research-on-temporal-characteristics)  
    3.4. [Part 4](#part-4-bonus-approximation-with-weights)


## Chapter I  

![Algorithmic trading](https://edu.21-school.ru/services/storage/download/public_any/e4ec63dd-cd02-40b4-807a-e806fd6a9fc7?path=tenantId/96098f4b-5708-4c42-a62c-6893419169b3/gitlab/content_versions/356296/e212129b-1822-3afa-a2a9-18a473b7fd56.JPG)

`-` \"Anyway, Bob told you the essence of the task, didn't he?\"

`-` \"Yes, the implementation of simplest interpolation and approximation methods. But I still don't understand what it's all for. He mentioned something about investments and clients, but he seemed more interested in what was happening on his screen,\" Eve answered to Dave, the lead developer in the finance department, to whom she had been transferred to help. Bob mentioned in his conversation with Eve that they were currently understaffed and had a lot of urgent tasks to take care of.

`-` \"That's right. But it's not really something we need right now - it's more of an order from the AID department.\"

`-` \"Wait, AID? What kind of department is that? I mean, we have a big company on every continent, but I have never heard of this department before.\"

`-` \"It's funny that you don't know. That’s an Assistive Intelligence Development department. AI assistants in short.  By the way, Alice is in charge there, with Charlie's help.\"

`-` \"Alice? But she was just doing simple object detection on video for surveillance systems.\"

`-` \"Not for a year now. Not many people know about the AID, of course: NDA, corporate secrecy, billions of dollars at stake, and all that. But you seemed to be talking quite a lot with her, so... I don't know,\" Dave stopped his apparently unsuccessful attempts to comfort an upset and confused Eve.  She struggled to figure out why her friend hadn't said anything.

`-` \"So, yeah, about the task,\" Dave continued as if nothing had happened. \"We were asked to write a module that could assist and accompany clients in their bidding..\" Eve was no longer really paying attention to what Dave was saying. All she was concerned about was the unexpected news.  Although this explained Alice's recent behavior, some things were still unclear and had yet to be figured out.

## Introduction

In this project you will learn about interpolation and approximation algorithms. Using these algorithms, you will be able to plot the probabilistic behavior of stock quotes and their price forecasts for the foreseeable future based on historical data without regard to external factors __*__.


## Chapter II

### Interpolation

*Interpolation* is a method of finding intermediate values of a quantity based on a discrete set of known values.

Function interpolation is used when you want to find the value of the function $`y(х)`$ at the value of the argument $`x`$ that belongs to the interval $`[x_0, ..., x_n]`$ ($`x_0, ..., x_n`$ are values given in the table), but does not coincide with any of the known values of this interval.

In many cases, the analytical expression of the function $`y(x)`$ is not known and it is not possible to find the value of this function from the table of its values.
So, instead of it another function $`f(x)`$ is plotted, which is easy to calculate and has the same table of values (coincides with it at the points $`x_0, x_1, x_2,..., x_n`$) as $`y(x)`$.

Finding an approximate function is called interpolation and points $`x_0, x_1, x_2, ..., x_n`$ are interpolation nodes. Usually the interpolating function is found as a polynomial of $`n`$ degree.

### Newton interpolation polynomial

If the interpolation nodes are equally spaced, so that $`x_i + 1 - x = h = const`$, where $`h`$ is the interpolation step, i.e. $`x_i = x_0 + n * h`$, then the interpolation polynomial can be written in the form proposed by Newton.

Newton's first interpolation formula is found in the form: $`Pn(x) = a_0 + a_1(x - x_0) + a_2(x - x_0)(x - x_1) + ... + a_n(x - x_0)...(x - x_n)`$.

### Cubic spline interpolation

Cubic spline interpolation is a special case of piecewise polynomial interpolation. In this special case, the function is interpolated by a cubic polynomial between any two neighboring nodes.
Its coefficients at each interval are determined from the conjugation conditions in the nodes:

$`f_i = y_i, f'(x_i - 0) = f'(x_i + 0), f''(x_i - 0) = f''(x_i + 0), i = 1, 2, ..., n - 1`$, where $`x_i + 0`$ and $`x_i - 0`$ - the neighborhood of point $`x_i`$.

In addition, there are conditions at the boundary at $`x = x_0`$ and $`x = x_n`$:
$`f''(x_0) = 0, f''(x_n) = 0`$

### Approximation

*Approximation* is a replacement of some mathematical objects by others, in one sense or another, close to the original ones.

When interpolating, the interpolating function strictly passes through the table nodes because the number of coefficients in the interpolating function is equal to the number of table values.
Approximation is a method in which the approximated function passes not through the interpolation nodes, but between them in order to find additional values that are different from the table data.

If the analytical expression of the function is unknown or very complex, then we have to find an empirical formula, the values of which would not differ much from the experimental data.

### Least Squares Method

The purpose of the least squares method is to find such values of $`x_i`$ at which the sum of the squares of deviations (errors) $`e_i = y_i - f_i(x)`$ will tend to a minimum.

Since each value of $`x_i`$ is generally \"accompanied\" by the corresponding coefficient $`a_i (i = 0, 1, 2, ..., n)`$, the problem is reduced to finding these coefficients.


## Chapter III

## Part 1. Interpolation of tabulated functions

You need to plot a tabulated function of stock quotes using interpolation methods:

- The program must be developed in C++ language of C++17 standard
- The library code must be located in the src folder in the develop branch
- When writing code it is necessary to follow the Google style
- The program must be built with Makefile which contains standard set of targets for GNU-programs all, install, uninstall, clean, dvi, dist. Installation directory could be arbitrary, except the building one
- GUI implementation, based on any GUI library with API for C++ (Qt, SFML, GTK+, Nanogui, Nngui, etc.)
- The data are loaded into the program from a file with stock quotes with the .csv extension:
    -  The file contains data in the form of a table, where the first column is the date, the second column is the value of the function (examples of data files are in the materials folder)
- When uploading a new data file, clear the field for drawing graphs
- The user sets the number of points on which the graph should be plotted (the number of points is not less than in the loaded file)
- All points are evenly distributed between the start and end dates
- On the final graph adjacent points must be connected by a straight line
- Two interpolation methods must be implemented: *Cubic Spline* and *Newton's Polynomial of nth degree*.
- There should be a button in the interface for drawing the cubic spline graph
- There should be a button in the interface for drawing the graph by the Newton polynomial of nth degree
- There should be a field in the interface for entering the degree of the Newton polynomial
-  There should be a button in the interface for clearing the field to draw graphs (the field is cleared only when you click on this button or new data is uploaded)
- There can be up to 5 graphs displayed in the field at the same time (all graphs have different color)
- If there are already 5 graphs displayed in the field, the buttons for drawing new graphs must be blocked
- The interface has to contain the following information about the graphs:
    - Color
    - Name of the file from which the data were taken
    - Interpolation method (specifying the degree if it is a Newton polynomial)
- Provide the ability to output the values of the stock quotes function obtained by both interpolation methods according to a user-defined argument value (date and time)

## Part 2. Approximation of tabulated functions

You need to plot a tabulated function of stock quotes using the *least squares method*. 
    
Moreover, the graph should cover a longer period of time than the input data:

- For graphs from this task there should be a separate field in the interface for drawing
- When uploading a new data file, clear the field for drawing graphs
- The user sets the number of points on which the graph should be plotted (the number of points is not less than in the loaded file)
- All points are evenly distributed between the start and end dates
- On the final graph adjacent points must be connected by a straight line
- On the graph, the points specified in the loaded file must be visually marked:
    - The radius of these points is larger than the thickness of the graph curve
    - The color of these points are differ from colors of the graphs in the field
- The user sets the number of days `M` for which we want to extend the graph (how many days ahead we want to predict the stock price)
- Clear the drawing field when adding a new approximation graph, in which `M` differs from `M` of already drawn graphs
- There can be up to 5 graphs with the same value of the number of days `M` displayed in the field at the same time
  (all graphs should have different color)
- There should be a button in the interface for drawing the graph plotted by the polynomial of the degree set at that time
- There should be a field in the interface for entering the degree of the polynomial
- There should be a button in the interface for clearing the field to draw the approximation graphs
- The interface has to contain the following information about the graphs:
    - Color
    - Name of the file from which the data were taken
    - Degree of polynomial
- If there are already 5 graphs displayed in the field, the buttons for drawing new graphs must be blocked
- Provide the ability to display the value of the approximating function for a given degree of the polynomial according to the user-defined value of the argument (date and time)

## Part 3. Bonus. Research on temporal characteristics

Study the temporal characteristics of interpolations by cubic spline and Newton polynomial methods, depending on the number of calculated points.

- The user sets the maximum number of points `k` and the number of partitions `h`.
- The minimum number `k` is the number of entries in the input table
- You need to measure the time required to calculate values using the spline interpolation algorithms and Newton's method, depending on the change in the number of points.  There must be a total of `h` measurements of the algorithm runtime, the first of which is the measurement for $`k_1`$, where $`k_1`$ equals the number of points in the source file, and the last is $`k_h`$, where $`k_h`$ equals the maximum number of points `k` that is entered through the GUI.
- Measurement of time at each iteration should be performed 10 times and the result should be the arithmetic mean of the obtained values
- In the same field plot two graphs showing the dependencies of the time required to find values from the number of points `k` for two interpolation methods

**Example** 
    
The user sets the number of points *k = 1000000* and the number of partitions *h = 11*.  A file containing 100 entries is inputted, then the average running time of the spline and Newton interpolation algorithms will be calculated for the next number of points:

    k1 = 100, t1_spline = <average_time_for_calculating_100_points_by_splines>, t1_newton = <average_time_for_calculating_100_points_by_Newton’s_method> 
    k2 = 100090, t2_spline = <average_time_for_calculating_100090_points_by_splines>, t2_newton = <average_time_for_calculating_100090_points_by_Newton’s_method> 
    k3 = 200080, t3_spline = <average_time_for_calculating_200080_points_by_splines>, t3_newton = <average_time_for_calculating_200080_points_by_Newton’s_method> 
    k4 = 300070, t4_spline = <average_time_for_calculating_300070_points_by_splines>, t4_newton = <average_time_for_calculating_300070_points_by_Newton’s_method> 
    k5 = 400060, t5_spline = <average_time_for_calculating_400060_points_by_splines>, t5_newton = <average_time_for_calculating_400060_points_by_Newton’s_method> 
    k6 = 500050, t6_spline = <average_time_for_calculating_500050_points_by_splines>, t6_newton = <average_time_for_calculating_500050_points_by_Newton’s_method> 
    k7 = 600040, t7_spline = <average_time_for_calculating_600040_points_by_splines>, t7_newton = <average_time_for_calculating_600040_points_by_Newton’s_method> 
    k8 = 700030, t8_spline = <average_time_for_calculating_700030_points_by_splines>, t8_newton = <average_time_for_calculating_700030_points_by_Newton’s_method> 
    k9 = 800020, t9_spline = <average_time_for_calculating_800020_points_by_splines>, t9_newton = <average_time_for_calculating_800020_points_by_Newton’s_method> 
    k10 = 900010, t10_spline = <average_time_for_calculating_900010_points_by_splines>, t10_newton = <average_time_for_calculating_900010_points_by_Newton’s_method> 
    k11 = 1000000, t11_spline = <average_time_for_calculating_1000000_points_by_splines>, t11_newton = <average_time_for_calculating_1000000_points_by_Newton’s_method> 

The result will be two graphs, each consisting of 11 points:
* the dependence of the number of points `k` from `t_spline`
* the dependence of the number of points `k` from `t_newton`

## Part 4. Bonus. Approximation with weights

Add weights to the table function of stock quotes and take them into account when plotting graphs.

- Add the 3rd column to the source data files: point weights
- For all values that have no weight specified, it is considered equal to 1
- Adapt the method of least squares so that it takes into account the weights of points
- Add the ability to plot the following 4 graphs simultaneously:
    - With the degree of polynomial 1 for a table with user-defined weights
    -  With the degree of polynomial 2 for a table with user-defined weights
    -  With the degree of polynomial 1 for a table in which all weights are 1
    -  With the degree of polynomial 2 for a table in which all weights are 1
- Find the weights that change the sign of the slope of the line corresponding to degree 1 of the polynomial
- Save the file part4.csv to the src folder in the repository, where the weights are set so that the condition of the previous point is met

__*__ - This is not an investment recommendation.


💡 [Tap here](https://forms.yandex.ru/u/635ab298c769f121dba81f0d/) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
