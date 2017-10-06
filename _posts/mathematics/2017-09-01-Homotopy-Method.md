---
layout: post
category: mathematics
title: Homotopy Method
date: 2017-09-01
---

### Basic concept of homotopy

Give two topological spaces X,Y,consider two continuous functions f and g which are the mapping between X and Y.If exist a continuous mapping H:X\*[0,1]->Y,satisfied:

![](/assets/mathematics/homotopy_method/fig1.png)

Then could say f and g are homotopy in space Y,function H is a path connected f and g.

### Apply homotopy method on Newton’s method

![](/assets/mathematics/homotopy_method/fig2.png)

Construction of H(x,s) and $F_0(x)$

![](/assets/mathematics/homotopy_method/fig3.png)

We can say that $F_x(x)$ and $F(x)$ are homotopy,the homotopy path are H(x,s).

The algorithm of applied homotopy method on Newton's method is as follows:

![](/assets/mathematics/homotopy_method/fig4.png)

Assume f(x)=arctan(x),to find the root of the equation f(x) = 0.The code is as follows:



1) Hxs.m(H(x,s))

```
function y = Hxs(x,s,x0)  
%H(x,s)=arctan(x) +(s-1)*arctan(x0)  
    y = atan(x) + (s-1)*atan(x0);  
end
```

2)gx.m
```
function y = gx(x)  
%g(x)=1/(1+x^2)  
    y = 1./(1+x.^2);  
end
```

3)NewtonIterHomo.m
```
function [x] = NewtonIterHomo(x0,Hxs,gx,s,tol,verbose)  
% Version: 1.0 written by zhenyutang 
% objective function：H(x,s)=arctan(x) + (s-1)*arctan(x0)  
% x0 is initialization, Hxs is objective function, gx is differential of Hxs，s is input parameter  
% tol is precision,verbose control whether output intermediate result  
% x is the last solution 
% References：1)Wikipedia：homotopy method 
% 3)http://www.maths.lth.se/na/courses/FMN081/FMN081-06/lecture8.pdf  
    if nargin < 6  
        verbose = 0;%default value  
    end  
    if nargin < 5  
        tol = 1e-3;  
    end  
    iter = 0;  
    x = x0;  
    if verbose  
        fprintf('Iter %d: x=%f,f(x)=%f\n',iter,x,Hxs(x,s,x0));  
    end  
    while abs(Hxs(x,s,x0)) > tol  
        x = x - Hxs(x,s,x0)/gx(x);%牛顿迭代公式  
        iter = iter + 1;  
        if verbose  
            fprintf('Iter %d: x=%f,f(x)=%f\n',iter,x,Hxs(x,s,x0));  
        end  
    end  
end
```

4)TestHomotopy.m
```
clear all;close all;clc;  
x0 = 5;  
s = 0:0.1:1;  
x_star = zeros(length(s),1);  
neginf = -20;posinf = 20;step = 0.05;  
X_Plot = neginf:step:posinf;%axis  
EnPlot = 1;%figure,1:yes，0:no  
if EnPlot  
    figure;plot(X_Plot,Hxs(X_Plot,s(1),x0),'r');%fig H(x,0)，F0(x)  
    xlabel('x');ylabel('H(x,s,x_0)');title('homotopy curve')  
    grid on;hold on;pause;      
end  
x_star(1) = x0;  
for i=2:1:11  
    x_star(i) = NewtonIterHomo(x_star(i-1),@Hxs,@gx,s(i),1e-3,1);  
    if EnPlot  
        plot(X_Plot,Hxs(X_Plot,s(i),x_star(i)),'b');  
        hold on;pause;          
    end  
end  
if EnPlot  
    hold off;  
end  
figure;plot(s,x_star,'.-','MarkerEdgeColor','r','MarkerSize',20);grid;  
xlabel('s');ylabel('x^*');title('convergance process of homotopy method');
```

After running this code,we can see x=0.000493.
