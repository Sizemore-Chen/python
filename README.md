**Bin-Packing and Piece-Wise Linearization**

POLab

Wei-Chin Chen

2020/06/26

**Background and Motivation**

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Bin-packing problem is a real problem in manufacturing industries and
logistics, when we want to put in more objects in a specific area or
space, and vise versa. But it is also a NP-hard (non-deterministic
polynomial-time hard) problem, academically, since it has numerous
binary variables to define the status of objects to solve the optimal
solution. With this characteristic in bin-packing problem, the solving
time will exponentially increase along with the number of objects.

![https://image.slideserve.com/459745/exponential-time-algorithms-n.jpg](media/image1.jpeg){width="5.767361111111111in"
height="2.3645833333333335in"}

Reference:
[[https://www.slideserve.com/gabi/np-completeness-nondeterministic-polynomial-completeness-powerpoint-ppt-presentation]{.underline}](https://www.slideserve.com/gabi/np-completeness-nondeterministic-polynomial-completeness-powerpoint-ppt-presentation)

**Methodology**

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Allocating given n rectangles with fixed lengths and widths within an
minimum area enveloping rectangle is a classic two-dimensional
bin-packing problem (cutting-stock problem).

![Picture 3](media/image1.png){width="3.0984251968503935in"
height="3.0in"}

Reference: Li *et al.* (2002)

We can formulate a mixed-integer linear programming (MILP), as follows,
to define a mathematical model and solve it.

Minimize xy

subject to

All of n rectangles are non-overlapping.

All of n rectangles are within the range of x and y.

$0 < x \leq \overset{??}{x}$ and $0 < y \leq \overset{??}{y}$
($\overset{??}{x}$ and $\overset{??}{y}$ are constants).

Then, to define parameters and variables as follows.\
\
**Parameters**\
$p$$i$ : length of $i$th object~\
~$q$$i$ : width of $i$th object\
$\overset{??}{x}$ : upper bound along the x-axis\
$\overset{??}{y}$: upper bound along the y-axis\
\
**Variables\
**[Continuous variables]{.underline}~\
~$x$$i$ : distance between center of rectangle $i$ and original point
along the x-axis~\
~$y$$i$ : distance between center of rectangle $i$ and original point
along the y-axis~\
~$x$$j$ : distance between center of rectangle $j$ and original point
along the x-axis~\
~$y$$j$ : distance between center of rectangle $j$ and original point
along the y-axis~\
~$x$ : maximum value of all rectangles along the x-axis~\
~$y$ : maximum value of all rectangles along the y-axis\
[Binary variables]{.underline}\
$s$$i$ : orientation indicator for rectangle $i$\
$s$$j$ : orientation indicator for rectangle $j$~\
~$u$$ij$ : relative position between rectangle $i$ and rectangle $j$
along the x-axis~\
~$v$$ij$ : relative position between rectangle $i$ and rectangle $j$
along the y-axis![](media/image2.png){width="4.1890879265091865in"
height="3.038837489063867in"}

![](media/image3.png){width="2.832787620297463in"
height="2.3328838582677167in"}\
\
\
![](media/image4.png){width="1.7150043744531933in"
height="1.2087685914260717in"}\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
The complete formulation is as
follows.![](media/image5.png){width="3.3843667979002623in"
height="3.9021522309711285in"}![](media/image6.png){width="3.2704516622922135in"
height="1.1965069991251094in"}

![](media/image7.png){width="4.976488407699038in"
height="0.21751640419947507in"}

But it still has a problem which is the objective function is a
nonlinear term, we cannot solve by linear programming solver or library
such like Python-Pulp. Hence, we should apply piecewise linearization
method to take logarithm with $x$$y$ and define some constraints for
transforming the original formula into a linear
programming.![](media/image8.png){width="3.992237532808399in"
height="0.9453390201224847in"}

![](media/image9.png){width="3.303209755030621in"
height="2.184106517935258in"}

![](media/image10.png){width="3.7953871391076115in"
height="0.8843624234470692in"}

![](media/image11.png){width="3.7953871391076115in"
height="3.606373578302712in"}

**Example and Application**

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

A real problem with rectangle as
follows.![](media/image12.png){width="3.0918646106736656in"
height="1.1226421697287838in"}\
\
\
\
\
\
\
\
\
I constructed the model by Python-Pulp which its solver is defaulted
CBC, but I could not solve 12 rectangles in limited time, so the
following figure shows the graphic result to a 6-rectangle case.

![Picture 4](media/image13.png){width="2.421259842519685in"
height="1.9015748031496063in"}

**Comments**

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Due to the number of binary variables consisting of MILP and piecewise
linearization, it is hard to solve this kind of bin-packing problem
within a limited time when the number of objects or dimensions grows.
Therefore, we should use or combine other methodologies (e.g.
meta-heuristic algorithms) to resolve the curse of dimension in more
complicated problems (e.g. scheduling).

**Reference**

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

1\.[[https://www.slideserve.com/gabi/np-completeness-nondeterministic-polynomial-completeness-powerpoint-ppt-presentation]{.underline}](https://www.slideserve.com/gabi/np-completeness-nondeterministic-polynomial-completeness-powerpoint-ppt-presentation)

2\. Li, Han-Lin, Ching-Ter Chang, Jung-Fa Tsai (2002). approximately
global optimization for assortment problems using piecewise
linearization techniques. European Journal of Operational Research 140
(2002) 584--589

3\. Li, H.-L., J. -F. Tsai and N. -Z. Hu (2003). A Distributed Global
Optimization Method for Packing Problems. The Journal of the Operational
Research Society, Vol. 54, No. 4, pp. 419-425

4\. Pentico, D.W., The assortment problem with nonlinear cost functions,
Operations Research 24 (6) (1976) 1129--1142

5\. Pling (2009), http://www.pling.org.uk/cs/toc.html.
