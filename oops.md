# Overloading & Overriding

Method overriding in Python is an object-oriented programming concept that allows a subclass (child class) to provide a specific implementation for a method that is already defined in its superclass (parent class). 


```python
def sum_num(*args):
    result=0
    for num in args:
        result+=num
    print('sum:',result)
print("single arg")
sum_num(10)
print('mul arg')
sum_num(10,20)
sum_num(10,20,30,40,50,60)
```

    single arg
    sum: 10
    mul arg
    sum: 30
    sum: 210
    


```python
def fun(a):
    print('hello')
def fun(a,b):
    print('hello')
def fun(a,b,c):
    print('hello')
fun(10,20,30)
```

    hello
    

### Method overriding

A Child class method overrides the parent class method of the same name,parameters and return type It is used to overwrite or redefine a parent class method in the derived class


```python
class A:
    def first(self):
        print('First fuction of class A')
    def second(self):
        print('Second function of class A')
class B(A):
    def first(self):
        print('redefined function')
    def display(self):
        print('display function of child class')
obj=B()
obj.first()
obj.second()
obj.display()
```

    redefined function
    Second function of class A
    display function of child class
    

### Operator overloading

- Giving extended meaning beyond their predefined operational meaning
<pre>
 + --> addtwo integer
   --> join two string
   --> marge two list
</pre>

some built in operator shows different behavior for objects of different class


```python
class A:
    def __init__(self,a):
        self.a=a
    def __add__(self,other):
        return self.a+other.a
obj1=A(5)
obj2=A(2)
obj3=A('hello')
obj4=A('HI')
print(obj1+obj2)
print(obj3+obj4)
print(obj1.__add__(obj2))
print(A.__add__(obj1,obj2))
```

    7
    helloHI
    7
    7
    


```python
class A:
    def __init__(self,a):
        self.a=a
    def __gt__(self,other):
        if self.a>other.a:
            return True
        return False
obj1=A(1)
obj2=A(7)
if obj1>obj2:
    print('obj1 is greater')
else:
    print('obj2 is greater')
```

    obj2 is greater
    

## Methematical operators

    operator               magic method
       +                    __add__(self,other)
       -                    __sub__(self,other)
       *                    __mul__(self,other)
       /                    __truediv__(self,other)
       //                   __floordiv__(self,other)
       %                    __mod__(self,other)
       **                   __pow__(self,other)
       >                    __gt__(self,other)
       <                    __lt__(self,other)
       >=                   __ge__(self,other)
       <=                   __le__(self,other)
       ==                   __eq__(self,other)
       !=                   __ne__(self,other)


```python
class A:
    def __init__(self,a):
        self.a=a
    def __sub__(self,other):
        return self.a-other.a
    def __mul__(self,other):
        return self.a*other.a
    def __pow__(self,other):
        return self.a**other.a
    def __truediv__(self,other):
        return self.a/other.a
    def __floordiv__(self,other):
        return self.a//other.a
obj1=A(2)
obj2=A(6)
obj3=A(10)
print(obj1-obj2)
print(obj1*obj3)
print(obj3/obj2)
print(obj3//obj2)
print(obj1**obj3)


```

    -4
    20
    1.6666666666666667
    1
    1024
    

## Inheritance

![image.png](attachment:image.png)

# 1 single Inheritance


```python
class parent:
    def func1(self):
        print('Hello parent')
class child(parent):
    def func2(self):
        print('hello child')
obj=child()
obj.func1()
obj.func2()
```

    Hello parent
    hello child
    


```python
#Multiple Inheritance
class a:
    def f1(self):
        print('a')
class b:
    def f2(self):
        print('b')
class c:
    def f2(self):
        print('c')
class d(a,c,b):
    def f2(self):
        print('d')
obj=d()
print(d.__mro__)
obj.f1()
obj.f2()
# obj.f3()
```

    (<class '__main__.d'>, <class '__main__.a'>, <class '__main__.c'>, <class '__main__.b'>, <class 'object'>)
    a
    d
    


```python
# 3 Multilevel inheritance
class a:
    pass
class b(a):
    pass
class c(b):
    pass
```


```python
# 4 hierarchical inheritance
class a:
    pass
class c1(a):
    pass
class c2(a):
    pass
```


```python
class a:
    def f1(self):
        print('f1')
class b(a):
    def f2(self):
        print('f2')
class c(a):
    def f3(self):
        print('f3')
class d(c,b):
    def f4(self):
        print('f4')
obj=d()
print(d.__mro__)
```

    (<class '__main__.d'>, <class '__main__.c'>, <class '__main__.b'>, <class '__main__.a'>, <class 'object'>)
    

# super()


