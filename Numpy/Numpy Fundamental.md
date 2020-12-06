# Array Objects

## Python list 与 Numpy array 的区别

Numpy array 支持多种创建方法，并且可以利用其进行数学运算。array 中的元素一定是同质的，这有利于数学运算。

Python list 允许存储多种类型的元素，这样进行运算时效率较差。

并且 Numpy array 所占存储空间更小，索引更快。

## Numpy array 增维

```python
>>> a = np.array([1,2,3,4,5,6])
>>> a.shape
(6,)
>>> a2 = a[np.newaxis, :]
>>> a2.shape
(1,6)
>>> a3 = a[:, np.newaxis]
>>> a3.shape
(6,1)

>>> a4 = np.expand_dims(a, axis=1)	# axis=1代表列
>>> a4.shape
(6,1)
>>> a4 = np.expand_dims(a, axis=0)	# axis=0代表行
(1,6)
```

## 选取满足条件的元素

```python
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])	# (2,4)
>>> print(a[a < 5])
[1 2 3 4]

# 使用条件来索引array
>>> five_up = (a >= 5)
>>> print(a[five_up])
[5 6 7 8 9 10 11 12]

# You can select elements that are divisible by 2:
>>> divisible_by_2 = a[a%2==0]
>>> print(divisible_by_2)
[ 2  4  6  8 10 12]

# Or you can select elements that satisfy two conditions using the & and | operators:
>>> c = a[(a > 2) & (a < 11)]
>>> print(c)
[ 3  4  5  6  7  8  9 10]

# You can also make use of the logical operators & and | in order to return boolean values that specify whether or not the values in an array fulfill a certain condition. This can be useful with arrays that contain names or other categorical values.
>>> five_up = (a > 5) | (a == 5)
>>> print(five_up)
[[False False False False]
 [ True  True  True  True]
 [ True  True  True True]]

# You can also use np.nonzero() to select elements or indices from an array.
# 如果不存在，则返回空数组
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
>>> b = np.nonzero(a < 5)
>>> print(b)
(array([0, 0, 0, 0]), array([0, 1, 2, 3]))

# If you want to generate a list of coordinates where the elements exist, you can zip the arrays, iterate over the list of coordinates, and print them.
>>> list_of_coordinates= list(zip(b[0], b[1]))
>>> for coord in list_of_coordinates:
...     print(coord)
(0, 0)
(0, 1)
(0, 2)
(0, 3)

# You can also use np.nonzero() to print the elements in an array that are less than 5 with:
>>> print(a[b])
[1 2 3 4]
```

