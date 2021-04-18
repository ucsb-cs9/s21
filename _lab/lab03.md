---
layout: lab
num: lab03
ready: true
desc: "Recursion"
assigned: 2021-04-18 23:59:59.59-7
due: 2021-04-25 23:59:59.59-7
---

In this lab, we'll practice:

* Writing recursive functions based on a specification.
* Practice writing pytests to ensure your recursive functions are correct.

# Instructions

For this lab, you will need to create two files:
* `lab03.py` - file containing your solution to all recursive functions you will implement in this lab.
* `testFile.py` - file containing pytest functions testing all recursive functions you will implement in this lab. **Note:** Gradescope's autograder requires you to submit your `testFile.py` in order for it to run your code (hopefully you're practicing TDD and use your tests to check correctness!). Gradescope will also require you to provide all function definitions (even if incorrect / incomplete) in `lab03.py` in order to run any of the tests.

There will be no starter code for this assignment, but rather function descriptions are given in the specification below.

It's recommended that you organize your lab work in its own directory. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the `import / from` technique shown in lecture.

## Recursive function definitions and specifications

You will write five recursive functions for this lab. Each one is specified below. One example test will be given, but you should write 3 - 5 explicit tests for each function (think of various interesting cases when writing your tests!).

**Note: You must write each function recursively in order to receive any credit, even if Gradescope's tests pass.**

* `power(n,k)` - The parameters `n` and `k` are positive integers (including 0). This function recursively returns `n` to the power of `k` (`n^k`) without explicitly using the `**` operator or a pre-defined function.

```
# Example test
assert power(2,4) == 16
```

* `integerDivision(n,k)` - The parameters `n` and `k` are positive integers (you may assume `n` is >= 0 and `k` is > 0). This function recursively returns the quotient (`n // k`) without explicitly using the `//` operator or a pre-defined function.

```
# Example test
assert integerDivision(27,4) == 6
```

* `collectVowels(s)` - The parameter `s` is a string. This function will recursively return a list where the elements in the list are the vowels that exist in `s` (in the case that appears in `s`). If there are no vowels in `s`, then this function will return an empty list.

```
# Example test
    assert collectVowels("This Is A Sentence") \
        == ['i', 'I', 'A', 'e', 'e', 'e']
```

* `reverseString(s)` - The parameter `s` is a string. This function will return a string in the reverse order of `s`. Note that the reverse of an empty string is an empty string.

```
# Example test
assert reverseString("CMPSC9") == "9CSPMC"
```

* `removeSubString(s, sub)` - The parameters `s` and `sub` are strings that contain at least one character. This function will return a string where all occurrences of `sub` are removed in the order it appears in the string `s` (see example test below for an interesting case). Your solution should not use the string's `replace` method.

```
Example test
assert removeSubString("Lolololol", "lol") == "Loo"
# The first "lol" is removed, which reduces the string 
# to: "Loolol". Then the 2nd "lol" is removed, which 
# reduces the string to: "Loo"
```

## `testFile.py` pytest

This file will contain unit tests using pytest to test if your functionality is correct. Write your tests first in order to check the correctness of your recursive function. Again, Gradescope requires `testfile.py` to be submitted before running any autograded tests. You should write 3 - 5 tests per function.

## Submission

Once you're done with writing your recursive function definitions and tests, submit your `lab03.py` and `testFile.py` files to the `Lab03` assignment on Gradescope. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab.

If the tests don't pass, you may get some error message that may or may not be obvious at this point. Don't worry - if the tests didn't pass, take a minute to think about what may have caused the error. If your tests didn't pass and you're still not sure why you're getting the error, feel free to ask your TAs or Learning Assistants.
