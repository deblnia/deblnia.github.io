---
date: 2021-03-23
draft: true 
tags:
- notes
title: Advanced R Bookclub
---

## Chapter 2: Names and Values 

- The `<-` creates an assignment, or binding 
  - A shared binding is when the same object is bound / assigned to two names 
- R is pass-by-reference (e.g. assignments point to memory addresses) but also has copy-on-modify (so the values in an object is copied when one binding is changed)
  - can use `tracemem()` to see what's pointing to what, but make sure to turn it off (`untracemem()`)
  - vectors are copied in their entirety when modified, but lists are copied piece by piece (e.g. modifiying one element changes the reference for that element)
- R deep copies by default (python does not)
- R stores characters in a global string pool that can be accessed from anywhere, by any function or object 
> More on the global string pool [here](https://stackoverflow.com/questions/29701721/object-size-for-characters-in-r-how-does-r-global-string-pool-work)
- `lobstr::obj_size()` can be used to tell how big an object is (`utils::object.size` can also be used for the same purpose, but does not account for shared references so can be inaccurate)
- Environments can be modified in place as well (and created using `rlang::env()`)
  - They are not deep copied by default! 
- `read.csv()` coerces non-syntactic names to syntactic names using `make.names()` which is irreversible and can corrupt data

## Chapter 3: Vectors 

- Atomic vectors must all be of the same type, lists can be of different types 
![Description of Types](https://d33wubrfki0l68.cloudfront.net/eb6730b841e32292d9ff36b33a590e24b6221f43/57192/diagrams/vectors/summary-tree-atomic.png)
  - Raw types holds raw bytes
  - Integers are followed by `L` e.g. anything longer than 32 bits will be stored as a double
- Vectors also have attributes (list of metadata including length and class)
  - Individual attributes can be retrieved and modified with `attr()`, or retrieved en masse with `attributes()`, and set en masse with `structure()`.
  - Think of them as ephemeral (most attributes dropped except for name and dimensions)
      - Names e.g. `c(first = "deblina", last = "mukherjee", id = 1)` or can be assigned piece by piece using the `names()` or `setNames()` functions)
      - Dimensions allow vectors to behave like a 2D matrix or multi-dimensional array 
- A matrix is a collections of elements of the same data type arranged in a fixed number of rows and columns (create using the `matrix()` function)
- An array can store data of similar types in more than two dimensions (e.g. array of dimension 2,3,4 creates 4 rectangular matrices each with 2 rows and 3 columns)
  - create using the `array()` function 
  - used in image processing
- Can also modify arrays and matrices in place using `dim()` 
  - `dim()` returns NULL for 1D vector (can't use `nrow()` or `ncol()` of 1D vector either)
- Having a class attribute makes something an S3 object (e.g. factors, date, datetime, difftimes)
  - factors can be ordered, don't forget `StringsasFactors = False`
  - times are doubles with attributes
- NULL is zero length vector with no attributes, NA is a sentinel (absence) value 
  - Use `is.na()` to test for missing-ness, because there's no reason to believe one missing value has the same value as the others (so == doesn't work)
  - There are type specific NAs, but type coerced 
  - Use NULLs to represent an empty or absent vector
- `c()` stands for combine / concatenate 
- Coersion occurs in the following order: character → double → integer → logical
- Lists can contain any atomic type or even other lists 
  - elements are references, they do not copy
  - data frames are a named list of vectors with attributes for column names, row names, and class data.frame 
    - must have same length 
    - need to use `rownames()` or `colnames()` with these, as `names()` are column names 
- Tibbles do less and complain more 
  - discourages rownames 
  - prints prittier 
  - strings are not factors 

## Chapter 4: Subsetting 

- Three subsetting operators (`[`, `[]`, and `$`) and six ways to subset atomic vectors
  -`[]` always returns another list while `[[]]` returns a single element
  - In a matrix it's RowsxColumns 
- Real numbers are truncated down when indexing
- Can use indexing to duplicate (recycling rules apply), can't use negative and positive indices in the same index
- Can also subset using logical vectors 
  - Subsetting with a single element (e.g. `df[1,]`) will return an object with lower dimensionality (can prevent this with the `drop = F` argument)
- Need to name elements to subset using character string 
- `pluck()` is also useful (along with the other list flattening variants)

## Chapter 5: Control Flow 

- If you don't give else for base if, defaults to return NULL 
- Base if/else is not vectorized, so only first element is evaluated
- Base if/else coerces types of branches to same (vectorized `if_else()` in tidyverse will throw warning)
- Switch is not vectorized, good for strings (no double quote)
- `repeat()` can produce a vector

## Chapter 6: Functions

- Everything that exists in R is an object, everything that happens is a function call 
- Primitive functions that call C code have types of NULL or base 
- Anonymous functions are just not bound to name 
- Can call functions with `do.call()` 
- Lexical Scoping (looks up values based on how function is defined not how its called)
  - Name masking -- uses the names defined inside a function first, then next environment 
  - 


