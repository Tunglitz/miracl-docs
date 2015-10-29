---
content_type: Chunks
title: Docs MIRACL Users Manual Internal Representation
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

Conventional computer arithmetic facilities as provided by most computer language compilers usually provide one or two floating-point data types (e.g. single and double precision) to represent all the real numbers, together with one or more integer types to represent whole numbers. These built-in data-types are closely related to the underlying computer architecture, which is sensibly designed to work quickly with large amounts of small numbers, rather than slowly with small amounts of large numbers (given a fixed memory allocation). Floating-point allows a relatively small binary number (e.g. 32 bits) to represent real numbers to an adequate precision (e.g. 7 decimal places) over a large dynamic range. Integer types allow small whole numbers to be represented directly by their binary equivalent, or in 2's complement form if negative. Nevertheless this conventional approach to computer arithmetic has several disadvantages.

*   Floating-point and Integer data-types are incompatible. Note that the set of integers, although infinite, is a subset of the rationals (i.e. fractions), which is in turn a subset of the reals. Thus every integer has an equivalent floating-point representation. Unfortunately these two representations will in general be different. For example a small positive whole number will be represented by its binary equivalent as an integer, and as separated mantissa and exponent as a floating-point. This implies the need for conversion routines, to convert from one form to the other.

*   Most rational numbers cannot be expressed exactly (e.g. 1/3). Indeed the floating-point system can only express exactly those rationals whose denominators are multiples of the factors of the underlying radix. For example our familiar decimal system can only represent exactly those rational numbers whose denominators are multiples of 2 and 5; 1/20 is 0.05 exactly, 1/21 is 0.0476190476190.....

*   Rounding in floating-point is base-dependant and a source of obscure errors.

*   The fact that the size of integer and floating-point data types are dictated by the computer architecture, defeats the efforts of language designers to keep their languages truly portable.

*   Numbers can only be represented to a fixed machine-dependent precision. In many applications this can be a crippling disadvantage, for example in the new and growing field of Public-Key cryptography.

*   Base-dependent phenomena cannot easily be studied. For example it would be difficult to access a particular digit of a decimal number, as represented by a traditional integer data-type.

Herein is described a set of standard C routines which manipulate multi-precision rational numbers directly, with multi-precision integers as a compatible subset. Approximate real arithmetic can also be performed.

The two new data-types are called _big_ and _flash_. The former is used to store multi-precision integers, and the latter stores multi-precision fractions as numerator and denominator in ‘floating-slash’ form. Both take the form of a fixed length array of digits, with sign and length information encoded in a separate 32-bit integer. The data type defined as **mr_small** used to store the number digits will be one of the built in types, for example int, long or even double. This is referred to as the “underlying type”.

Both new types can be introduced into the syntax of the C language by the C statements

``` c
    struct bigtype
    {
      mr_unsign32 L;
      mr_small *d;
    };

    typedef struct bigtype *big;

    typedef struct bigtype *flash;
```

Now _big_ and _flash_ variables can be declared just like any built-in data type, e.g.

``` c
	big x,y[10],z[10][10];
```

Observe that a _big_ is just a pointer. The memory needed for each _big_ or _flash_ number instance is taken from the heap (or from the stack). Therefore each _big_ or _flash_ number must be initialised before use, and the required memory assigned to it.

Note that the user of these data-types is not concerned with this internal representation; the library routines allow _big_ and _flash_ numbers to be manipulated directly.

The structure of _big_ and _flash_ numbers is illustrated in figure (4.1).

These structures combine ease of use with representational efficiency. A denominator of length zero (_d=0_), implies an actual denominator of one; and similarly a numerator of length zero (_n=0_) implies a numerator of one. Zero itself is uniquely defined as the number whose first element is zero (i.e. _n=d=0_).   

![](/img/4-1.png)

Figure 4.1:   Structure of _big_ and _flash_ data-types where s is the sign of the number, _n_ and _d_ are the lengths of the numerator and denominator respectively, and LSW and MSW mean ‘Least significant word and ‘Most significant word’ respectively

Note that the slash in the _flash_ data-type is not in a fixed position, and may ‘float’ depending on the relative size of numerator and denominator.

A _flash_ number is manipulated by splitting it up into separate _big_ numerator and denominator components. A _big_ number is manipulated by extracting and operating on each of its component integer elements. To avoid possible overflow, the numbers in each element are normally limited to a somewhat smaller range than that of the full word-length, e.g. 0 to 32767 (= 2<sup>15</sup> - 1) on a 16-bit computer. However with careful programming a full-width base of 2<sup>16</sup> can also be used, as the C language does not report a run-time error on integer overflow [Scott89b].

When the system is initialised the user specifies the fixed number of words (or bytes) to be assigned to all _big_ or _flash_ variables, and the number base to be used. Any base can be used, up to a maximum which is dependent on the word length of the computer used. If requested to use a small base _b_, the system will, for optimal efficiency, actually use base _b<sup>n</sup>_, where _n_ is the largest integer such that _b<sup>n</sup>_ fits in a single computer word. Programs will in general execute fastest if a full-width base is used (achieved by specifying a base of 0 in the initial call to **mirsys**). Note that this mode may be supported by extensive in-line assembly language for certain popular compiler/processor combinations, in certain time-critical routines, for example if using Borland/Turbo C with an 80x86 processor. Examine, for example, the source code in module _mrarth1.c_.

The encoding of the sign and numerator and denominator size information into a single word is possible, as the C language has standard constructs for bit manipulation.