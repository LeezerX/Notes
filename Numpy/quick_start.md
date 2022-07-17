---
title: "Habits"
author: John Doe
date: March 22, 2005
output: beamer_presentation
---

# numpy quick start

## ndarray

numpy's array class. It has these attribute:

- *ndim* the length of shape
- *shape* a tuple
- *size* the product of shape
- *dtype* datas' type
- *itemsize* 
- *data*

## creation

1. *np.array*:get a ndarray from a known sequence

    - from a sequense

        ```Python
        a = np.array([1,2,3])
        ```

    - if from a sequence of sequence,the ndarray will be of two ndim

    - para:*dtype* can define the item's type of the ndarray

2. get a ndarray whose shape is decided by a tuple to decide the ndarray's shape,but the elem are unknown

    - *zeros* 
        ```Python
        >>> np.zeros(3,dtype=int)
        np.array([0,0,0])
        ```

    - *ones* 

    - *empth* all the item is random,and its type is float64

    when add **_like** , we can get a ndarray from a sequence:

    ```Python
    >>> np.zeros_like([[1,2],[3,4]])
    array([[0,0],[0,0]])
    ```
    

3. to creat a sequence of numbers

    - *arange* 

        ```Python
        >>> np.arange(10,30,5)
        array([10,15,20,25])
        ```
    
        the **5** is step[^1],and it can be float,but when use float,it's precision will not be predict,therefor another method:

    [^1]: from begin ,then add step by step, before reach end(don't get the end)

    - *linspace* 

        ```Python
        >>> np.linspce(begin,end,amounts)
        ```

        *amount*: the number of elem we want

        we can get begin and end

## printing

just `print(np.array)`

## Basic Operation

### Arithmetic Operation

like + - * \, it apply elementwise, and return a new array

excepcially, * applies elementwise, not stands matrix product, **@** or **dot method** is matrix product

```Python
>>> a = np.array([[1,1],
...               [0,1]])
>>> b = np.array([[2,0],
...               [3,4]])
>>> a @ b or a.dot(b)
array([[5,4],
       [3,4]])
```

+= *= is modify an existing array

### ndarray class methods

- *ndarray.sum* 
- *ndarray.max*
- *ndarray.min*
- *np.cumsum* 逐项求和

para: **axis** 对于二维array，`axis=0`时,对每**列**运用method,`axis=1`时,对每**行**运用method

## Universal Functions

ufunc operate elementwise and producting a new array

- `np.exp`
- `np.sin`
- ...

## Indexing,Slicing,Iterating

`array[0:n:2]`,`array[0:n:1,0:n:2]`

dots(...) represent as many colons as needed to produced a complete indexing tuple

```Python
as x.ndim = 5
x[...,3] is equal to x[:,:,:,:,3]
x[4,...,5,:] is equal to x[4,:,:,5,:]
```

**iterating** 

for a multidimensional arrays is done with respect to the first axis:
```Python
b.ndim = 2
for row in b:
    row is b's row
```

however, if want to operate all elem,can use *flat* attribute
```Python
for element in b.flat: 
    element is b's every item
```

## shape

change the shape of an array:the three commands return a modified array,not change the original array:

- `ndarray.ravel()` return a flattened array

- `ndarray.reshape()` the para is some numbers like *a.reshape(3,4)*, return the shape you want. If a dimension is given as -1, then the other dimensions are automatically calculated

- `ndarray.T` thransposed the array

- `ndarray.resize()` will modify the ndarray itself

## Stacking together

- `np.hstack` stack column
- `np.vstake` stack row
- `np.concatenate`

## View and Copies

### No copy at all

1. **simple assignment:** `b=a`

2. **references,like function call** 

    ```Python
    >>> def func(a):
    ...     b = a
    >>> a = np.array()
    >>> func(a)
    ## b is a --> True
    ```

### View or Shallow Copy

creat a new array, but share the same data, when an array's datas change, another will change too.

Slicing an array returns its View

```Python
c = a.view()
c is a --> flase
c.base is a --> true
c.flags.owndata --> false
```


### Deep Copy

make a really new array, and they don't share data together

when to use it?

>  when an array is intermediate, and the result is only a part of it, then we can 
>make a deep copy of the old, and **then** del the old. However, if will just slice
>the old, it only returns a view, even we del the old, as we use the view of the old,
>the old will still persist in the memory.

