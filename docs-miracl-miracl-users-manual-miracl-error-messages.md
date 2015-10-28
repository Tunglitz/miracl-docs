---
content_type: Chunks
title: Docs MIRACL Users Manual Error Messages
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

MIRACL error messages, diagnosis and response.

___

**Message:** Number base too big for representation

**Diagnosis:** An attempt has been made to input or output a number using a number base that is too big. For example outputting using a number base of 2<sup>32</sup> is clearly impossible. For efficiency the largest possible internal number base is used, but numbers in this format should be input/output to a much smaller number base £ 256\. This error typically arises when using using _innum_(.) or _otnum_(.) after _mirsys_(.,0_)_.

**Response:** Perform a change of base prior to input/output. For example set the instance variable **IOBASE** to 10, and then use _cinnum_(.) or _cotnum_(.). To avoid the change in number base, an alternatively is to initialise MIRACL using something like _mirsys_(400,16_)_ which uses an internal base of 16\. Now Hex I/O can be performed using _innum_(.) and _otnum_(.). Note that this will not impact performance on a 32-bit processor, as 8 Hex digits will be packed into each computer word.
___

**Message:** Division by zero attempted

**Diagnosis:** Self-explanatory

**Response:** Don't do it!

___

**Message:** Overflow - Number too big

**Diagnosis:** A number in a calculation is too big to be stored in its fixed length allocation of memory.

**Response:** Specify more storage space for all _big_ and _flash_ variables, by increasing the value of _n_ in the initial call to _mirsys_(n.b);

___

**Message:** Internal Result is Negative

**Diagnosis:** This is an internal error that should not occur using the high level MIRACL functions.  It may be caused by user-induced memory over-runs.

**Response:** Report to [mike.scott@miracl.com](mailto:mike.scott@miracl.com)

___

**Message:** Input Format Error

**Diagnosis:** The number being input contains one or more illegal symbols with respect to the current I/O number base. For example this error might occur if **IOBASE** is set to 10, and a Hex number is input.

**Response:** Re-input the number, and be careful to use only legal symbols. Note that for Hex input only upper-case A-F are permissible.  

___

**Message:** Illegal number base

**Diagnosis:** The number base specified in the call to _mirsys_(.) is illegal. For example a number base of 1 is not allowed.

**Response:** Use a different number base.

___

**Message:** Illegal parameter usage

**Diagnosis:** The parameters used in a function call are not allowed. In certain cases certain parameters must be distinct - for example in _divide_(.) the first two parameters must refer to distinct _big_ variables.

**Response:** Read the documentation for the function in question.

___

**Message:** Out of space

**Diagnosis:** An attempt has been made by a MIRACL function to allocate too much heap memory.

**Response:** Reduce your memory requirements. Try using a smaller value of _n_ in your initial call to _mirsys(n,b)._

___

**Message:** Even root of a negative number

**Diagnosis:** An attempt has been made to find, for example, the square root of a negative number.

**Response:** Don't do it!

___

**Message:** Raising integer to negative power

**Diagnosis:** Self-explanatory.

**Response:** Don't do it!

___

**Message:** Integer operation attempted on flash number

**Diagnosis:** Certain functions should only be used with _big_ numbers, and do not make sense for _flash_ numbers. Note that this error message is often provoked by memory problems, where for example the memory allocated to a _big_ variable is accidentally over-written.

**Response:**Don't do it!

___

**Message:** Flash overflow

**Diagnosis:** This error is provoked by Flash overflow or underflow. The result is outside of the representable dynamic range.

**Response:** Use bigger _flash_ numbers. Analyse your program carefully for numerical instability.  

___

**Message:** Numbers too big

**Diagnosis:** The size of _big_ or _flash_ numbers requested in your call to _mirsys(.)_ are simply too big. The length of each _big_ and _flash_ is encoded into a single computer word. If there is insufficient room for this encoding, this error message occurs.

**Response:** Build a MIRACL library that uses a bigger "underlying type". If not using Flash arithmetic, build a library without it - this allows much bigger _big_ numbers to be used.

___

**Message:** Log of a non-positive number

**Diagnosis:** An attempt has been made to calculate the logarithm of a non-positive _flash_ number.

**Response:** Don't do it!

___

**Message:** Flash to double conversion failure

**Diagnosis:** An attempt to convert a Flash number to the standard built-in C _double_ type has failed, probably because the Flash number is outside of the dynamic range that can be represented as a _double._

**Response:** Don't do it!

___

**Message:** I/O buffer overflow

**Diagnosis:** An input output operation has failed because the I/O buffer is not big enough.

**Response:** Allocate a bigger buffer by calling _set_io_buffer_size(.)_ after calling _mirsys(.)_.

___

**Message:** MIRACL not initialised - no call to mirsys()

**Diagnosis:** Self-explanatory

**Response:** Don't do it!

___

**Message:** Illegal modulus

**Diagnosis:** The modulus specified for use internally forMontgomery reduction, is illegal. Note that this modulus must not be even.

**Response:** Use an odd positive modulus.

___

**Message:** No modulus defined

**Diagnosis:** No modulus has been specified, yet a function which needs it has been called.

**Response:** Set a modulus for use internally

___

**Message:** Exponent too big

**Diagnosis:** An attempt has been made to perform a calculation using a pre-computed table, for an exponent (or multiplier in the case of elliptic curves) bigger than that catered for by the pre-computed table.

**Response:** Re-compute the table to allow bigger exponents, or use a smaller exponent.  

___

**Message:** Number base must be power of 2

**Diagnosis:** A small number of functions require that the number base specified in the initial call to _mirsys(.)_ is a power of 2.

**Response:** Use another function, or specify a power-of-2 as the number base in the initial call to _mirsys(.)_

___

**Message:** Specified double-length type isn't

**Diagnosis:** MIRACL has determined that the double length type specified in _mirdef.h_ is in fact not double length. For example if the underlying type is 32-bits, the double length type should be 64 bits.

**Response:** Don't do it!

___

**Message:** Specified basis is not irreducible

**Diagnosis:** The basis specified for GF(2<sup>m</sup>) arithmetic is not irreducible.

**Response:** Don't do it!