# Bin-Packing and Piece-Wise Linearization

POLab
Wei-Chin Chen
2020/06/26


Background and Motivation
______________________________________________________________
Bin-packing problem is a real problem in manufacturing industries and logistics, when we want to put in more objects in a specific area or space, and vise versa. But it is also a NP-hard (non-deterministic polynomial-time hard) problem, academically, since it has numerous binary variables to define the status of objects to solve the optimal solution. With this characteristic in bin-packing problem, the solving time will exponentially increase along with the number of objects. 

Reference: https://www.slideserve.com/gabi/np-completeness-nondeterministic-polynomial-completeness-powerpoint-ppt-presentation


Methodology
______________________________________________________________
Allocating given n rectangles with fixed lengths and widths within an minimum area enveloping rectangle is a classic two-dimensional bin-packing problem (cutting-stock problem). 

Reference: Li et al. (2002)

We can formulate a mixed-integer linear programming (MILP), as follows, to define a mathematical model and solve it. 

Minimize 
subject to
All of n rectangles are non-overlapping.
All of n rectangles are within the range of  and .
 and  ( and  are constants).

Then, to define parameters and variables as follows.  Parameters  : length of th object  : width of th object  : upper bound along the x-axis :  upper bound along the y-axis  Variables Continuous variables  : distance between center of rectangle  and original point along the x-axis  : distance between center of rectangle  and original point along the y-axis  : distance between center of rectangle  and original point along the x-axis  : distance between center of rectangle  and original point along the y-axis  : maximum value of all rectangles along the x-axis  : maximum value of all rectangles along the y-axis Binary variables  : orientation indicator for rectangle   : orientation indicator for rectangle   : relative position between rectangle  and rectangle  along the x-axis  : relative position between rectangle  and rectangle  along the y-axis


                              		The complete formulation is as follows. 
         










         





 	But it still has a problem which is the objective function is a nonlinear term, we cannot solve by linear programming solver or library such like Python-Pulp. Hence, we should apply piecewise linearization method to take logarithm with  and define some constraints for transforming the original formula into a linear programming. 
      
































    

 Example and Application
______________________________________________________________
A real problem with rectangle as follows.         	I constructed the model by Python-Pulp which its solver is defaulted CBC,    but I could not solve 12 rectangles in limited time, so the following figure shows the graphic result to a 6-rectangle case.

  Comments
______________________________________________________________
Due to the number of binary variables consisting of MILP and piecewise linearization, it is hard to solve this kind of bin-packing problem within a limited time when the number of objects or dimensions grows. Therefore, we should use or combine other methodologies (e.g. meta-heuristic algorithms) to resolve the curse of dimension in more complicated problems (e.g. scheduling). 

 Reference
______________________________________________________________
1. https://www.slideserve.com/gabi/np-completeness-nondeterministic-polynomial-completeness-powerpoint-ppt-presentation
2. Li, Han-Lin, Ching-Ter Chang, Jung-Fa Tsai (2002). approximately global optimization for assortment problems using piecewise linearization techniques. European Journal of Operational Research 140 (2002) 584–589 
3. Li, H.-L., J. -F. Tsai and N. -Z. Hu (2003). A Distributed Global Optimization Method for Packing Problems. The Journal of the Operational Research Society, Vol. 54, No. 4, pp. 419-425 
4. Pentico, D.W., The assortment problem with nonlinear cost functions, Operations Research 24 (6) (1976) 1129–1142 
5. Pling (2009), http://www.pling.org.uk/cs/toc.html. 
