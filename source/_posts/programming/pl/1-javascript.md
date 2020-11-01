---
title: Programming Language Chapter 1
categories: 
- Programming
- PL
tags:
- Programming
- PL
- Javascript
language: en-US
---

<div align="center" style="font-size: 33px"><b>
    Chapter 1: Javascript
    <div style="font-size: 15px">and First Class Functions</div>
</b></div>

## History of Javascript

Javascript originally targets explicitly for browsers. Netscape, a browser that is extremely popular in the 90s, asked Brendan Eich to design an "HTML scripting language" that had to look like Java on the basis of Scheme, another language at that time. Well, brilliant Eich finished the language in **10 days** and they later called it Javascript, JS for short. Since they didn't change anything and directly embedded the made-in-10-day language into their browser, it so happens that some designs of Javascript are considered poor, even though people tried to fix them later. An example is the mind-blowing type conversion. That's why Microsoft later developed Typescript in top of Javascript to restrict the types. 

## Components in Javascript

### Functions

Let's look at the definition of functions in Javascript.

```js
function(x) {
    return x + 1;
}
```

Functions in Javascript are **first class**, meaning that they can be used **just like a variable**. The above example is an anonymous function that has no use. A newer way to write this is using **lambda expressions** `(x) => x + 1`, but they have some differences. Now, let's give it a name.

```js
function f1(x) {
    return x + 1;
}

var f2 = function (x) {
    return x + 1;
}
```

Both ways are fine, and they can be used as variables. That's why they are **first class functions**. Let's write another function and make use of these variables.

```js
function apply(f, x) {
    return f(x);
}

f(f1, 2)   // -> 3
f(f2, 2)   // -> 3
```

> I said before that the type conversion is bad in JS. Here is how. Just guess what is `f1("5")`. Yes, it's `"51"`. This may be OK, but here comes the strange thing. Try `f1([])`. It will be `"1"`. `f([1, 2])` will be `"1,21"`. This is because oprands on both sides will be converted to `string` if the interpretor doesn't know how to evaluate the operation. This will bring wierd bugs sometimes, and you can read more in [wtfjs][wtfjs].

Here, `apply` is called a **higher order function**. This kind of functions either takes a function as an argument, or returns a function.

### Closures

Another important concept in Javascript is **closure**. A function definition "captures" variables in its context, which can be used if the function is called later.

```js
function counter() {
    var count = 0;
    return function () {
        count += 1;
        console.log(count);
    }
}

var c = counter();
c();    // > 1
c();    // > 2
```

This is an important concept because we will be using it all the time later when we talk about currying and continuations. Also, here, `counter` is a higher order function. Let's just look at a more complicated example. We will **never** have to understand it, just look at how functions can be and laziness play a role in that!

```js
function y(g) {
    return function (f) {
        return f(f);
    }(function (f) {
        return g(function (x) {
            return f(f)(x);
        });
    });
}

var fact = y(function (fact) {
    return function (n) {
        return (n <= 2) ? n : n * fact(n - 1);
    }
});

fact(5)    // -> 120
```

### Objects

Objects are basically hashmaps or dictionaries in Javascript. However, to make the language Object Oriented, objects without **prototypes** are not enough. Let's look firstly at objects without prototypes.

```js
var obj = {
    x: 3,
    f: function () { return this.x; }
}

obj.f()   // -> 3
```

Here, you can see the structure of this object. You can access the members by `.` **or** `[...]`. Actually, objects and arrays in Javascript are the same except that when accessing using index notation `[key]`, `key` for objects must be (or will be converted to) string, and `key` for arrays must be (or will be converted to) Number. Members can be added or modified using dot or index notation, and can be deleted by `delete` keyword followed by the member you want to delete, e.g. `delete obj.f`.

Further, `this` is a pointer pointing to the object that **owns** the function as a **method**. In python, it's even more clear:

```python
class A():
    def __init__(self, x):
        self.x = x

    def f(self):
        return self.x

A(3).f()   # -> 3
```

Here, `self` explicitly goes into the arguments and when the method is called, the object pointer is passed in **implicitly**. 

Now, let's look at the Javascript way of defining a class like Python above. 

```js
function A(x) {
    this.x = x;
    this.f = function () {
        return this.x;
    };
}

var a = new A(3);
a.f()   // -> 3
```

Like Python, the complexity of ojbects in Javascript comes from the concept of **prototypes** of objects. However, since our focus is not on objects for now, let's skip this part. Our focus is on "functions," and from this point we are going to think in a **functional** way.

## References

1. https://en.wikipedia.org/wiki/JavaScript#Creation_at_Netscape


<hr>
<h6 align="right"><a href="#">Next</a> | <a href="/programming/pl/preface">Home</a></h6>


[wtfjs]: https://github.com/denysdovhan/wtfjs
