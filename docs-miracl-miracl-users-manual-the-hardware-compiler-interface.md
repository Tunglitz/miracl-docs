---
content_type: Chunks
title: Docs MIRACL Users Manual The Hardware Compiler Interface
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

Hardware/compiler details are specified to MIRACL in this header file _mirdef.h_

For example:-

``` c
    /*
    *  MIRACL compiler/hardware definitions - mirdef.h
    *  This version suitable for use with most 32-bit
    *  computers
    *
    * Copyright (c) 1988-1999 Shamus Software Ltd.
    */

    #define MIRACL_32
    #define MR_LITTLE_ENDIAN

    /* this may need to be changed  */
    #define mr_utype int /* the underlying type is usually int *
                          * but see mrmuldv.any  */
    #define mr_unsign32 unsigned long /* 32 bit unsigned type  */
    #define MR_IBITS  32 /* number of bits in an int */
    #define MR_LBITS  32 /* number of bits in a long */
    #define MR_FLASH 52  /* delete this definition if integer *
                          * only version of MIRACL required  *
                          * Number of bits per double mantissa */

    #define MAXBASE ((mr_small)1<<(MIRACL-1))
    #define MRBITSINCHAR 8

    /* Number of bits in char type  */
    /* #define MR_NOASM  * define this if using C code only  *
     * Note: mr_dltype MUST be defined  */
    /* #define mr_dltype long long
     * double-length type  */

    /* #define MR_STRIPPED_DOWN * define this to minimize size *
     * of library - all error messages *
     * lost! USE WITH CARE - see mrcore.c */
```

This file must be edited if porting to a new hardware environment. Assembly language versions of the time-critical routines in _mrmuldv.any_ may also have to be written, if not already provided, although in most cases the standard C version _mrmuldv.ccc_ can simply be copied to _mrmuldv.c_.

It is best where possible to use the _mirdef.h_ file that is generated automatically by the interactive _config.c_ program.