```python
class parent:
    def __init__(self):
        self.attr1=50
        self.attr2=60
class child(parent):
    def __init__(self):
        super().__init__()#parent.__init__(self)
        self.attr3=45
obj=child()
print(obj.attr3)
print(obj.attr2)
print(obj.attr1)
```

    45
    60
    50
    

### issubclass()


```python
class parent:
    def func1(self):
        print('Hello parent')
class child(parent):
    def func2(self):
        print('hello child')
print(issubclass(child,parent))
print(issubclass(parent,child))
```

    True
    False
    

### isinstance()


```python
A=child()
B=parent()
print(isinstance(A,child))
print(isinstance(A,parent))
print(isinstance(B,child))
print(isinstance(B,parent))

```

    True
    True
    False
    True
    

# Method Resolution order(MRO)

MRO stands for Method Resolution Order in Python. It is the sequence in which Python searches for methods and attributes within a class hierarchy, especially in scenarios involving multiple inheritance


```python
class a:
    def f1(self):
        print('a')
class b(a):
    def f2(self):
        print('b')
class c(a):
    def f2(self):
        print('c')
class d(c,b):
    def f2(self):
        print('d')
obj=d()
print(d.__mro__)
print(d.mro())
```

    (<class '__main__.d'>, <class '__main__.c'>, <class '__main__.b'>, <class '__main__.a'>, <class 'object'>)
    [<class '__main__.d'>, <class '__main__.c'>, <class '__main__.b'>, <class '__main__.a'>, <class 'object'>]
    


```python
class p1:
    def foo(self):
        print('foo from p1')
class p2:
    def foo(self):
        print('foo from p2')
    def bar(self):
        print('bar from p2')
class c1(p1,p2):
    pass
class c2(p2,p1):
    def bar(self):
        print('bar from c2')
class gc(c1,c2):
    pass
obj=gc()
obj.bar()
obj.foo()
print(gc.mro())
    
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-24-b24999b0dac7> in <module>
         12     def bar(self):
         13         print('bar from c2')
    ---> 14 class gc(c1,c2):
         15     pass
         16 obj=gc()
    

    TypeError: Cannot create a consistent method resolution
    order (MRO) for bases p1, p2


# Abstract class


```python
from abc import ABC
class class_name(ABC):
    #body of class
#abc-->abstract base class
```


```python
from abc import ABC,abstractmethod
class shape(ABC):
    def __init__(self,shape_name):
        self.shape_name=shape_name
        
    @abstractmethod
    def draw(self):
        print('Drawing:',self.shape_name)
class circle(shape):
        def __init__(self):
            super().__init__('circle')
        def draw1(self):
            print(super().draw())
            print('Drawing:',self.shape_name)
        def draw(self):
            print('hi')
class B(circle):
    def draw(self):
        print('Drawing:',self.shape_name)
    
obj=B()
obj.draw()
```

    Drawing: circle
    


```python
class Book:
    def __init__(self,name,l,publisher,isbn,year):
        self.name=name
        self.l=l
        self.no_of_authers=len(self.l)
        self.publisher=publisher
        self.isbn=isbn
        self.year=year
    def display(self):
        print(f"Name: {self.name} number of books:{self.no_of_authers} list:{self.l} ISBN:{self.isbn} year:{self.year}")
class coursebook(Book):
    def __init__(self,name,l,publisher,isbn,year,coursename):
        super().__init__(name,l,publisher,isbn,year)
        self.coursename=coursename
    def display(self):
        super().display()
        print(self.coursename)
obj=coursebook('xyz',[],'lj','1','2026','Python')
obj.display()
```

    Name: xyz number of books:0 list:[] ISBN:1 year:2026
    Python
    


```python
class student:
    def __init__(self,rollno,name,age,totalmarks):
        self.rollno=rollno
        self.name=name
        self.age=age
        self.totalmarks=totalmarks
    def display(self):
        print(self.rollno,self.name,self.age,self.totalmarks)
    def __eq__(self,other):
        return self.totalmarks==other.totalmarks
a=student(1,'')
```


```python
class bill:
    
    def __init__ (self):
        self.b=0
        self.hd=5000
        self.ram=2000
        self.printer=6000
        self.pd=800
        
        print('HDD 5000')
        print('Add to cart y/n',end='')
        t=input(':')
        if t in'yY':
            n=int(input('Enter quantity:'))
            self.b+=self.hd*n
          
        print('ram 2000')
        print('Add to cart y/n',end='')
        t=input(':')
        if t in'yY':
            n=int(input('Enter quantity:'))
            self.b+=self.ram*n
        
        print('printer 6000')
        print('Add to cart y/n',end='')
        t=input(':')
        if t in'yY':
            n=int(input('Enter quantity:'))
            self.b+=self.printer*n
        
        print('pendrive 800')
        print('Add to cart y/n',end='')
        t=input(':')
        if t in'yY':
            n=int(input('Enter quantity:'))
            self.b+=self.pd*n
        
        print('1.Cash Payment')
        print('2.cheque Payment')
        a=int(input('Enter 1/2:'))
        if a==1:
            cashpayment(self.b)
        else:
            chequepayment(self.b)
        
