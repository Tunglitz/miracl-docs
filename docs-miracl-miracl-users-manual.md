---
content_type: Chunks
title: Docs MIRACL Users Manual
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

The MIRACL library consists of well over 100 routines that cover all aspects of multi-precision arithmetic. Two new data-types are defined - _big_ for large integers and _flash_ (short for floating-slash) for large rational numbers. The large integer routines are based on Knuth’s algorithms, described in Chapter 4 of his classic work ‘The Art of Computer Programming’. Floating-slash arithmetic, which works with rounded fractions, was originally proposed by D. Matula and P. Kornerup. All routines have been thoroughly optimised for speed and efficiency, while at the same time remaining standard, portable C. However optional fast assembly language alternatives for certain time-critical routines are also included, particularly for the popular Intel 80x86 range of processors. A C++ interface is also provided. Full source code is included.