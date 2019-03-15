---
title: Advancing in Julia
tags: [tutorial]
header:
excerpt: "A gentle introduction to Julia Language"
---
---

You can find part one of this tutorial [here](http://datascience.ronakshah.xyz/Intro-toJulia-p1/)
## Topics Covered So Far:
1. How to print
2. How to assign variable
3. Math Syntax
4. How to get strings
5. String Manipulation
6. String concatentation
7. Data Structures
    a. Tuples
    b. Dict
    c. Arrays
8. Loops

## In this notebook we'll discuss:

1. Conditionals
2. Functions
3. Packages and Libraries
4. Plotting graphs

## Conditionals

we use the ```if``` and ```else``` keywords to define conditions

The syntax is as follows:

```Julia
if *condition 1*
    option 1
elseif *condition 2*
    option 2
else 
    option 3
end
``` 

Unlike python where the end of piece of code is handled by indentations we have ```end``` key word. Making the code a bit more readable

## Functions

Functions are very important for any programming language as it allows the users to develop software that does exactly what it wants. In julia we can define functions in multiple ways. 


```julia
function sayhi(name)
    println("Hi $name, it's great to see you!")
end
```




    sayhi (generic function with 1 method)




```julia
sayhi("Harry Potter")
```

    Hi Harry Potter, it's great to see you!



```julia
function f(x)
    x^2
end
```




    f (generic function with 1 method)




```julia
f(42)
```




    1764



We can also declare functions in single line


```julia
sayhi2(name) = println("Hi $name, it's great to see you!")
f2(x) = x^2
```




    f2 (generic function with 1 method)




```julia
sayhi2("Kvothe")
```

    Hi Kvothe, it's great to see you!



```julia
f2(123)
```




    15129



We can also declare these as "anonymous" function


```julia
sayhi3 = name -> println("Hi $name, it's great to see you!")
f3 = x -> x^2
```




    #5 (generic function with 1 method)




```julia
sayhi3("Kaladin")
```

    Hi Kaladin, it's great to see you!



```julia
f3(111)
```




    12321



### Duck-typing in Julia

*"If it quacks like a duck, it's a duck."*

Fancy word for saying that Julia, unlike C++ will work on any input data type till it makes sense.


```julia
sayhi(55595472)
```

    Hi 55595472, it's great to see you!


### Mutating vs Non-Mutating Function

A mutating function is represented by ```!``` after the name


```julia
v = [3, 5, 2]
```




    3-element Array{Int64,1}:
     3
     5
     2




```julia
sort(v)
```




    3-element Array{Int64,1}:
     2
     3
     5




```julia
v
```




    3-element Array{Int64,1}:
     3
     5
     2



As seen from the example the content of array ```v``` isn't altered and hence ```sort``` is a non mutating function

Let's see how a mutating function works...


```julia
sort!(v)
```




    3-element Array{Int64,1}:
     2
     3
     5




```julia
v
```




    3-element Array{Int64,1}:
     2
     3
     5



Yes! ```v``` contents are altered

### Some higher order functions

#### map

`map` is a "higher-order" function in Julia that *takes a function* as one of its input arguments. 
`map` then applies that function to every element of the data structure you pass it. For example, executing

```julia
map(f, [1, 2, 3])
```
will give you an output array where the function `f` has been applied to all elements of `[1, 2, 3]`
```julia
[f(1), f(2), f(3)]
```


```julia
map(f, [1, 2, 3])
```




    3-element Array{Int64,1}:
     1
     4
     9



Easy breezy.

## Packages

Julia has over 2000 registered packages, making packages a huge part of the Julia ecosystem.

Even so, the package ecosystem still has some growing to do. Notably, we have first class function calls  to other languages, providing excellent foreign function interfaces. We can easily call into python or R, for example, with `PyCall` or `Rcall`.

This means that you don't have to wait until the Julia ecosystem is fully mature, and that moving to Julia doesn't mean you have to give up your favorite package/library from another language! 

To see all available packages, check out

https://pkg.julialang.org/
or
https://juliaobserver.com/

For now, let's learn how to use a package.


```julia
using Pkg
Pkg.add("Example")
```

    [32m[1m Resolving[22m[39m package versions...
    [32m[1m  Updating[22m[39m `~/.julia/Project.toml`
    [90m [no changes][39m
    [32m[1m  Updating[22m[39m `~/.julia/Manifest.toml`
    [90m [no changes][39m



```julia
using Example
```

In the source code of `Example.jl` at
https://github.com/JuliaLang/Example.jl/blob/master/src/Example.jl
we see the following function declared

```
hello(who::String) = "Hello, $who"
```

Having loaded `Example`, we should now be able to call `hello`


```julia
hello("it's me. I was wondering if after all these years you'd like to meet.")
```




    "Hello, it's me. I was wondering if after all these years you'd like to meet."



## Plotting

Julia has created a unique library ```plots``` that seamlessly integrates multiple graph plotting backends like ```pyplot``` ```plotly``` etc. This makes the library a easy to use and consistent

Let's look at some awesome Julia graphs. As an example let us examine relationship between pirates between 1860 and 2000 and global temperature


```julia
globaltemperatures = [14.4, 14.5, 14.8, 15.2, 15.5, 15.8]
numpirates = [45000, 20000, 15000, 5000, 400, 17];
```

Now let us add the plots library


```julia
using Plots
```

Let's use the gr backend to plot awesome graphs


```julia
gr()
```




    Plots.GRBackend()




```julia
plot(numpirates, globaltemperatures, label="line")
```




![]({{ site.baseurl }}/images/Julia/output_39_0.svg)



The above function initiates a plot object with number of pirates on x and global temperatures on y


```julia
scatter!(numpirates, globaltemperatures, label="points")
```




![]({{ site.baseurl }}/images/Julia/output_41_0.svg)



```scatter``` with a ```!``` tells julia that it is a mutating function, meaning it will alter the plot object initiated above
Let's give a shot at using non-mutating ```scatter```


```julia
scatter(numpirates, globaltemperatures, label="points")
```




![]({{ site.baseurl }}/images/Julia/output_43_0.svg)



Neat!

The graph above isn't very intuitive let's add labels to it


```julia
xlabel!("Number of Pirates [Approximate]")
ylabel!("Global Temperature (C)")
title!("Influence of pirate population on global warming")
```




![]({{ site.baseurl }}/images/Julia/output_46_0.svg)



In the next post we'll explore some simple mathematical programs using julia and kick start our journey at machine learning with Julia