class cashpayment(bill):
    def __init__ (self,total):
        self.total=total
        d={}
        print(self.total)
        d[2000]=f"{self.total//2000} Notes"
        self.total=self.total%2000
        d[500]=f"{self.total//500} Notes"
        self.total=self.total%500
        d[100]=f"{self.total//100} Notes"
        self.total=self.total%100
        
        print(d)
        
class chequepayment(bill):
    def __init__ (self):
        n=int(input('Enter cheque number'))
        s=input('Enter bankname')
        print(n,s)
        print('payment complete')
a=bill()
```

    HDD 5000
    Add to cart y/n:y
    Enter quantity:1
    ram 2000
    Add to cart y/n:y
    Enter quantity:2
    printer 6000
    Add to cart y/n:y
    Enter quantity:1
    pendrive 800
    Add to cart y/n:y
    Enter quantity:1
    1.Cash Payment
    2.cheque Payment
    Enter 1/2:1
    15800
    {2000: '7 Notes', 500: '3 Notes', 100: '3 Notes'}
    

# numpy


```python
import numpy as np
import sys

s=range(1000)
print('Size of each element of list in bytes',sys.getsizeof(s))
print('size of whole list in bytes:',sys.getsizeof(s)*len(s))
```

    Size of each element of list in bytes 48
    size of whole list in bytes: 48000
    


```python
d=np.arange(1000)
print('Size of each element of Numpy array in bytes',d.itemsize)
print(d.itemsize*d.size)
```

    Size of each element of Numpy array in bytes 4
    4000
    


```python
import numpy as np
arr=np.array(42)
print(type(arr))
print(arr.ndim)# 1d 2d 3d

```

    <class 'numpy.ndarray'>
    0
    


```python
import numpy as np
arr=np.array([[1,2,3,4]])
print(type(arr))
print(arr)
print(arr.ndim)
```

    <class 'numpy.ndarray'>
    [[1 2 3 4]
     [1 2 3 4]]
    2
    


```python
import numpy as np
arr=np.array([[[1,2,3,4],[1,2,3,4]],[[1,2,4,3],[1,2,3,3]]])
print(type(arr))
print(arr)
print(arr.ndim)

```

    <class 'numpy.ndarray'>
    [[[1 2 3 4]
      [1 2 3 4]]
    
     [[1 2 4 3]
      [1 2 3 3]]]
    3
    


```python
import numpy as np
arr=np.array([[1,2,3,4,5],[6,7,8,9,10]])
print(arr[:1,:3])

```

    [[1 2 3]]
    


```python
print(arr.shape)
```

    (2, 5)
    


```python
arr=np.array([1,2,3,4,5,6])
print(arr.reshape(3,2))
```

    [[1 2]
     [3 4]
     [5 6]]
    


```python
import numpy as np
arr=np.array([1,2,3,4,5,6])
newarr=arr.reshape(-1,2)
print(newarr)
for x in arr:
    print(x)
```

    [[1 2]
     [3 4]
     [5 6]]
    1
    2
    3
    4
    5
    6
    


```python
arr=np.array([[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]])
for i in np.nditer(arr):
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    


```python
arr=np.array([[1,2,3,4],[5,6,7,8]])
for x in np.nditer(arr[0:1,1::2]):
    print(x)

```

    2
    4
    


```python
for x in np.nditer(arr[:,::2]):
    print(x)
```

    1
    3
    5
    7
    

# Built-in function

## concatenate()


```python
arr1=np.array([1,2,3])
arr2=np.array([4,5,6])
arr3=np.array([7,8,9])
arr5=np.concatenate((arr1,arr2,arr3))
print(arr5)
```

    [1 2 3 4 5 6 7 8 9]
    


```python
arr1=np.array([[1,2],[5,6]])
arr2=np.array([[3,4],[7,8]])
arr5=np.concatenate((arr1,arr2),axis=1)
print(arr5)
```

    [[1 2 3 4]
     [5 6 7 8]]
    

## split()


```python
arr1=np.array([1,2,3,4])
newarr=np.array_split(arr1,4)
print(newarr)
```

    [array([1]), array([2]), array([3]), array([4])]
    


```python
arr1=np.array([1,2,3,4])
newarr=np.array_split(arr1,3)
print(newarr)
```

    [array([1, 2]), array([3]), array([4])]
    


