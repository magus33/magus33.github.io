# R Tutorial

## Introduction

R is a powerful open‑source language (https://www.R-project.org/) for statistical computing and graphics, created in the early 1990s by Ross Ihaka and Robert Gentleman at the University of Auckland (the name was a play on the proprietary statistical software popular at the time called S, later S-plus). Initially with a statistical focus, it has become one of the best data-science languages.  While a huge number of people have made, and continue to make, contributions to R, a notable push to the standardisation of the language was given by Hadley Wickham and colleagues at RStudio (now Posit, https://posit.co/), who created a standardised ecosystem of packages know as the "tidyverse", as well as providing data publishing tools RShiny and more recently Quarto.  While there is some controversy about how the tidyverse has come to dominate R, at the risk of neglecting other key contributors and frameworks, it is undeniable that the tidyverse offers rapid data prototyping and data display using a flexible, regular and easy to learn syntax. 

*Citation: R Core Team (2021). R: A language and environment for statistical  computing. R Foundation for Statistical Computing, Vienna, Austria.
**Origin story: https://www.stat.auckland.ac.nz/~ihaka/downloads/Otago.pdf

### Preface

There are a huge number of resources for learning R (e.g., see https://r4ds.hadley.nz/, https://rc2e.com/, https://r02pro.github.io/) and so the ambition of this tutorial is small.  As a user of R and other languages over the years, I have been impressed with the capability of R and am delighted to share the learnings I have had with the language.  This documentation seeks to develop a lightweight resource that provides the key knowledge for learning R as I understand it as an experienced data scientist who has used R along with other languages (SQL, R, Python, SAS etc.). It assumes some coding familiarity, or a desire to become familiar, as the goal is to have a condensed understanding of the different data structures available within R and the key properties and methods for each. This document was begun as a self-resource, but I have expanded it and standardised it.

#### Confession

Throughout the documentation, I use the "=" sign as an assignment operator, rather than the dedicated "<-" operator.  While many people prefer the dedicated assignment operator and its functionality (you can assign both ways, "a <- 3" or "3 -> a"), coming from other languages I have never really found it difficult to disambiguate assignment calls from other uses of the equals signs.  This makes me something of a renegade so feel free to ignore in your own coding.

### Base R

The standard library in R that come with the install is the base package (https://cran.r-project.org/doc/manuals/r-devel/packages/base/refman/base.html). 

#### Datatypes

R has the usual basic datatypes:

- numerics (integer, double)
- character ("a string")
- logical (TRUE/FALSE or T/F)
- complex (3 + 2i)
- raw (raw bytes)

Assignment is done dynamically (dynamic typing) without the need for initialisation. 

```R
> x = 1
> typeof(x)
[1] "double"
```
To assign an integer literal, use L as a subscript
```R
> x = 1L
> typeof(x)
[1] "integer"
```

# Common Numeric Operators in Base R

R includes a rich set of numeric operators for arithmetic, comparison, and sequence generation. These are all part of **base R**, so no packages are required.

---

## 🔢 **1. Arithmetic Operators**

| Operator | Meaning | Example | Result |
|---------|---------|---------|--------|
| `+` | Addition | `3 + 2` | `5` |
| `-` | Subtraction | `7 - 4` | `3` |
| `*` | Multiplication | `6 * 3` | `18` |
| `/` | Division | `10 / 4` | `2.5` |
| `^` or `**` | Exponentiation | `2 ^ 3` | `8` |
| `%%` | Modulus (remainder) | `10 %% 3` | `1` |
| `%/%` | Integer division | `10 %/% 3` | `3` |

---

## 🔍 **2. Comparison Operators**

These return **logical values** (`TRUE` or `FALSE`).

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `3 == 3` | `TRUE` |
| `!=` | Not equal to | `3 != 4` | `TRUE` |
| `>` | Greater than | `5 > 2` | `TRUE` |
| `<` | Less than | `2 < 1` | `FALSE` |
| `>=` | Greater or equal | `5 >= 5` | `TRUE` |
| `<=` | Less or equal | `3 <= 1` | `FALSE` |

---

## 🔗 **3. Logical Operators (often used with numeric comparisons)**

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `&` | AND (element-wise) | `c(TRUE, FALSE) & c(TRUE, TRUE)` | `TRUE FALSE` |
| `\|` | OR (element-wise) | `c(TRUE, FALSE) \| c(FALSE, FALSE)` | `TRUE FALSE` |
| `!` | NOT | `!TRUE` | `FALSE` |

### Example
```r
x <- 5
x > 3 & x < 10
[1] TRUE
```

---

**3. Vectors: R’s Most Fundamental Data Structure**

A **vector** is a sequence of elements of the *same* data type. Note that indexing starts at 1 in R (not 0 like in many other languages).


### **Creating vectors**
The combine/concatenate function c(...) is used to create vectors. 

```r
v <- c(1, 2, 3, 4)
names <- c("Alice", "Bob")
flags <- c(TRUE, FALSE, TRUE)
> a = c(1,2)
> b = c(3,4)
> c(a, b)
[1] 1 2 3 4
```

### **Type coercion**
If you mix types, R converts them to the most flexible type:

```r
c(1, "a")       # becomes character
c(TRUE, 2)      # becomes numeric
```

### Naming
Vectors can be named, and then accessed via names. In other operations they behave identically as non-named vectors.

```r
> a <- c(ID = 1234, age=24)
> a["ID"]
[1] 1234
> a[1]
[1] 1234
a[1] + 1
> 1235
> names(a)
[1] c("ID", "age")
```

Vectors can have elements reassigned although this will create a copy of the data
--

## **4. Subsetting Vectors**

R gives you several powerful ways to extract elements.

### **By position**
```r
v
v[1]       # first element
v[2:4]     # positions 2 through 4
v[c(1,3)]  # positions 1 and 3
v[-1]      # all except the first element
v[-c(1,3) # all except positions 1 and 3
```

### **By logical vector**
```r
v[v > 2]   # all elements greater than 2
```

### **By name**
If your vector has names:
```r
ages <- c(Alice = 25, Bob = 30)
ages["Bob"]
```

---



## **5. Mathematical Functions (base R)**

These aren’t operators but are essential for numeric work.

| Function | Example | Result |
|----------|---------|--------|
| `abs()` | `abs(-5)` | `5` |
| `sqrt()` | `sqrt(16)` | `4` |
| `log()` | `log(10)` | natural log |
| `log10()` | `log10(100)` | `2` |
| `exp()` | `exp(1)` | Euler’s number |
| `round()` | `round(3.14159, 2)` | `3.14` |
| `sum()` | `sum(1:5)` | `15` |
| `mean()` | `mean(c(1,2,3))` | `2` |

---



```R
```



## **4. Sequence and Range Operators**

These are numeric but used for generating sequences.
---
### **Colon operator**
```r
1:5      # 1 2 3 4 5
5:1      # 5 4 3 2 1
```

### **seq()**
```r
seq(1, 10, by = 2)      # 1 3 5 7 9
seq(0, 1, length.out = 5)
```

### **rep()**
```r
rep(3, times = 4)       # 3 3 3 3
rep(1:3, each = 2)      # 1 1 2 2 3 3
```