```python
arr1=np.array([1,2,3,4])
newarr=np.array_split(arr1,2)
print(newarr)
```

    [array([1, 2]), array([3, 4])]
    


```python
arr1=np.array([1,2,3,4])
newarr=np.array_split(arr1,1)
print(newarr)
```

    [array([1, 2, 3, 4])]
    


```python
arr1=np.array([1,2,3,4])
newarr=np.array_split(arr1,5)
print(newarr)
```

    [array([1]), array([2]), array([3]), array([4]), array([], dtype=int32)]
    


```python
arr1=np.array([1,2,3,4])
newarr=np.array_split(arr1,6)
print(newarr)
```

    [array([1]), array([2]), array([3]), array([4]), array([], dtype=int32), array([], dtype=int32)]
    


```python
arr1=np.array([[1,2],[3,4],[5,6],[7,8]])
newarr=np.array_split(arr1,4,axis=1)
print(newarr)
```

    [array([[1],
           [3],
           [5],
           [7]]), array([[2],
           [4],
           [6],
           [8]]), array([], shape=(4, 0), dtype=int32), array([], shape=(4, 0), dtype=int32)]
    

## where


```python
arr1=np.array([1,2,3,4,5,6,4,2,3])
x=np.where(arr1==4)
print(x)
```

    (array([3, 6], dtype=int64),)
    


```python
y=np.where(arr1%2==0)
print(y)
```

    (array([1, 3, 5, 6, 7], dtype=int64),)
    


```python
arr1=np.array([[1,2],[3,4],[5,6],[4,8]])
x=np.where(arr1==4)
print(x)
```

    (array([1, 3], dtype=int64), array([1, 0], dtype=int64))
    


```python
arr=np.array([[[1,4,3],[4,5,6]],[[7,8,4],[4,11,12]]])
x=np.where(arr==4)
print(x)
```

    (array([0, 0, 1, 1], dtype=int64), array([0, 1, 0, 1], dtype=int64), array([1, 0, 2, 0], dtype=int64))
    

# sort()


```python
arr1=np.array([1,2,3,4,5,6,4,3,2])
print(np.sort(arr1))
```

    [1 2 2 3 3 4 4 5 6]
    


```python
arr1=np.array([[3,4,2],[1,7,3],[4,2,5]])
print(np.sort(arr1,axis=1))
```

    [[2 3 4]
     [1 3 7]
     [2 4 5]]
    


```python
arr1=np.array([True,False,True])
print(np.sort(arr1))
```

    [False  True  True]
    


```python
arr=np.array([[[3,2,8],[7,9,3]],[[6,7,2],[9,6,4]]])
print(np.sort(arr,axis=1))
```

    [[[3 2 3]
      [7 9 8]]
    
     [[6 6 2]
      [9 7 4]]]
    


```python
arr=np.array([[[3,2,8],[7,9,3]],[[6,7,2],[9,6,4]]])
print(np.sort(arr,axis=2))
```

    [[[2 3 8]
      [3 7 9]]
    
     [[2 6 7]
      [4 6 9]]]
    

# Random module


```python
from numpy import random
x=random.randint(10,100,size=(5))
print(x)
```

    [85 95 85 18 17]
    


```python
from numpy import random
x=random.randint(10,100,size=(3,5))
print(x)
```

    [[55 12 92 93 11]
     [82 13 10 69 62]
     [76 32 29 12 67]]
    


```python
x=random.rand(5)*10
print(x)
```

    [1.93858205 7.32891014 2.85507548 7.11193986 3.71775075]
    


```python
x=random.rand(3,5)*10
print(x)
```

    [[6.63308139 3.72004298 9.90861788 6.63976484 4.81886474]
     [7.2591574  5.64662556 9.76046243 4.82933557 0.94464426]
     [6.82792176 1.61269234 9.78937372 7.39470022 8.89996471]]
    


```python
x=random.choice([1,2,3,4,5,6],size=(5))
print(x)
```

    [5 1 2 5 2]
    


```python
#number gassing game
from numpy import random
a=7
n=random.randint(1,101)
while a>0:
    i=int(input('Enter a number:'))
    if n==i:
        print('You won')
        break
    else:
        a=a-1
        if n<i:
            print('num is lower')
        else:
            print('num is higher')
        if a==0:
            print('you lose')
            print('correct number is:',n)
            break
        print(f'{a} attempt left try again')
    
```

    Enter a number:1
    num is higher
    6 attempt left try again
    Enter a number:5
    num is higher
    5 attempt left try again
    Enter a number:89
    num is lower
    4 attempt left try again
    Enter a number:67
    You won
    


```python

```


```python

```
