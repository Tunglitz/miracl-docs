---
content_type: Chunks
title: Docs MIRACL Users Manual The MIRACL Routines
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

> Note: In these routines a _big_ parameter can also be used wherever a _flash_ > is specified, but not visa-versa. Further information may be gleaned from the > (lightly) commented source code. An asterisk * after the name indicates that
> the function does not take a _mip_ parameter if **MR\_GENERIC\_MT**  is
> defined in _mirdef.h_. See Section 2.3 for more details.

## 9.1  Low level routines

### 9.1.1  absol *

**Function:**  void **absol**(x,y)

flash x,y;

**Module:**  mrcore.c

**Description:**  Gives absolute value of a big or flash number.

**Parameters:**  Two big/flash variables _x_ and _y_. On exit _y_=|_x_|.

**Return value:**  None

**Restrictions:**  None

### 9.1.2  add

**Function:**  void **add**(x,y,z)

big x,y,z;

**Module:**  mrarth0.c

**Description:**  Adds two big numbers.

**Parameters:**  Three big numbers _x_, _y_ and _z_. On exit _z=x+y_.

**Return value:**  None

**Restrictions:**  None

**Example:**

``` c
	add(x,x,x);  /* This doubles the value of _x_. */  
```

### 9.1.3  brand

**Function:**  int **brand**()

**Module:**  mrcore.c

**Description:**  Generates random integer number

**Parameters:**  None

**Return Value:**  A random integer number

**Restrictions:**  First use must be preceded by an initial call to **irand**.

> Note: This generator is not cryptographically strong. For cryptographic
> applications, use the **strong\_rng** routine.

### 9.1.4  bigbits

**Function:**  void **bigbits**(n,x)

int n;
big x;

**Module:**  mrbits.c

**Description:**  Generates a big random number of given length. Uses the built-in simple random number generator initialised by **irand.**

**Parameters:**  A big number _x_ and an integers _n_. On exit _x_ contains a big random number _n_ bits long.

**Return value:**  None

**Restrictions:**  None

**Example:**

``` c
    //This generates a 100 bit random number
    bigbits(100,x);
```

### 9.1.5  big\_to\_bytes

**Function:**  int **big\_to\_bytes**(max,x,ptr,justify)

int max;
big x;
char *ptr;
BOOL justify

**Module:**  mrarth1.c

**Description:**  Converts a positive big number _x_ into a binary octet string

**Parameters:**  A big number _x_ and a byte array _ptr_ of length _max_. Error checking is carried out to ensure that the function does not write beyond the limits of _ptr_ if _max>0_. If _max_=0, no checking is carried out. If _max_>0 and _justify_=TRUE, the output is right-justified, otherwise leading zeros are suppressed.

**Return value:**  The number of bytes generated in _ptr_. If _justify_=TRUE then the return value is _max_.

**Restrictions:**  _max_ must be greater than 0 if _justify_=TRUE  

### 9.1.6  bytes\_to\_big

**Function:**  void **bytes\_to\_big**(len,ptr,x)

int len;
char *ptr;
big x;

**Module:**  mrarth1.c

**Description:**  Converts a binary octet string to a big number. Binary to big conversion.

**Parameters:**  A pointer to a byte array _ptr_ of length _len_, and a big result _x_.

**Return value:**  None

**Restrictions:**  None

**Example:** 

``` c
    /*
     *  test program to exercise big_to_bytes() and bytes_to_big()
     */

    #include <stdio.h>
    #include "miracl.h"

    int main()
    {
      int i,len;
      miracl *mip=mirsys(100,0);
      big x,y;
      char b[200]; /* b needs space allocated to it */
      x=mirvar(0);  /* all big variables need to be "mirvar"ed */
      y=mirvar(0);
      expb2(100,x);
      incr(x,3,x);  /* x=2^100 + 3 */
      len=big_to_bytes(200,x,b,FALSE);
      
      /* Now b contains big number x in raw binary */
      /* it is len bytes in length */
      /* now print out the raw binary number b in hex */
      for (i=0;i<len;i++) printf("%02x",b[i]);
      printf("\n");
      bytes_to_big(len,b,y);
      
      /* now convert it back to big format, and print it out again */
      mip->IOBASE=16;
      cotnum(y,stdout);
      return 0;
    }  
```

### 9.1.7  cinnum

**Function:**  int **cinnum**(x,f)

flash x;
FILE *f;

**Module:**  mrio2.c

**Description:**  Inputs a flash number from the keyboard or a file, using as number base the current value of the instance variable IOBASE. Flash numbers can be entered using either a slash '/' to indicate numerator and denominator, or with a radix point.

**Parameters:**  A big/flash number _x_ and a file descriptor _f_. For input from the keyboard specify _f_ as _stdin_, otherwise as the descriptor of some other opened file. To force input of a fixed number of bytes, set the instance variable INPLEN to the required number, just before calling **cinnum**.

**Return value:**  The number of input characters.

**Restrictions:**  None

**Example:**  mip->IOBASE=256;

``` c
    mip->INPLEN=14;  /* This inputs 14 bytes from _fp_ and */
    cinnum(x,fp);  /* converts them into big number _x_  */
```

### 9.1.8  cinstr

**Function:**  int **cinstr**(x,s)

flash x;
char *s;

**Module:**  mrio2.c

**Description:**  Inputs a flash number from a character string, using as number base the current value of the instance variable IOBASE. Flash numbers can be input using a slash '/' to indicate numerator and denominator, or with a radix point.

**Parameters:**  A big/flash number _x_ and a string _s_.

**Return value:**  The number of input characters.

**Restrictions:**  None

**Example:**

``` c
    /* input large hex number into big x */
    mip->IOBASE=16;
    cinstr(x,"AF12398065BFE4C96DB723A");
```

### 9.1.9  compare

**Function:**  int **compare**(x,y)

big x,y;

**Module:**  mrcore.c

**Description:**  Compares two big numbers.

**Parameters:**  Two big numbers _x_ and _y_.

**Return value:**  Returns +1 if _x > y_, returns 0 if _x = y_, returns -1 if _x < y_.

**Restrictions:**  None

### 9.1.10  convert

**Function:**  void **convert**(n,x)

int n;
big x;

**Module:**  mrcore.c

**Description:**  Convert an integer number to big number format.

**Parameters:**  An integer _n_ and a big number _x_.

**Return value:**  None

**Restrictions:**  None

### 9.1.11  copy

**Function:**  void **copy**(x,y)

flash x,y;

**Module:**  mrcore.c

**Description:**  Copies a big or flash number to another.

**Parameters:**  Two big or flash numbers _x_ and _y_. On exit _y=x_. Note that if _x_ and _y_ are the same variable, no operation is performed.

**Return value:**  None

**Restrictions:**  None

### 9.1.12  cotnum

**Function:**  int **cotnum**(x,f)

flash x;
FILE *f;

**Module:**  mrio2.c

**Description:**  Output a big or flash number to the screen or to a file, using as number base the value currently assigned to the instance variable IOBASE. A flash number will be converted to radix-point representation if the instance variable RPOINT=ON. Otherwise it will be output as a fraction.

**Parameters:**  A big/flash number _x_ and a file descriptor _f_. If _f_ is _stdout_ then output will be to the screen, otherwise to the file opened with descriptor _f_.

**Return value:**  Number of output characters.

**Restrictions:**  None

**Example:**

``` c
    //This outputs _x_ in hex, to the file associated with _fp_.
    mip->IOBASE=16;
    cotnum(x,fp);
```

### 9.1.13  cotstr

**Function:**  int **cotstr**(x,s)

flash x;
char *s;

**Module:**  mrio2.c

**Description:**  Output a big or flash number to the specified string, using as number base the value currently assigned to the instance variable IOBASE. A flash number will be converted to radix-point representation if the instance variable RPOINT=ON. Otherwise it will be output as a fraction.

**Parameters:**  A big/flash number _x_ and a string _s_. On exit _s_ will contain a representation of the number _x_.

**Return value:**  Number of output characters.

**Restrictions:**  Note that there is nothing to prevent this routine from overflowing the limits of the user supplied character array _s_, causing obscure runtime problems. It is the programmers responsibility to ensure that _s_ is big enough to contain the number output to it. Alternatively use the internally declared instance string **IOBUFF**, which is of size **IOBSIZ**. If this array overflows a MIRACL error **will** be flagged.

### 9.1.14  decr**

**Function:**  void **decr**(x,n,z)

big x,z;
int n;

**Module:**  mrarth0.c

**Description:**  Decrement a big number by an integer amount.

**Parameters:**  Big numbers _x_ and _z_, and integer _n._

On exit _z=x-n_.

**Return value:**  None

**Restrictions:**  None  

### 9.1.15  divide

**Function:**  void **divide**(x,y,z)

big x,y,z;

**Module:**  mrarth2.c

**Description:**  Divides one big number by another.

**Parameters:**  Three big numbers _x_, _y_ and _z_. On exit _z=x/y_; _x=x mod y_. The quotient only is returned if _x_ and _z_ are the same, the remainder only if _y_ and _z_ are the same.

**Return value:**  None

**Restrictions:**  Parameters _x_ and _y_ must be different, and _y_ must be non-zero.

**Example:**

``` c
//This sets _x_ equal to the remainder when _x_ is divided by _y_. The quotient is not returned.
divide(x,y,y);
```

### 9.1.16  divisible

**Function:**  BOOL **divisible**(x,y)

big x,y;

**Module:**  mrarth2.c

**Description:**  Tests a big number for divisibility by another

**Parameters:**  Two big numbers _x_ and _y_.

**Return value:**  TRUE if _y_ divides _x_ exactly, otherwise FALSE

**Restrictions:**  The parameter _y_ must be non-zero.

### 9.1.17  ecp_memalloc

**Function:**  void \***ecp\_memalloc**(n)

int n;

**Module:**  mrcore.c

**Description:**  Reserves space for _n_ elliptic curve points in one heap access. Individual points can subsequently be initialised from this memory by calling **epoint\_init\_mem**.

**Parameters:**  The number _n_ of elliptic curve points to reserve space for.

**Return value:**  A pointer to the allocated memory.

**Restrictions:**  None.

### 9.1.18  ecp\_memkill

**Function:**  void **ecp\_memkill**(mem,n)

char *mem;
int n;

**Module:**  mrcore.c

**Description:**  Deletes and sets to zero the memory previously allocated by **ecp_memalloc**

**Parameters:**  A pointer to the memory to be erased and deleted, and the size of that memory in elliptic curve points.

**Return value:**  None

**Restrictions:**  Must be preceded by a call to **ecp\_memalloc**

### 9.1.19  exsign

**Function:**  int **exsign**(x)

flash x;

**Module:**  mrcore.c

**Description:**  Extracts the sign of a big/flash number.

**Parameters:**  A big/flash number _x_.

**Return value:**  The sign of _x_, i.e. -1 if _x_ is negative, +1 if _x_ is zero or positive.

**Restrictions:**  None

### 9.1.20  getdig

**Function:**  int **getdig**(x,i)

big x;
int i;

**Module:**  mrcore.c

**Description:**  Extracts a digit from a big number.

**Parameters:**  A big number _x_, and the required digit _i_.

**Return value:**  The value of the requested digit.

**Restrictions:**  Returns rubbish if required digit does not exist.

### 9.1.21  get\_mip

**Function:**  miracl \***get\_mip**(void)

**Module:**  mrcore.c

**Description:**  Get the current Miracl Instance Pointer

**Parameters:**  None

**Return value:**  The _mip_ - Miracl Instance Pointer – for the current thread.

**Restrictions:**  This function does not exist if **MR\_GENERIC\_MT** is defined.  

### 9.1.22  igcd

**Function:**  int **igcd**(x,y)

int x,y;

**Module:**  mrcore.c

**Description:**  Calculates the Greatest Common Divisor of two integers using Euclids Method.

**Parameters:**  Two integers _x_ and _y_

**Return value:**  The GCD of _x_ and _y_

### 9.1.23  incr

**Function:**  void **incr**(x,n,z)

big x,z;
int n;

**Module:**  mrarth0.c

**Description:**  Increment a big variable.

**Parameters:**  Big numbers _x_ and _z_, and an integer _n_. On exit _z=x+n_.

**Return value:**  None

**Restrictions:**  None

**Example:**  incr(x,2,x);  /* This increments x by 2\. */

### 9.1.24  init\_big\_from\_rom

**Function:**  BOOL **init\_big\_from\_rom**(big,int,const mr_small\*,int,int\*)

big x;
int len;
const mr_small \*rom;
int romsize;
int \*romptr;

**Module:**  mrcore.c

**Description:**  Initialises a big variable from ROM memory.

**Parameters:**  A big number _x_ and its length in computer words. The address of ROM memory which stores up to _romsize_ computer words, and a pointer into the ROM. This pointer is incremented internally as ROM memory is accessed to fill _x_.

**Return value:**  TRUE if successful, or FALSE if an attempt is made to read beyond the end of the ROM

### 9.1.25  init\_point\_from\_rom

**Function:**  BOOL **init\_point\_from\_rom**(epoint \*,int,const mr_small\*,int,int\*)

epoint \*P;
int len;
const mr_small *rom;
int romsize;
int \*romptr;

**Module:**  mrcore.c

**Description:**  Initialises an elliptic curve point from ROM memory.

**Parameters:**  An elliptic curve point _P_ and its length of its two big coordinates in computer words. The address of ROM memory which stores up to _romsize_ computer words, and a pointer into the ROM. This pointer is incremented internally as ROM memory is accessed to fill _P_.

**Return value:**  TRUE if successful, or FALSE if an attempt is made to read beyond the end of the ROM

### 9.1.26  innum

**Function:**  int **innum**(x,f)

flash x;
FILE \*f;

**Module:**  mrio1.c

**Description:**  Inputs a big or flash number from a file or the keyboard, using as number base the value specified in the initial call to **mirsys**. Flash numbers can be entered using either a slash '/' to indicate numerator and denominator, or with a radix point.

**Parameters:**  A big/flash number _x_ and a file descriptor _f_. For input from the keyboard specify _f_ as _stdin_, otherwise as the descriptor of some other opened file.

**Return value:**  The number of characters input.

**Restrictions:**  The number base specified in **mirsys** must be less than or equal to 256\. If not use **cinnum** instead.

**Hint:**  For fastest inputting of ASCII text to a big number, and if a full-width base is possible, use mirsys(...,256); initially. This has the same effect as specifying mirsys(...,0);, except that now ASCII bytes may be input directly via innum(x,fp); without the time-consuming change of base implicit in the use of **cinnum**.

### 9.1.27  insign

**Function:**  void **insign**(s,x)

int s;
flash x;

**Module:**  mrcore.c

**Description:**  Forces a big/flash number to a particular sign.

**Parameters:**  A big/flash number _x_, and the sign _s_ that it is to take. On exit _x=s.|x_|.

**Return value:**  None

**Restrictions:**  None

**Example:**

``` c
insign(PLUS,x);  /* force _x_ to be positive */  
```

### 9.1.28  instr

**Function:**  int **instr**(x,s)

flash x;
char \*s;

**Module:**  mrio1.c

**Description:**  Inputs a big or flash number from a character string, using as number base the value specified in the initial call to **mirsys**. Flash numbers can be entered using either a slash '/' to indicate numerator and denominator, or with a radix point.

**Parameters:**  A big/flash number _x_ and a character string _s_.

**Return value:**  The number of characters input.

**Restrictions:**  The number base specified in **mirsys** must be less than or equal to 256\. If not use **cinstr** instead.

### 9.1.29  irand

**Function:**  void **irand**(seed)

long seed;

**Module:**  mrcore.c

**Description:**  Initializes internal random number system. Long integer types are used internally to yield a generator with maximum period.

**Parameters:**  A long integer seed, which is used to start off the random number generator.

**Return value:**  None

**Restrictions:**  None

### 9.1.30  lgconv

**Function:**  void **lgconv**(ln,x)

long ln;
big x;

**Module:**  mrcore.c

**Description:**  Converts a long integer to big number format

**Parameters:**  A long integer _ln_ and a big number _x_

**Return value:**  None

**Restrictions:**  None

### 9.1.31  mad

**Function:**  void **mad**(x,y,z,w,q,r)

big x,y,z,w,q,r;

**Module:**  mrarth2.c

**Description:**  Multiply add and divide big numbers. The initial product is stored in a double-length internal variable to avoid the possibility of overflow at this stage.

**Parameters:**  Six big numbers _x,y,z,w,q_ and _r_. On exit _q=(x.y+z)/w_ and _r_ contains the remainder. If _w_ and _q_ are not distinct variables then only the remainder is returned; if _q_ and _r_ are not distinct then only the quotient is returned. The addition of _z_ is not done if _x_ and _z_ (or _y_ and _z_) are the same.

**Return value:**  None

**Restrictions:**  Parameters _w_ and _r_ must be distinct. The value of _w_ must not be zero.

**Example:**

``` c
	mad(x,x,x,w,x,x); /* _x=x^2/w_ */
```

### 9.1.32  memalloc

**Function:**  void \***memalloc**(n)

int n;

**Module:**  mrcore.c

**Description:**  Reserves space for _n_ big variables in one heap access. Individual big/flash variables can subsequently be initialised from this memory by calling **mirvar_mem**.

**Parameters:**  The number _n_ of big/flash variables to reserve space for.

**Return value:**  A pointer to the allocated memory.

**Restrictions:**  None.  

### 9.1.33  memkill

**Function:**  void **memkill**(mem,n)

char \*mem;
int n;

**Module:**  mrcore.c

**Description:**  Deletes and sets to zero the memory previously allocated by **memalloc**

**Parameters:**  A pointer to the memory to be erased and deleted, and the size of that memory in bigs.

**Return value:**  None

**Restrictions:**  Must be preceded by a call to **memalloc**

### 9.1.34  mirexit

**Function:**  void **mirexit**()

**Module:**  mrcore.c

**Description:**  Cleans up after the current instance of MIRACL, and frees all internal variables. A subsequent call to **mirsys** will re-initialise the MIRACL system.

**Parameters:**  None

**Return value:**  None

**Restrictions:**  Must be called after **mirsys**.

### 9.1.35  mirkill

**Function:**  void **mirkill**(x)

big x;

**Module:**  mrcore.c

**Description:**  Securely kills off a big/flash number by zeroising it, and freeing its memory.

**Parameters:**  A big/flash number _x_.

**Return Value:** None  

### 9.1.36  mirsys

**Function:**  miracl ***mirsys**(nd,nb)

int nd,nb;

**Module:**  mrcore.c

**Description:**  Initialise the MIRACL system for the current program thread, as described below. Must be called before attempting to use any other MIRACL routines.

(1)  The error tracing mechanism is initialised.

(2)  the number of computer words to use for each big/flash number is calculated from _nd_ and _nb_.

(3)  Sixteen big work variables (four of them double length) are initialised.

(4)  Certain instance variables are given default initial values.

(5)  The random number generator is started by calling **irand(0L)**.

**Parameters:**  The number of digits _nd_ to use for each big/flash variable and the number base _nb_. If _nd_ is negative it is taken as indicating the size of big/flash numbers in 8-bit bytes.

**Return value:**  The Miracl Instance Pointer, via which all instance variables can be accessed, or NULL if there was not enough memory to create an instance.

**Restrictions:**  The number base _nb_ should normally be greater than 1 and less than or equal to MAXBASE. A base of 0 implies that the 'full-width' number base should be used. The number of digits _nd_ must be less than a certain maximum, depending on the underlying type _mr_utype_ and on whether or not **MR_FLASH** is defined. (See _mirdef.h_)

**Example:**

``` c
//This initialises the MIRACL system to use 500 decimal digits for each big or flash number.
miracl *mip=mirsys(500,10);
```

### 9.1.37  mirvar

**Function:**  flash **mirvar**(iv)

int iv;

**Module:**  mrcore.c

**Description:**  Initialises a big/flash variable by reserving a suitable number of memory locations for it. This memory may be released by a subsequent call to the function **mirkill**.

**Parameters:**  An integer initial value for the big/flash number.

**Return value:**  A pointer to the reserved memory.

**Restrictions:**  None

**Example:**

``` c
    //Creates a flash variable _x=8_.
    flash x;
    x=mirvar(8);
```

### 9.1.38  mirvar\_mem

**Function:**  flash **mirvar\_mem**(mem,index)

char \*mem;
int index;

**Module:**  mrcore.c

**Description:**  Initialises memory for a big/flash variable from a pre-allocated byte array _mem_. This array may be created from the heap by a call to **memalloc**, or in some other way. This is quicker than multiple calls to **mirvar**.

**Parameters:**  A pointer to the pre-allocated array _mem_, and an index into that array. Each index should be unique.

**Return value:**  An initialised big/flash variable

**Restrictions:**  Sufficient memory must have been allocated and pointed to by _mem_.

**Example:**  See _brent.c_ for an example of use.

### 9.1.39  multiply

**Function:**  void **multiply**(x,y,z)

big x,y,z;

**Module:**  mrarth2.c

**Description:**  Multiplies two big numbers

**Parameters:**  Three big numbers _x,y_ and _z_. On exit _z=x.y_

**Return value:**  None

**Restrictions:**  None

### 9.1.40  negify

**Function:**  void **negify**(x,y)

flash x,y;

**Module:**  mrcore.c

**Description:**  Negates a big/flash number.

**Parameters:**  Two big/flash numbers _x_ and _y_. On exit _y=-x_.

**Return value:**  None

**Restrictions:**  None. Note that negify(x,x) is valid and sets _x=-x_

### 9.1.41  normalise

**Function:**  int **normalise**(x,y)

big x,y;

**Module:**  mrarth2.c

**Description:** Multiplies a big number such that its Most Significant Word is greater than half the number base. If such a number is used as a divisor by **divide**, the division will be carried out faster. If many divisions by the same divisor are required, it makes sense to normalise the divisor just once beforehand.

**Parameters:**  Two big numbers _x_ and _y_. On exit _y=n.x_.

**Return value:**  Returns _n_, the normalising multiplier.

**Restrictions:**  Use with care. Used internally.

### 9.1.42  numdig

**Function:**  int **numdig**(x)

big x;

**Module:**  mrcore.c

**Description:**  Determines the number of digits in a big number.

**Parameters:**  A big number _x_.

**Return value:**  The number of digits in _x_.

**Restrictions:**  None

### 9.1.43  otnum

**Function:**  int **otnum**(x,f)

flash x;
FILE \*f;

**Module:**  mrio1.c

**Description:** Output a big or flash number to the screen or to a file, using as number base the value specified in the initial call to **mirsys**. A flash number will be converted to radix-point representation if the instance variable RPOINT=ON. Otherwise it will be output as a fraction.

**Parameters:** A big/flash number _x_ and a file descriptor _f_. If _f_ is _stdout_ then output will be to the screen, otherwise to the file opened with descriptor _f_.

**Return value:**  Number of output characters.

**Restrictions:** The number base specified in **mirsys** must be less than or equal to 256\. If not, use **cotnum** instead.

### 9.1.44 otstr

**Function:**  int **otstr**(x,s)

flash x;
char *s;

**Module:**  mrio1.c

**Description:** Output a big or flash number to the specified string, using as number base the value specified in the initial call to **mirsys**. A flash number will be converted to radix-point representation if the instance variable RPOINT=ON. Otherwise it will be output as a fraction.

**Parameters:** A big/flash number _x_ and a character string _s_. On exit _s_ will contain a representation of _x_.

**Return value:**  Number of output characters.

**Restrictions:** The number base specified in **mirsys** must be less than or equal to 256\. If not, use **cotstr** instead.

> Note that there is nothing to prevent this routine from overflowing the limits > of the user supplied character array _s_, causing obscure runtime problems. It > is the programmers responsibility to ensure that _s_ is big enough to contain > the number output to it. Alternatively use the internally declared instance
> string **IOBUFF**, which is of size **IOBSIZ**. If this array overflows a
> MIRACL error **will** be flagged.

### 9.1.45  premult

**Function:**  void **premult**(x,n,z)

int n
big x,z;

**Module:**  mrarth1.c

**Description:**  Multiplies a big number by an integer

**Parameters:**  Two big numbers _x_ and _z_, and an integer _n_.

On exit _z=n.x_

**Return value:**  None

**Restrictions:**  None  

### 9.1.46  putdig

**Function:**  void **putdig**(n,x,i)

big x;
int i,n;

**Module:**  mrcore.c

**Description:**  Set a digit of a big number to a given value

**Parameters:**  A big number _x_, a digit number _i_, and its new value _n_.

**Return value:**  None

**Restrictions:**  The digit indicated must exist.

### 9.1.47  remain

**Function:**  int **remain**(x,n)

big x;
int n;

**Module:**  mrarth1.c

**Description:**  Finds the integer remainder, when a big number is divided by an integer.

**Parameters:**  A big number _x_, and an integer _n_.

**Return value:**  The integer remainder  

### 9.1.48  set\_io\_buffer\_size

**Function:**   void set_io_buffer_size(len)

int len;

**Module:**  mrcore.c

**Description:**  Sets the size of the input/output buffer. By default this is set to 1024, but programs that need to handle very large numbers may require a larger I/O buffer.

**Parameters:**  The size of I/O buffer required.

**Return value:**  None

**Restrictions:**  Destroys the current contents of the I/O buffer

### 9.1.49  set\_user\_function

**Function:**  void set\_user\_function(func)

BOOL (*user)(void);

**Module:**  mrcore.c

**Description:**  Supplies a user-specified function, which is periodically called during some of the more time-consuming MIRACL functions, particularly those involved in modular exponentiation and in finding large prime numbers. The supplied function must take no parameters and return a BOOL value. Normally this should be TRUE. If FALSE then MIRACL will attempt to abort its current operation. In this case the function should continue to return FALSE until control is returned to the calling program. The user-supplied function should normally include only a few instructions, and no loops, otherwise it may adversely impact the speed of MIRACL functions.

Once MIRACL is initialised, this function may be called multiple times with a new supplied function. If no longer required, call with a NULL parameter.

**Parameters:**  A pointer to a user-supplied function, or NULL if not required.

**Return value:**  None

**Example:**

``` c
    /* Windows Message Pump */
    static BOOL idle()
    {
        MSG msg;
        if (PeekMessage(&msg,NULL,0,0,PM_NOREMOVE))
        {
            if (msg.message!=WM_QUIT)
            {
                if (PeekMessage(&msg,NULL,0,0,PM_REMOVE))
                { /* do a Message Pump */
                    TranslateMessage(&msg);
                    DispatchMessage(&msg);
                }
            }
            else
                return FALSE;
        }
        return TRUE;
    }
    ...
    set_user_function(idle);
```

### 9.1.50  size *

**Function:**  int **size**(x)

big x;

**Module:**  mrcore.c

**Description:**  Tries to convert big number to a simple integer. Also useful for testing the sign of big/flash variable as in: if (size(x) < 0) ...

**Parameters:**  A big number _x_.

**Return value:**  The value of _x_ as an integer. If this is not possible (because _x_ is too big) it returns the value plus or minus **MR_TOOBIG.**

**Restrictions:**  None

### 9.1.51  subdiv

**Function:**  int **subdiv**(x,n,z)

int n;
big x,z;

**Module:**  mrarth1.c

**Description:**  Divide a big number by an integer.

**Parameters:**  Two big numbers _x_ and _z_, and an integer _n_.

On exit _z=x/n_.

**Return value:**  The integer remainder.

**Restrictions:**  The value of _n_ must not be zero.

### 9.1.52  subdivisible

**Function:**  BOOL **subdivisible**(x,n)

big x;
int n;

**Module:**  mrarth1.c

**Description:**  Tests a big number for divisibility by an integer.

**Parameters:**  A big number _x_ and an integer _n_.

**Return value:**  TRUE is _n_ divides _x_ exactly, otherwise FALSE.

**Restrictions:**  The value of _n_ must not be zero.

### 9.1.53  subtract

**Function:**  void **subtract**(x,y,z)

big x,y,z;

**Module:**  mrarth0.c

**Description:**  Subtracts two big numbers.

**Parameters:**  Three big numbers _x_, _y_ and _z_. On exit _z=x-y_.

**Return value:**  None

**Restrictions:**  None

### 9.1.54  zero *

**Function:**  void **zero**(x)

flash x;

**Module:**  mrcore.c

**Description:**  Sets a big or flash number to zero

**Parameters:**  A big or flash number _x_.

**Return value:**  None

## 9.2  Advanced Arithmetic Routines

### 9.2.1  bigdig

**Function:**  void **bigdig**(n,b,x)

int n,b;
big x;

**Module:**  mrrand.c

**Description:**  Generates a big random number of given length. Uses the built-in simple random number generator initialised by **irand.**

**Parameters:** A big number _x_ and two integers _n_ and _b_. On exit _x_ contains a big random number _n_ digits long to base _b_.

**Return value:**  None

**Restrictions:**  The base _b_ must be printable, that is 2 £ _b_ £ 256.

**Example:**

``` c
    //This generates a 100 decimal digit random number
    bigdig(100,10,x);
```

### 9.2.2  bigrand

**Function:**  void **bigrand**(w,x)

big w,x;

**Module:**  mrrand.c

**Description:**  Generates a big random number. Uses the built-in simple random number generator initialised by **irand.**

**Parameters:**  Two big numbers _w_ and _x_. On exit _x_ is a big random number in the range _0__£x < w_.

**Return value:**  None

**Restrictions:**  None

###9.2.3  brick\_init

**Function:**  BOOL **brick\_init**(binst,g,n,w,nb)

brick *binst;
big g,n;
int w,nb;

**Module:**  mrbrick.c

**Description:**  Initialises an instance of the Comb method for modular exponentiation with precomputation. Internally memory is allocated for 2_<sup>w</sup>_ big numbers which will be precomputed and stored. For bigger _w_ more space is required, but the exponentiation is quicker. Try _w_=8.

**Parameters:**  A pointer to the current instance _binst_, the fixed generator _g_, the modulus _n_, the window size _w_, and the maximum number of bits to be used in the exponent _nb_.

**Return value:**  TRUE if all went well, FALSE if there was a problem.

Restrictions:  Note: If MR_STATIC is defined in _mirdef.h_, then the _g_ parameter in this function is replaced by an mr_small * pointer to a precomputed table. In this case the function returns a void.

### 9.2.4  brick\_end

**Function:**  void **brick\_end**(binst)

brick \*binst

**Module:**  mrbrick.c

**Description:**  Cleans up after an application of the Comb method.

**Parameters:**  A pointer to the current instance

**Return value:**  None

**Restrictions:**  None   

### 9.2.5  crt

**Function:**  void **crt**(pbc,rem,x)

big_chinese \*pbc;
big \*rem;
big x;

**Module:**  mrcrt.c

**Description:** Applies Chinese Remainder Theorem.

**Parameters:**  A pointer _pbc_ to the current instance. On exit _x_ contains the big number which yields the given big remainders _rem[.]_ when it is divided by the big moduli specified in a prior call to **crt_init**.

**Return value:**  None

**Restrictions:**  The routine **crt_init** must be called first.

### 9.2.6  crt\_end

**Function:**  void **crt_end**(pbc)

big_chinese \*pbc;

**Module:**  mrcrt.c

**Description:**  Cleans up after an application of the Chinese Remainder Theorem.

**Parameters:**  A pointer to the current instance of the Chinese Remainder Theorem.

**Return value:**  None

**Restrictions:**  None

### 9.2.7  crt_init

**Function:**  BOOL **crt\_init**(pbc,np,m)

big_chinese *pbc;
int np;
big *m;

**Module:**  mrcrt.c

**Description:**  Initialises an instance of the Chinese Remainder Theorem. Some internal workspace is allocated.

**Parameters:**  A pointer to the current instance _pbc_, the number of co-prime moduli _np_, and an array of at least two big moduli _m[.]_

**Return value:**  TRUE if all went well, FALSE if there was a problem.

**Restrictions:**  None

### 9.2.8  egcd

**Function:**  int **egcd**(x,y,z)

big x,y,z;

**Module:**  mrgcd.c

**Description:**  Calculates the Greatest Common Divisor of two big numbers.

**Parameters:**  Three big numbers _x, y_ and _z_.

On exit _z=gcd(x,y)_

**Return value:**  GCD as integer, if possible, otherwise **MR_TOOBIG**

**Restrictions:**  None

### 9.2.9  expb2

**Function:**  void **expb2**(n,x)

int n;
big x;

**Module:**  mrbits.c

**Description:**  Calculates 2 to the power of an integer as a big

**Parameters:**  An integer _n_, and a big result _x_.

On exit _x=2<sup>n</sup>._

**Return value:**  None

**Restrictions:**  None

**Example:**

``` c
    //This calculates and prints out the largest known prime number (on a true 32-
    //bit computer with lots of memory!)
    expb2(1398269,x);
    decr(x,1,x);
    mip->IOBASE=10;
    cotnum(x,stdout);
```

### 9.2.10  expint

**Function:**  void **expint**(b,n,x)

int b,n;
big x;

**Module:**  mrarth3.c

**Description:**  Calculates an integer to the power of an integer as a big

**Parameters:**  An integer _b_, an integer _n_, and a big result _x_.

On exit _x=b<sup>n</sup>._

**Return value:**  None

**Restrictions:**  None

### 9.2.11  fft\_mult

**Function:**  void **fft\_mult**(x,y,z)

big x,y,z;

**Module:**  mrfast.c

**Description:**  Multiplies two big numbers, using the Fast Fourier Method. See [Pollard71].

**Parameters:**  Three big numbers _x, y_ and _z_. On exit _z=x.y_

**Return value:**  None

**Restrictions:**  Should only be used on a 32-bit computer when _x_ and _y_ are very large, at least 1000 decimal digits.

**Example:**

> See _mersenne.c_

### 9.2.12  gprime

**Function:**  void **gprime**(n)

int n;

**Module:**  mrprime.c

**Description:**  Generates all prime numbers up to a certain limit into the instance array PRIMES, terminated by zero. This array is used internally by the routines **isprime** and **nxprime**.

**Parameters:**  A positive integer _n_ indicating the maximum prime number to be generated. If _n=0_ the PRIMES array is deleted.

**Return value:**  None

### 9.2.13  hamming

**Function:**  int **hamming**(n)

big n;

**Module:**  mrarth1.c

**Description:**  Calculates the hamming weight of a big number (in fact the number of 1's in its binary representation.)

**Parameters:**  A big number _x_.

**Return value:**  Hamming weight of  _x_

### 9.2.14  invers

**Function:**  unsigned int **invers**(x,y)

unsigned int x,y;

**Module:**  mrsmall.c

**Description:**  Calculates the inverse of an integer modulus a co-prime integer

**Parameters:**  An integer _x_ and a co-prime integer _y_.

**Return value:**  _x<sup>-1</sup>  mod y_

**Restrictions:**  Result unpredictable if _x_ and _y_ not co-prime  

### 9.2.15  isprime

**Function:**  BOOL **isprime**(x)

big x;

**Module:**  mrprime.c

**Description:**  Tests whether or not a big number is prime using a probabilistic primality test. The number is assumed to be prime if it passes this test **NTRY** times, where **NTRY** is an instance variable with a default initialisation in routine **mirsys**.

> NOTE: This routine first test divides _x_ by the list of small primes stored
> in the instance array **PRIMES**. The testing of larger primes will be
> significantly faster in many cases if this list is increased. See **gprime**.
> By default only the small primes less than 1000 are used.

**Parameters:**  A big number _x_.

**Return value:**  Returns the boolean value TRUE if _x_ is (almost certainly) prime, otherwise FALSE.

**Restrictions:**  None

### 9.2.16  jac

**Function:**  int **jac**(x,n)

unsigned int x,n;

**Module:**  mrsmall.c

**Description:**  Calculates the value of the Jacobi symbol. See [Reisel].

**Parameters:**  Two unsigned numbers _x_ and _n_

**Return value:**  The value of _(x/n)_ as +1 or -1, or 0 if symbol undefined

**Restrictions:**  None

### 9.2.17  jack

**Function:**  int **jack**(x,n)

big x,n;

**Module:**  mrjack.c

**Description:**  Calculates the value of the Jacobi symbol. See [Reisel].

**Parameters:**  Two big numbers _x_ and _n_

**Return value:**  The value of _(x/n)_ as +1 or -1, or 0 if symbol undefined

**Restrictions:**  None

### 9.2.18  logb2

**Function:**  int **logb2**(x)

big x;

**Module:**  mrbits.c

**Description:**  Calculates the approximate integer log to the base 2 of a big number (in fact the number of bits in it.)

**Parameters:**  A big number _x_.

**Return value:**  Number of bits in _x_

**Restrictions:**  None

### 9.2.19  lucas

**Function:**  void **lucas**(x,e,n,vp,v)

big x,e,n,vp,v

**Module:**  mrlucas.c

**Description:**  Performs Lucas modular exponentiation.  Uses Montgomery arithmetic internally. This function can be speeded up further for particular moduli, by invoking special assembly language routines to implement Montgomery arithmetic. See **powmod**.

**Parameters:**  Five big numbers _x, e, n, vp_ and _v_.

On exit _v_=V_<sub>e</sub>_(_x_) mod _n_ and _vp_=V_<sub>e-1</sub>_(_x_) mod _n_ where _n_ is the current Montgomery modulus. Only _v_ is returned if _v_ and _vp_ are not distinct.

**Return value:**  None

**Restrictions:**  The value of _n_ must be odd.

> Note:  The "sister" Lucas function U_<sub>e</sub>(x)_ can, if required,  be calculated as

U_<sub>e</sub>(x)_ _º_ _[x._V_<sub>e</sub>(x)– 2._V_<sub>e-1</sub>(x)]/(x<sup>2</sup> – 4)_ mod _n_

### 9.2.20  multi_inverse

**Function:**  BOOL **multi_inverse**(m,x,n,w)

int m;
big n;
big *x,*w;

**Module:**  mrxgcd.c

**Description:**  Finds the modular inverses of many numbers simultaneously, exploiting Montgomery's observation that _x_<sup>-1</sup> _= y.(xy)_<sup>-1</sup>_,  y_<sup>-1</sup> _= x.(xy)_<sup>-1</sup>. This will be quicker, as modular inverses are slow to calculate, and this way only one is required.

**Parameters:**  The number of inverses required _m_, an array _x_[.] of _m_ numbers whose inverses are wanted, the modulus _n_, and the resulting  array of inverses _w_[.].

**Return value:**  TRUE if successful, otherwise FALSE.

**Restrictions:**  The parameters _x_ and _w_ must be distinct.

### 9.2.21  nres

**Function:**  void **nres**(x,y)

big x,y;

**Module:**  mrmonty.c

**Description:**  Converts a big number to _n-residue_ form.

**Parameters:**  Two big numbers _x_ and _y_.

On exit _y_ is the _n-residue_ form of _x_.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty**.

### 9.2.22  nres\_dotprod

**Function:**  void **nres_dotprod**(m,x,y,w)

int m;
big x[],y[],w;

**Module:**  mrmonty.c

**Description:**  Finds the dot product of two arrays of _n-residues_. So-called "lazy" reduction is used, in that the sum of products is only reduced once with respect to theMontgomery modulus. This is quicker –nearly twice as fast.

**Parameters:**  Two arrays _x_ and _y_ each of _m_ _n-residues._

On exit _w=__S x<sub>i</sub> y<sub>i</sub>_mod _n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty**.

### 9.2.23  nres\_double\_modadd

**Function:**  void **nres\_double\_modadd**(x,y,w)

big x,y,w;

**Module:**  mrmonty.c

**Description:**  Adds two double length bigs modulo _p.R_, where _R_ is 2_<sup>n</sup>_ and _n_ is the smallest multiple of the word-length of the underlying MIRACL type, such that _R>p_. This is required for lazy reduction.

**Parameters:**  Three big numbers _x_, _y_ and _z_. On exit _z=a+b_ mod _pR_

**Return value:**  None  

### 9.2.24  nres\_double\_modsub

**Function:**  void **nres\_double\_modsub**(x,y,w)

big x,y,w;

**Module:**  mrmonty.c

**Description:**  Subtracts two double length bigs  modulo _p.R_, where _R_ is 2_<sup>n</sup>_ and _n_ is the smallest multiple of the word-length of the underlying MIRACL type, such that _R>p_. This is required for lazy reduction.

**Parameters:**  Three big numbers _x_, _y_ and _z_. On exit _z=a-b_ mod _pR_

**Return value:**  None

### 9.2.25  nres\_lazy

**Function:**  void **nres\_lazy**(a,b,c,d,x,y)

big a,b,c,d,x,y;

**Module:**  mrmonty.c

**Description:**  Uses the method of lazy reduction combined with Karatsuba's method to multiply two zzn2 variables. Requires just 3 multiplications and two modular reductions.

**Parameters:**   Six big numbers. On exit _(x+iy)=(a+ib)(c+id)_, where _i_ is imaginary square root of the quadratic non-residue.

**Return value:**  None

### 9.2.26  nres\_lucas

**Function:**  void **nres\_lucas**(x,e,vp,v)

big x,e,vp,v;

**Module:**  mrlucas.c

**Description:**  Modular Lucas exponentiation of an _n-residue_

**Parameters:**  An _n-residue_ _x_, a big exponent _e_, and two _n-residue_ outputs _vp_ and _v_.

On exit _v_=V_<sub>e</sub>_(_x_) mod _n_ and _vp_=V_<sub>e-1</sub>_(_x_) mod _n_ where _n_ is the current Montgomery modulus. Only _v_ is returned if _v_ and _vp_ are the same big variable.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of the first parameter to _n-residue_ form. Note that the exponent is **not** converted to _n-residue_ form.

### 9.2.27  nres\_modadd

**Function:**  void **nres_modadd(x,y,z)**

big x,y,z;

**Module:**  mrmonty.c

**Description:**  Modular addition of two _n-residues_

**Parameters:**  Three _n-residue_ numbers _x_, _y_, and _z_.

On exit _z=x+y mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by a call to **prepare_monty.**

### 9.2.28  nres\_moddiv

**Function:**  int **nres\_moddiv**(x,y,z)

big x,y,z;

**Module:**  mrmonty.c

**Description:**  Modular division of two _n-residues_.

**Parameters:**  Three _n-residue_ numbers _x, y_ and _z_.

On exit _z =x/y mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  GCD of _y_ and _n_ as an integer, if possible, or **MR_TOOBIG**. Should be 1 for a valid result.

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of parameters to _n-residue_ form. Parameters _x_ and _y_ must be distinct.

### 9.2.29  nres\_modmult

**Function:**  void **nres\_modmult**(x,y,z)

big x,y,z;

**Module:**  mrmonty.c

**Description:**  Modular multiplication of two _n-residues_. Note that this routine will invoke a KCM Modular Multiplier if **MR_KCM** has been defined in _mirdef.h_ and set to an appropriate size for the current modulus, or a Comba fixed size modular multiplier if **MR_COMBA** is defined as exactly the size of the modulus.

**Parameters:**  Three _n-residue_ numbers _x_, _y_ and _z_

On exit _z =xy mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of parameters to _n-residue_ form.  

### 9.2.30  nres\_modsub

**Function:**  void **nres\_modsub(x,y,z)**

big x,y,z;

**Module:**  mrmonty.c

**Description:**  Modular subtraction of two _n-residues_

**Parameters:**  Three _n-residue_ numbers _x_, _y_, and _z_.

On exit _z=x-y mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by a call to **prepare_monty.**

### 9.2.31  nres\_multi\_inverse

**Function:**  BOOL **nres\_multi\_inverse**(m,x,w)

int m;
big \*x,\*w;

**Module:**  mrmonty.c

**Description:**  Finds the modular inverses of many numbers simultaneously, exploiting Montgomery's observation that _x_<sup>-1</sup> _= y.(xy)_<sup>-1</sup>_,  y_<sup>-1</sup> _= x.(xy)_<sup>-1</sup>. This will be quicker, as modular inverses are slow to calculate, and this way only one is required.

**Parameters:**  The number of inverses required _m_, an array _x_[.] of _m_ _n-residues_ whose inverses are wanted, and an array of their inverses _w_[.].

**Return value:**  TRUE if successful, otherwise FALSE.

**Restrictions:**  The parameters _x_ and _w_ must be distinct.

### 9.2.32  nres_negate

**Function:**  void **nres\_negate**(x,w)

big x,w;

**Module:**  mrmonty.c

**Description:**  Modular negation.

**Parameters:**  Two _n-residue_ numbers _x_ and _w_.

On exit _w= -x mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by a call to **prepare_monty.**

### 9.2.33  nres\_powltr

**Function:**  void **powltr**(x,e,w)

int x;
big e,w;

**Module:**  mrpower.c

**Description:**  Modular exponentiation of an _n-residue_

**Parameters:**  An ordinary small integer _x_, a big number _e_ and an _n-residue_ result _w_.

On exit _w=x<sup>e</sup> mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty**. Note that the small integer _x_ and the exponent are **not** converted to _n-residue_ form.

### 9.2.34  nres\_powmod

**Function:**  void **nres_powmod**(x,y,z)

big x,y,z;

**Module:**  mrpower.c

**Description:**  Modular exponentiation of an _n-residue_.

**Parameters:**  An _n-residue_ number _x_, a big number _y_ and an _n-residue_ result _z_. On exit _z =x<sup>y</sup> mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of the first parameter to _n-residue_ form. Note that the exponent is **not** converted to _n-residue_ form.

**Example:**

``` c
    prepare_monty(n);
    ...
    nres(x,y); /* convert to _n-residue_ form */
    nres_powmod(y,e,z);
    redc(z,w); /* convert back to normal form */
```

### 9.2.35  nres_powmod2

**Function:**  void **nres_powmod2**(x,y,a,b,w)

big x,y,a,b,w;

**Module:**  mrpower.c

**Description:**  Calculate the product of two modular exponentiations involving _n-residues_.

**Parameters:**  Three _n-residue_ numbers _x_, _a_ and _w_, and two big integers _y_ and _b_.

On exit _w = x<sup>y</sup> .a<sup>b</sup> mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of the appropriate parameters to _n-residue_ form. Note that the exponents are **not** converted to _n-residue_ form.

### 9.2.36  nres\_powmodn

**Function:**  void **nres\_powmodn**(m,x,y,w)

int m;
big ***x,***y,w;

**Module:**  mrpower.c

**Description:**  Calculate the product of _m_ modular exponentiations involving _n-residues_. Extra memory is allocated internally by this function.

**Parameters:**  The integer _m,_ an array of _m n-residue_ numbers _x_, an array of _m_ big integers _y_, and an _n-residue_ _w_.

On exit _w = x[0]<sup>y[0]</sup> . x[1]<sup>y[1]</sup> … . x[m-1]<sup>y[m-1]</sup> mod n_, where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of the appropriate parameters to _n-residue_ form. Note that the exponents are **not** converted to _n-residue_ form.

### 9.2.37  nres\_premult

**Function:**  void **nres\_premult**(x,k,w)

int k;
big x,w;

**Module:**  mrmonty.c

**Description:**  Multiplies an _n-residue_ by a small integer.

**Parameters:**  Two _n-residues_ _x_ and _w_, and a small integer _k_.

On exit _w = kx mod n,_ where _n_ is the currentMontgomery modulus.

**Return value:**  None

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of the first parameter to _n-residue_ form. Note that the small integer is **not** converted to _n-residue_ form.

### 9.2.38  nres\_sqroot

**Function:**  BOOL **nres_sqroot**(x,w)

big x,w;

**Module:**  mrsroot.c

**Description:**  Calculates the square root of an _n-residue_ mod a prime modulus

**Parameters:**  Two _n-residues_ _x_ and _w_.

On exit _w=__Öx mod n_ where _n_ is the currentMontgomery modulus.

**Return value:**  TRUE if the square root exists, otherwise FALSE

**Restrictions:**  Must be preceded by call to **prepare_monty** and conversion of the first parameter to _n-residue_ form.

### 9.2.39  nroot

**Function:**  BOOL **nroot**(x,n,z)

big x,z;
int n;

**Module:**  mrarth3.c

**Description:**  Extracts lower approximation to a root of a big number.

**Parameters:**  Two big numbers _x_ and _z_, and an integer _n_.

On exit _z=_ ë_x<sup>1/n</sup>_ û.

**Return value:**  Returns the boolean value TRUE if the root found is exact, otherwise returns FALSE.

**Restrictions:**  The value of _n_ must be positive. If _x_ is negative, then _n_ must be odd.

### 9.2.40  nxprime

**Function:**  BOOL **nxprime**(w,x)

big w,x;

**Module:**  mrprime.c

**Description:**  Find next prime number.

**Parameters:**  Two big numbers _w_ and _x_.

On exit _x_ contains the next prime number greater than _w_.

**Return value:**  TRUE if successful, FALSE otherwise.

**Restrictions:**  None

### 9.2.41  nxsafeprime

**Function:**  BOOL n**xsafeprime**(type,subset,w,p)

int type,subset;
big w,p;

**Module:**  mrprime.c

**Description:**  Find next _safe_ prime number greater than _w_. A _safe_ prime number _p_ is defined here to be one for which _q=_(_p_-1)/2 (_type_=0) or _q=_(_p_+1)/2 (_type=_1_)_ is also prime.

**Parameters:**  The integer parameter _type_ determines the type of safe prime as above. If the parameter _subset_=1, then the search is restricted so that the value of the prime _q_ is congruent to 1 mod 4\. If _subset=_3, then the search is restricted so that the value of _q_ is congruent to 3 mod 4\. If _subset_=0 then there is no condition on _q_: it can be either 1 or 3 mod 4.

**Return value:**  TRUE if successful, FALSE otherwise

### 9.2.42  pow\_brick

**Function:**  void **pow\_brick**(binst,e,w)

brick *binst;
big e,w;

**Module:**  mrbrick.c

**Description:**  Carries out a modular exponentiation, using the precomputed values stored in the _brick_ structure.

**Parameters:**  A pointer to the current instance, a big exponent _e_ and a big number _w_. On exit _w=g<sup>e</sup> mod n_, where _g_ and _n_ are specified in the initial call to **brick_init.**

**Return value:**  None

**Restrictions:**  Must be preceded by a call to **brick_init**.

### 9.2.43  power

**Function:**  void **power**(x,n,z,w)

long n;
big x,z,w;

**Module:**  mrarth3.c

**Description:**  Raise a big number to an integer power.

**Parameters:**  Two big numbers _x_ and _z_, and an integer _n_. On exit _w=x<sup>n</sup>_ . If _w_ and _z_ are distinct, then _w=x<sup>n</sup>  mod z_

**Return value:**  None

**Restrictions:**  The value of _n_ must be positive

### 9.2.44  powltr

**Function:**  int **powltr**(x,y,z,w)

int x;
big y,z,w;

**Module:**  mrpower.c

**Description:**  Raise an _int_ to the power of a big number modulus another big number. Uses Left-to-Right binary method, and will be somewhat faster than **powmod** for small _x_. Uses Montgomery arithmetic internally if the modulus _z_ is odd.

**Parameters:**  An integer _x_ and three bigs _y_, _z_ and _w_.

On exit _w=x<sup>y</sup> mod z_

**Return value:**  The result expressed as an integer, if possible. Otherwise the value **MR_TOOBIG**.

**Restrictions:**  The value of _y_ must be positive. The parameters _w_ and _z_ must be distinct.

### 9.2.45  powmod

**Function:**  void **powmod**(x,y,z,w)

big x,y,z,w;

**Module:**  mrpower.c

**Description:**  Raise a big number to a big power modulus another big. Uses a sophisticated 5-bit sliding window technique, which is close to optimal for popular modulus sizes (such as 512 or 1024 bits). Uses Montgomery arithmetic internally if the modulus _z_ is odd.

This function can be speeded up further for particular moduli, by invoking special assembly language routines (if your compiler allows it). A KCM Modular Multiplier will be automatically invoked if **MR_KCM** has been defined in _mirdef.h_ and has been set to an appropriate size. Alternatively a Comba modular multiplier will be used if **MR_COMBA** is so defined, and the modulus is of the specified size. Experimental coprocessor code will be called if **MR_PENTIUM** is defined. Only one of these conditionals should be defined.

**Parameters:**  Four big numbers _x, y, z_ and _w_.

On exit _w=x<sup>y</sup> mod z_.

**Return value:**  None

**Restrictions:**  The value of _y_ must be positive. The parameters _w_ and _z_ must be distinct.

### 9.2.46  powmod2

**Function:**  void **powmod2**(a,b,c,d,z,w)

big a,b,c,d,z,w;

**Module:**  mrpower.c

**Description:**  Calculate the product of two modular exponentiations. This is quicker than doing two separate exponentiations, and is useful for certain Cryptographic protocols. Uses 2-bit sliding window.

**Parameters:**  Six big numbers _a ,b, c, d, z_ and _w_.

On exit _w=a<sup>b</sup>.c<sup>d</sup> mod z_.

**Return value:**  None

**Restrictions:**  The values of _b_ and _d_ must be positive. The parameters _w_ and _z_ must be distinct. The modulus _z_ must be odd.

**Example:**

> See _dssver.c_

### 9.2.47  powmodn

**Function:**  void **powmodn**(m,a,b,z,w)

int m;
big ***a,***b,z,w;

**Module:**  mrpower.c

**Description:**  Calculate the product of _m_ modular exponentiations. This is quicker than doing _m_ separate exponentiations, and is useful for certain Cryptographic protocols. Extra memory is allocated internally for this function

**Parameters:**  An integer _m_, two big number arrays _a[]_ and _b[]_, and two big numbers _ z_ and _w_. On exit _w=a[0]<sup>b[0]</sup>.a[1]<sup>b[1]</sup> …  . a[m-1]<sup>b[m-1]</sup> mod z_.

**Return value:**  None

**Restrictions:**  The values of _b[]_ must be positive. The parameters _w_ and _z_ must be distinct. The modulus _z_ must be odd. The underlying number base must be a power of 2.

### 9.2.48  prepare_monty

**Function:**  void **_prepare_monty_**(n)

big n;

**Module:**  mrmonty.c

**Description:**  Prepares a Montgomery Modulus for use. Each call to this function replaces the previous modulus (if any).

**Parameters:**  A big number _n_, which is to be theMontgomery modulus.

**Return value:**  None

**Restrictions:**  The parameter _n_ must be positive and odd. Allocated memory is freed when the current instance of MIRACL is terminated by a call to **mirexit**.

### 9.2.49  redc

**Function:**  void **redc**(x,y)

big x,y;

**Module:**  mrmonty.c

**Description:**  Converts an _n-residue_ back to normal form.

**Parameters:**  Two big numbers _x_ and _y_.

On exit _y_ is the normal form of the _n-residue_ _x_.

**Return value:**  None

**Restrictions:**  Use must be preceded by call to **prepare_monty**.

### 9.2.50  scrt

**Function:**  void **scrt**(psc,rem,x)

small_chinese *psc;
int \*rem;
big x;

**Module**:  mrscrt.c

**Description:**  Applies Chinese Remainder Theorem (for small prime moduli).

**Parameters:**  A pointer _psc_ to the current instance of the Chinese Remainder Theorem. On exit _x_ contains the big number which yields the given integer remainders _rem[.]_ when it is divided by the integer moduli specified in a prior call to **scrt_init**.

**Return value:**  None

**Restrictions:**  The routine **scrt_init** must be called first.

### 9.2.51  scrt\_end

**Function:**  void **scrt_end**(psc)

small_chinese *psc;

**Module:**  mrscrt.c

**Description:**  Cleans up after an application of the Chinese Remainder Theorem.

**Parameters:**  A pointer to the current instance of the Chinese Remainder Theorem..

**Return value:**  None

**Restrictions:**  None

### 9.2.52  scrt\_initcopy

**Function:**  BOOL **scrt\_init**(psc,np,m)

small_chinese *psc;
int np;
int *m;

**Module:**  mrscrt.c

**Description:**  Initialises an instance of the Chinese Remainder Theorem. Some internal workspace is allocated.

**Parameters:**  A pointer to the current instance _psc_. The number of co-prime moduli _np_, and an array of at least two integer moduli _m[.]._

**Return value:**  TRUE if all went well, FALSE if there was a problem.

**Restrictions:**  None

### 9.2.53  sftbit

**Function:**  void **sftbit**(x,n,z)

big x,z;
int n;

**Module:**  mrbits.c

**Description:**  Shifts a big integer left or right by a number of bits.

**Parameters:**  The big parameter _x_ is shifted by _n_ bits, to give _z_. Positive _n_ shifts to the left, negative to the right.

**Return value:**  None

**Restrictions:**  None

### 9.2.54  smul

**Function:**  unsigned int **smul**(x,y,z)

Unsigned int x,y,z;

**Module:**  mrsmall.c

**Description:**  Multiplies two integers mod a third

**Parameters:**  Integers _x, y_ and _z_

**Return value:**  _x.y mod z_

### 9.2.55  spmd

**Function:**  unsigned int **spmd**(x,y,z)

Unsigned int x,y,z;

**Module:**  mrsmall.c

**Description:**  Raises an integer to an integer power modulus a third

**Parameters:**  Integers _x, y_, and _z_

**Return value:**  _x<sup>y</sup> mod z_

**Restrictions:**  None

### 9.2.56  sqrmp

**Function:**  unsigned int **sqrmp**(x,p)

Unsigned int x,p;

**Module:**  mrsmall.c

**Description:**  Calculates the square root of an integer mod an integer prime number

**Parameters:**  An integer _x_ and a prime number _p_

**Return value:** _Öx mod p_, or 0 if root does not exist

**Restrictions:**  Return value unpredictable if _p_ is not prime  

### 9.2.57  sqroot

**Function:**  BOOL **sqroot**(x,p,w)

big x,p;

**Module:**  mrsroot.c

**Description:**  Calculates the square root of a big integer mod a big integer prime.

**Parameters:**  Two big integers _x_ and _w_, and a big prime number _p_.

On exit _w=_Öx mod p_ if the square root exists, otherwise _w=0_. Note that the "other" square root may be found by subtracting _w_ from _p_.

**Return value:**  TRUE if the square root exists, FALSE otherwise.

**Restrictions:**  The number _p_ must be prime.

### 9.2.58  trial\_division

**Function:**  int **trial\_division**(x,y)

big x,y;

**Module:**  mrprime.c

**Description:**  Dual purpose trial division routine. If _x_ and _y_ are the same big variable then trial division by the small prime numbers in the instance array **PRIMES** is attempted to determine the primality status of the big number. If _x_ and _y_ are distinct then, after trial division, the unfactored part of _x_ is returned in _y_.

**Parameters:**  Two big integers _x_ and _y_.

**Return value:**  If _x_ and _y_ are the same, then a return value of 0 means that the big number is definitely not prime, a return value of 1 means that it definitely is prime, while a return value of 2 means that it is possibly prime (and that perhaps further testing should be carried out).

If _x_ and _y_ are distinct, then a return value of 1 means that _x_ is _smooth_, that is it is completely factored by trial division (and _y_ is the largest prime factor). A return value of 2 means that the unfactored part _y_ is possibly prime.   

### 9.2.59  xgcd

**Function:**  int **xgcd**(x,y,xd,yd,z)

big x,y,xd,yd,z;

**Module:**  mrxgcd.c

**Description:**  Calculates extended Greatest Common Divisor of two big numbers. Can be used to calculate modular inverses. Note that this routine is much slower than a **mad** operation on numbers of similar size.

**Parameters:**  Five big numbers _x,y,xd,yd_ and _z_.

On exit _z=gcd(x,y)=x.xd+y.yd_

**Return value:**  GCD as integer, if possible, otherwise **MR_TOOBIG**

**Restrictions:**  If _xd_ and _yd_ are not distinct, only _xd_ is returned. The GCD is only returned if _z_ distinct from both _xd_ and _yd_.

**Example:**

``` c
	xgcd(x,p,x,x,x);  /* _x = 1/x mod_ _p_  (_p_ is prime) */
```

### 9.2.60  zzn2\_add

**Function:**  void **zzn2\_add**(x,y,z)

zzn2 \*x,\*y,\*z;

**Module:**  mrzzn2.c

**Description:**   Adds two zzn2 variables.

**Parameters:**  Three zzn2 variables _x_, _y_ and _z_. On exit _z=x+y_

**Return value:**   None

### 9.2.61  zzn2\_compare

**Function:**  BOOL **zzn2\_compare**(x,y)

zzn2 \*x,\*y;

**Module:**  mrzzn2.c

**Description:**   Compares two zzn2 variables for equality

**arameters:**  Two zzn2 values _x_ and _y_

**Return value:**   TRUE if _x=y_, otherwise FALSE

### 9.2.62  zzn2\_conj

**Function:**  void **zzn2\_conj**(x,y)

zzn2 \*x,\*y;

**Module:**  mrzzn2.c

**Description:**   Finds the conjugate of a zzn2

**Parameters:**  Two zzn2 variables _x_ and _y_. If _x=a+ib_, then on exit _y=a-ib_

**Return value:**   None

### 9.2.63  zzn2\_copy

**Function:**   void **zzn2\_copy**(x,y)

zzn2 \*x,\*y;

**Module:**  mrzzn2.c

**Description:**  Copies one zzn2 to another

**Parameters:**  Two zzn2 variables _x_ and _y_. On exit _y=x_

**Return value:**   None

### 9.2.64  zzn2\_from\_big

**Function:**  void **zzn2\_from\_big**(a,x)

big a;
zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Creates a zzn2 from a big integer. This is converted internally into _n-residue_ format.

**Parameters:**   A big integer _a_ and a zzn2 _x_. On exit _x=a_

**Return value:**  None

### 9.2.65  zzn2\_from\_bigs

**Function:**  void **zzn2\_from\_bigs**(a,b,x)

big a,b;
zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Creates a zzn2 from two big integers. These are converted internally into _n-residue_ format.

**Parameters:**   Two big integers _a_ and _b_ and a zzn2 _x_. On exit _x=a+ib_

**Return value:**  None  

### 9.2.66  zzn2\_from\_int

Function:  void **zzn2\_from\_int**(a,x)

int a;
zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Converts an integer to zzn2 format

**Parameters:**  An integer _a_ and a zzn2 _x_. On exit _x=a_

**Return value:**   None

### 9.2.67  zzn2\_from\_ints

**Function:**  void **zzn2\_from\_ints**(a,b,x)

int a,b;
zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Creates a zzn2 from two integers

**Parameters:**   Two integers _a_ and _b_ and a zzn2 _x_. On exit _x=a+ib_

**Return value:**  None

### 9.2.68  zzn2\_from\_zzn

**Function:**  void **zzn2\_from\_zzn**(a,x)

big a;
zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Creates a zzn2 from a big already in _n-residue_ format.

**Parameters:**   A big _a_ and a zzn2 _x_. On exit _x=a_

**Return value:**  None  

### 9.2.69  zzn2\_from\_zzns

**Function:**  void **zzn2\_from\_zzns**(a,b,x)

big a,b;
zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Creates a zzn2 from two bigs already in _n-residue_ format.

**Parameters:**   Two bigs _a_ and _b_ and a zzn2 _x_. On exit _x=a+ib_

**Return value:**  None

### 9.2.70  zzn2\_imul

**Function:**  void **zzn2\_simul**(x,y,z)

zzn2 *x,*z;
int y;

**Module:**  mrzzn2.c

**Description:**   Multiplies a zzn2 variable by an integer.

**Parameters:**  Two zzn2 variables _x_ and _z_, and an integer _y_. On exit _z=x.y_

**Return value:**   None

### 9.2.71  zzn2\_inv

**Function:**  BOOL **zzn2_inv**(x)

zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  In-place inversion of a zzn2 variable

**Parameters:**  A single zzn2 variable _x_. On exit _x=1/x_.

**Return value:**  None

### 9.2.72  zzn2\_isunity

**Function:**  BOOL **zzn2\_isunity**(x)

zzn2 *x;

**Module:**  mrzzn2.c

**Description:**  Tests a zzn2 value for equality to one

**Parameters:**  A single zzn2 variable _x_

**Return value:**  TRUE if _x_ is one, otherwise FALSE.

### 9.2.73  zzn2\_iszero

**Function:**  BOOL **zzn2_iszero**(x)

zzn2 \*x;

**Module:**  mrzzn2.c

**Description:**  Tests a zzn2 variable for equality to zero

**Parameters:**  A single zzn2 value _x_

**Return value:**  TRUE if _x_ is zero, otherwise FALSE.

### 9.2.74  zzn2\_mul

**Function:**  void **zzn2\_mul**(x,y,z)

zzn2 \*x,\*y,*z;

**Module:**  mrzzn2.c

**Description:**   Multiplies two zzn2 variables. If _x_ and _y_ are the same variable, a faster squaring method is used.

**Parameters:**  Three zzn2 variables _x, y_ and _z_. On exit _z=x.y_

**Return value:**   None

### 9.2.75  zzn2\_negate

**Function:**  void **zzn2\_negate**(x,y)

zzn2 \*x,\*y;

**Module:**  mrzzn2.c

**Description:**  Negate a zzn2.

**Parameters:**  Two zzn2 variables _x_ and _y_. On exit _y=-x_

**Return value:**  None

### 9.2.76  zzn2\_sadd

**Function:**  void **zzn2\_sadd**(x,y,z)

zzn2 *x,*z;
big y;

**Module:**  mrzzn2.c

**Description:**   Adds a big in _n-residue_ format to a zzn2 .

**Parameters:**  Two zzn2 variables _x_ and _z_, and a big variable _y_. On exit _z=x+y_

**Return value:**   None

### 9.2.77  zzn2\_smul

**Function:**  void **zzn2\_smul**(x,y,z)

zzn2 *x,*z;
big y;

**Module:**  mrzzn2.c

**Description:**   Multiplies a zzn2 variable by a big in _n-residue_.

**Parameters:**  Two zzn2 variables _x_ and _z_, and a big variable _y_. On exit _z=x.y_

**Return value:**   None

### 9.2.78  zzn2\_ssub

**Function:**  void **zzn2_ssub**(x,y,z)

zzn2 *x,*z;
big y;

**Module:**  mrzzn2.c

**Description:**   Subtracts a big in _n-residue_ format from a zzn2 .

**Parameters:**  Two zzn2 variables _x_ and _z_, and a big variable _y_. On exit _z=x-y_

**Return value:**   None

### 9.2.79  zzn2\_sub

**Function:**  void **zzn2\_sub**(x,y,z)

zzn2 \*x,\*y,\*z;

**Module:**  mrzzn2.c

**Description:**   Subtracts two zzn2 variables .

**Parameters:**  Three zzn2 variables _x, y_ and _z_. On exit _z=x-y_

**Return value:**   None

### 9.2.80  zzn2\_timesi

**Function:**  BOOL **zzn2_timesi**(x)

zzn2 \*x;

**Module:**  mrzzn2.c

**Description:** In-place multiplication of a zzn2 by _i,_ the imaginary square root of the quadratic non-residue.

**Parameters:**  A single zzn2 variable _x_. If _x=a+ib_ then on exit _x=i__<sup>2</sup>b+ia_.

**Return value:**  None

### 9.2.81  zzn2\_zero

**Function:**  void **zzn2_iszero**(x)

zzn2 \*x;

**Module:**  mrzzn2.c

**Description:**  Sets a zzn2 variable to zero

**Parameters:**  A single zzn2 variable _x_. On exit _x=0_

**Return value:**  None

## 9.3 Elliptic curve routines

### 9.3.1  ebrick\_init

**Function:**  BOOL **ebrick\_init**(binst,x,y,a,b,n,w,nb)

ebrick \*binst;
big x,y;
big a,b,n;
int w,nb;

**Module:**  mrebrick.c

**Description:**  Initialises an instance of the Comb method for GF(_p_) elliptic curve multiplication with precomputation. Internally memory is allocated for 2_<sup>w</sup>_ elliptic curve points which will be precomputed and stored. For bigger _w_ more space is required, but the exponentiation is quicker. Try _w_=8.

**Parameters:**  A pointer to the current instance _binst_, the fixed point _G=_(_x,y_) on the curve  _y<sup>2</sup> =x<sup>3</sup> + ax + b_, the modulus _n_, and the maximum number of bits to be used in the exponent _nb_.

**Return value:**  TRUE if all went well, FALSE if there was a problem.

**Restrictions:**  Note: If MR_STATIC is defined in _mirdef.h_, then the _x_ and _y_ parameters in this function are replaced by a single mr_small * pointer to a precomputed table. In this case the function returns a void.

### 9.3.2  ebrick2\_init

**Function:**  BOOL **ebrick2\_init**(binst,x,y,A,B,m,a,b,c,nb)

ebrick2 *binst;
big x,y;
big A,B;
int m,a,b,c,nb;

**Module:**  mrec2m.c

**Description:**  Initialises an instance of the Comb method for GF(2_<sup>m</sup>_) elliptic curve multiplication with precomputation. The field is defined with respect to the trinomial basis _t<sup>m</sup>+t<sup>a</sup>+1_ or the pentanomial basis _t<sup>m</sup>+t<sup>a</sup>+t<sup>b</sup>+t<sup>c</sup>+1_. Internally memory is allocated for 2_<sup>w</sup>_ elliptic curve points which will be precomputed and stored. For bigger _w_ more space is required, but the exponentiation is quicker. Try _w_=8.

**Parameters:**  A pointer to the current instance _binst_, the fixed point _G=_(_x,y_) on the curve  _y<sup>2</sup> + xy = x<sup>3</sup> + Ax<sup>2</sup> + B_, the field parameters _m, a, b, c_, and the maximum number of bits to be used in the exponent _nb_. Set _b_ = 0 for a trinomial basis.

**Return value:**  TRUE if all went well, FALSE if there was a problem.

**Restrictions:**  Note: If MR_STATIC is defined in _mirdef.h_, then the _x_ and _y_ parameters in this function are replaced by a single mr_small * pointer to a precomputed table. In this case the function returns a void.

### 9.3.3  ebrick\_end

**Function:**  void **ebrick\_end**(binst)

ebrick \*binst

**Module:**  mrebrick.c

**Description:**  Cleans up after an application of the Comb for GF(_p_) elliptic curves

**Parameters:**  A pointer to the current instance

**Return value:**  None

**Restrictions:**  None

### 9.3.4  ebrick2\_end

**Function:**  void **ebrick2\_end**(binst)

ebrick2 \*binst

**Module:**  mrec2m.c

**Description:**  Cleans up after an application of the Comb method for GF(2_<sup>m</sup>_) elliptic curves.

**Parameters:**  A pointer to the current instance

**Return value:**  None

**Restrictions:**  None

### 9.3.5  ecurve\_add

**Function:**  void **ecurve\_add**(p,pa)

epoint \*p,\*pa;

**Module:**  mrcurve.c

**Description:**  Adds two points on a GF(_p)_ elliptic curve using the special rule for addition. Note that if _pa=p_, then a different duplication rule is used. Addition is quicker if _p_ is normalised.

**Parameters:**  Two points on the current active curve_, pa_ and _p_. On exit _pa=pa+p._

**Return value:**  None

**Restrictions:**  The input points must actually be on the current active curve.  

### 9.3.6  ecurve2\_add

**Function:**  void **ecurve2\_add**(p,pa)

epoint *p,*pa;

**Module:**  mrec2m.c

**Description:**  Adds two points on a GF(2_<sup>m</sup>_) elliptic curve using the special rule for addition. Note that if _pa=p_, then a different duplication rule is used. Addition is quicker if _p_ is normalised.

**Parameters:**  Two points on the current active curve_, pa_ and _p_. On exit _pa=pa+p._

**Return value:**  None

**Restrictions:**  The input points must actually be on the current active curve.

### 9.3.7  ecurve\_init

**Function:**  void **ecurve\_init**(A,B,p,type)

big A,B,p;
int type;

**Module:**  mrcurve.c

**Description:**  Initialises the internal parameters of the current active GF(_p_) elliptic curve. The curve is assumed to be of the form  _y<sup>2</sup> =x<sup>3</sup> + Ax + B mod p_, the so-called Weierstrass model. This routine can be called subsequently with the parameters of a different curve.

**Parameters:**  Three big numbers _A_, _B_ and _p_. The _type_ parameter must be either **MR_PROJECTIVE** or ** MR_AFFINE**, and specifies whether projective or affine co-ordinates should be used internally. Normally the former is faster.

**Return value:**  None

**Restrictions:**  Allocated memory will be freed when the current instance of MIRACL is terminated by a call to **mirexit**. However only one elliptic curve, GF(_p_) or GF(2_<sup>m</sup>_) may be active within a single MIRACL instance. In addition, a call to a function like **powmod** will overwrite the stored modulus. This can be restored by a repeat call to **ecurve_init**

### 9.3.8  ecurve2\_init

Function:  BOOL **ecurve2\_init**(m,a,b,c,A,B,check,type)

big A,B;
int m,a,b,c,type;
BOOL check;

**Module:**  mrec2m.c

**Description:**  Initialises the internal parameters of the current active elliptic curve. The curve is assumed to be of the form  _y<sup>2</sup> + xy =x<sup>3</sup> + Ax<sup>2</sup> + B_ . The field is defined with respect to the trinomial basis _t<sup>m</sup>+t<sup>a</sup>+1_ or the pentanomial basis _t<sup>m</sup>+t<sup>a</sup>+t<sup>b</sup>+t<sup>c</sup>+1_. This routine can be called subsequently with the parameters of a different curve.

**Parameters:**  The fixed point _G=_(_x,y_) on the curve  _y<sup>2</sup> + xy = x<sup>3</sup> + Ax<sup>2</sup> + B_, the field parameters _m, a, b, c._ Set _b_ = 0 for a trinomial basis. The _type_ parameter must be either **MR_PROJECTIVE** or ** MR_AFFINE**, and specifies whether projective or affine co-ordinates should be used internally. Normally the former is faster. If _check_ is TRUE a check is made that the specified basis is irreducible. If FALSE, this basis validity check, which is time-consuming, is suppressed.

**Return value:**  TRUE if parameters make sense, otherwise FALSE.

**Restrictions:** Allocated memory will be freed when the current instance of MIRACL is terminated by a call to **mirexit**. However only one elliptic curve, GF(_p_) or GF(2_<sup>m</sup>_) may be active within a single MIRACL instance.

### 9.3.9  ecurve\_mult

**Function:**  void **ecurve\_mult**(k,p,pa)

big k;
epoint \*p,\*pa;

**Module:**  mrcurve.c

**Description:**  Multiplies a point on a GP(_p_) elliptic curve by an integer. Uses the addition/subtraction method.

**Parameters:**  A big number _k_, and two points  _p_ and _pa_. On exit _pa=k*p._

**Return value:**  None

**Restrictions:**  The point _p_ must be on the active curve.  

### 9.3.10  ecurve2\_mult

**Function:**  void **ecurve2\_mult**(k,p,pa)

big k;
epoint \*p,\*pa;

**Module:**  mrec2m.c

**Description:**  Multiplies a point on a GF(2_<sup>m</sup>_)  elliptic curve by an integer. Uses the addition/subtraction method.

**Parameters:**  A big number _k_, and two points  _p_ and _pa_. On exit _pa=k*p._

**Return value:**  None

**Restrictions:**  The point _p_ must be on the active curve.

### 9.3.11  ecurve\_mult2

**Function:**  void **ecurve\_mult2**(k1,p1,k2,p2,pa)

big k1,k2;
epoint \*p1,\*p2,\*pa;

**Module:**  mrcurve.c

**Description:**  Calculates the point _k1.p1+k2.p2_ on a GF(_p_) elliptic curve. This is quicker than doing two separate multiplications and an addition. Useful for certain cryptosystems. (See _ecsver.c_ for example)

**Parameters:**  Two big integers _k1_ and _k2_, and three points _p1, p2_ and _pa_.

On exit _pa = k1.p1+k2.p2_

**Return value:**  None

**Restrictions:**  The points _p1_ and _p2_ must be on the active curve.

### 9.3.12  ecurve2\_mult2

**Function:**  void **ecurve2\_mult2**(k1,p1,k2,p2,pa)

big k1,k2;
epoint \*p1,\*p2,\*pa;

**Module:**  mrec2m.c

**Description:**  Calculates the point _k1.p1+k2.p2_ on a GF(2_<sup>m</sup>_) elliptic curve. This is quicker than doing two separate multiplications and an addition. Useful for certain cryptosystems. (See _ecsver2.c_ for example)

**Parameters:**  Two big integers _k1_ and _k2_, and three points _p1, p2_ and _pa_.

On exit _pa = k1.p1+k2.p2_

**Return value:**  None

**Restrictions:**  The points _p1_ and _p2_ must be on the active curve.

### 9.3.13 ecurve\_multi\_add

**Function:**  void **ecurve\_multi\_add**(m,x,w)

int m;
epoint \*x,\*w;

**Module:**  mrcurve.c

**Description:**  Simultaneously adds pairs of points on the active GF(_p_) curve. This is much quicker than adding them individually, but *only* when using Affine co-ordinates.

**Parameters:**  An integer _m_ and two arrays of points _w_ and _x_. On exit _w[i]=w[i]+x[i]_ for _i_ =0 to _m_-1

**Return value:**  None

**Restrictions:**  Only useful when using Affine co-ordinates.

**See also:**  **ecurve_init** and **nres_multi_inverse**, which is used internally.

### 9.3.14  ecurve2\_multi\_add

**Function:**  void **ecurve2\_multi\_add**(m,x,w)

int m;
epoint \*x,\*w;

**Module:**  mrec2m.c

**Description:**  Simultaneously adds pairs of points on the active GF(2_<sup>m</sup>_) curve. This is much quicker than adding them individually, but only when using Affine co-ordinates.

**Parameters:**  An integer _m_ and two arrays of points _w_ and _x_. On exit _w[i]=w[i]+x[i]_ for _i_ =0 to _m_-1

**Return value:**  None

**Restrictions:**  Only useful when using Affine co-ordinates.

> See also:  **ecurve2_init**

### 9.3.15  ecurve\_multn

**Function:**  void **ecurve\_multn**(n,k,p,pa)

int n;
big \*k;
epoint \*\*p;

**Module:**  mrcurve.c

**Description:**  Calculates the point _k[0].p[0] + k[1].p[1] + … + k[n-1].p[n-1]_ on a GF(_p_) elliptic curve, for _n>2_.

**Parameters:**  An integer _n_, an array of _n_ big numbers _k[]_, and an array of _n_ points. The result is returned in _pa_.

**Return value:**  None

**Restrictions:**  The points must be on the active curve. The _k[]_ values must all be positive. The underlying number base must be a power of 2.

### 9.3.16  ecurve2\_multn

**Function:**  void **ecurve2\_multn**(n,k,p,pa)

int n;
big \*k;
epoint \*\*p;

**Module:**  mrec2m.c

**Description:**  Calculates the point _k[0].p[0] + k[1].p[1] + … + k[n-1].p[n-1]_ on a GF(2_<sup>m</sup>_) elliptic curve, for _n>2_.

**Parameters:**  An integer _n_, an array of _n_ big numbers _k[]_, and an array of _n_ points. The result is returned in _pa_.

**Return value:**  None

**Restrictions:**  The points must be on the active curve. The _k[]_ values must all be positive. The underlying number base must be a power of 2.

### 9.3.17  ecurve\_sub

**Function:**  void **ecurve_sub**(p,pa)

epoint \*p,\*pa;

**Module:**  mrcurve.c

**Description:**  Subtracts two points on a GF(_p_) elliptic curve. Actually negates _p_ and adds it to _pa_. Subtraction is quicker if _p_ is normalised.

**Parameters:**  Two points on the current active curve_, pa_ and _p_. On exit _pa = pa-p._

**Return value:**  None

**Restrictions:**  The input points must actually be on the current active curve.

### 9.3.18  ecurve2\_sub

**Function:**  void **ecurve2\_sub**(p,pa)

epoint \*p,\*pa;

**Module:**  mrec2m.c

**Description:**  Subtracts two points on a GF(2_<sup>m</sup>_) elliptic curve. Actually negates _p_ and adds it to _pa_. Subtraction is quicker if _p_ is normalised.

**Parameters:**  Two points on the current active curve_, pa_ and _p_. On exit _pa = pa-p._

**Return value:**  None

**Restrictions:**  The input points must actually be on the current active curve.

### 9.3.19  epoint\_comp

**Function:**  BOOL **epoint\_comp**(p1,p2)

epoint \*p1,\*p2;

**Module:**  mrcurve.c

**Description:**  Compares two points on the current active GF(_p_) elliptic curve.

**Parameters:**  Two points _p1_ and _p2_.

**Return Value:**  TRUE if the points are the same, otherwise FALSE.

**Restrictions:**  None

### 9.3.20  epoint2\_comp

**Function:**  BOOL **epoint2\_comp**(p1,p2)

epoint \*p1,\*p2;

**Module:**  mrec2m.c

**Description:**  Compares two points on the current active GF(2_<sup>m</sup>_) elliptic curve.

**Parameters:**  Two points _p1_ and _p2_.

**Return Value:**  TRUE if the points are the same, otherwise FALSE.

**Restrictions:**  None

### 9.3.21  epoint\_copy

**Function:**  void **epoint\_copy**(p1,p2)

epoint \*p1,\*p2;

**Module:**  mrcurve.c

**Description:**  Copies one point to another on a GF(_p_) elliptic curve.

**Parameters:**  Two points _p1_ and _p2_. On exit _p2=p1_.

**Return value:**  None

**Restrictions:**  None

### 9.3.22  epoint2\_copy

**Function:**  void **epoint2\_copy**(p1,p2)

epoint \*p1,\*p2;

**Module:**  mrec2m.c

**Description:**  Copies one point to another on a GF(2_<sup>m</sup>_) elliptic curve.

**Parameters:**  Two points _p1_ and _p2_. On exit _p2=p1_.

**Return value:**  None

**Restrictions:**  None

### 9.3.23  epoint\_free

**Function:**  void **epoint_free**(p)

epoint \*p;

**Module:**  mrcore.c

**Description:**  Frees memory associated with a point on a GF(_p_) elliptic curve.

**Parameters:**  A point _p_.

**Return value:**  None

**Restrictions:**  None

### 9.3.24  epoint\_get

**Function:**  int **epoint\_get**(p,x,y)

epoint \*p;
big x,y;

**Module:**  mrcurve.c

**Description:**  Normalises a point and extracts its _(x,y)_ co-ordinates on the active GF(_p_) elliptic curve.

**Parameters:**  A point _p_, and two big integers _x_ and _y_. If _x_ and _y_ are not distinct variables on entry then only the value of _x_ is returned.

**Return value:**  The least significant bit of _y_. Note that it is possible to reconstruct a point from its _x_ co-ordinate and just the least significant bit of _y_. Often such a "compressed" description of a point is useful.

**Restrictions:**  The point _p_ must be on the active curve.

**Example:**

``` c
/* extract x co-ordinate and lsb of y */
i=epoint_get(p,x,x);
```

### 9.3.25  epoint\_getxyz

**Function:**   void **epoint_getxyz**(p,x,y,z)

epoint \*p;
big x,y,z;

**Module:**  mrcurve.c

**Description:**  Extracts the raw (_x,y,z_) co-ordinates of a point on the active GF(_p_) elliptic curve.

**Parameters:**  A point _p_, and three big integers _x, y_ and _z_. If any of these is NULL that coordinate is not returned.

**Return value:**  None

**Restrictions:**   The point _p_ must be on the active curve.

### 9.3.26  epoint2\_get

**Function:**  int **epoint2\_get**(p,x,y)

epoint \*p;
big x,y;

**Module:**  mrec2m.c

**Description:**  Normalises a point and extracts its _(x,y)_ co-ordinates on the active GF(2_<sup>m</sup>_) elliptic curve.

**Parameters:**  A point _p_, and two big integers _x_ and _y_. If _x_ and _y_ are not distinct variables on entry then only the value of _x_ is returned.

**Return value:**  The least significant bit of _y/x_. Note that it is possible to reconstruct a point from its _x_ co-ordinate and just the least significant bit of _y/x_. Often such a "compressed" description of a point is useful.

**Restrictions:**  The point _p_ must be on the active curve.

**Example:**

``` c
    /* extract x co-ordinate and lsb of y/x */  
    i=epoint_get(p,x,x);
```

### 9.3.27  epoint2\_getxyz

**Function:**   void **epoint2\_getxyz**(p,x,y,z)

epoint \*p;
big x,y,z;

**Module:**  mrcurve.c

**Description:**  Extracts the raw (_x,y,z_) co-ordinates of a point on the active GF(2_<sup>m</sup>_) elliptic curve.

**Parameters:**  A point _p_, and three big integers _x, y_ and _z_. If any of these is NULL that coordinate is not returned.

**Return value:**  None

**Restrictions:**   The point _p_ must be on the active curve.

### 9.3.28  epoint\_init

**Function:**  epoint\* **epoint_init**()

**Module:**  mrcore.c

**Description:**  Assigns memory to a point on a GF(_p_) elliptic curve, and initialises it to the "point at infinity".

**Parameters:**  None.

**Return value:**  A point _p_ (in fact a pointer to a structure allocated from the heap).

**Restrictions:**  It is the C programmers responsibility to ensure that all elliptic curve points initialised by a call to this function, are ultimately freed by a call to **epoint_free**. If not a memory leak will result.

### 9.3.29  epoint\_init\_mem

**Function:**  epoint\* **epoint\_init\_mem**(mem,index)

char \*mem;
int index;

**Module:**  mrcore.c

**Description:**  Initialises memory for an elliptic curve point from a pre-allocated byte array _mem_. This array may be created from the heap by a call to **ecp_memalloc**, or in some other way. This is quicker than multiple calls to **epoint_init**

**Parameters:**  A pointer to the pre-allocated array _mem_, and an index into that array. Each index should be unique.

**eturn value:**  An initialised elliptic curve point.

**Restrictions:**  Sufficient memory must have been allocated and pointed to by _mem_.

### 9.3.30  epoint\_norm

**Function:**  BOOL **epoint\_norm**(p)

epoint \*p;

**Module:**  mrcurve.c

**Description:**  Normalises a point on the current active GF(_p_) elliptic curve. This sets the _z_ coordinate to 1\. Point addition is quicker when adding a normalised point. This function does nothing if affine coordinates are being used (in which case there is no _z_ co-ordinate)

**Parameters:**  A point on the current active elliptic curve.

**Return value:**  TRUE if successful.

### 9.3.31  epoint2\_norm

**Function:**  BOOL **epoint2\_norm**(p)

epoint \*p;

**Module:**  mrec2m.c

**Description:**  Normalises a point on the current active GF(2_<sup>m</sup>_) elliptic curve. This sets the _z_ coordinate to 1\. Point addition is quicker when adding a normalised point. This function does nothing if affine coordinates are being used (in which case there is no _z_ co-ordinate)

**Parameters:**  A point on the current active elliptic curve.

**Return value:**  TRUE if successful.

### 9.3.32  epoint\_set

**Function:**  BOOL **epoint\_set**(x,y,lsb,p)

big x,y;
int lsb;
epoint \*p;

**Module:**  mrcurve.c

**Description:**  Sets a point on the current active GF(_p_) elliptic curve (if possible).

**Parameters:**  The integer co-ordinates _x_ and _y_ of the point _p_. If  _x_ and _y_ are not distinct variables then _x_ only is passed to the function, and _lsb_ is taken as the least significant bit of _y._ In this case the full value of _y_ is reconstructed internally. This is known as "point decompression" (and is a bit time-consuming, requiring the extraction of a modular square root). On exit _p=(x,y)_.

**Return value:**  TRUE if the point exists on the current active point, otherwise FALSE.

**Restrictions:**  None

**Example:**

``` c
    /* decompress p */ 
    p=epoint_init();
    epoint_set(x,x,1,p);
```
   

### 9.3.33  epoint2\_set

**Function:**  BOOL **epoint2\_set**(x,y,lsb,p)

big x,y;
int lsb;
epoint \*p;

**Module:**  mrec2m.c

**Description:**  Sets a point on the current active GF(2_<sup>m</sup>_) elliptic curve (if possible).

**Parameters:**  The integer co-ordinates _x_ and _y_ of the point _p_. If  _x_ and _y_ are not distinct variables then _x_ only is passed to the function, and _lsb_ is taken as the least significant bit of _y/x._ In this case the full value of _y_ is reconstructed internally. This is known as "point decompression" (and is a bit time-consuming, requiring the extraction of a field square root). On exit _p=(x,y)_.

**Return value:**  TRUE if the point exists on the current active point, otherwise FALSE.

**Restrictions:**  None

**Example:**

``` c
    /* decompress p */
    p=epoint_init();
    epoint2_set(x,x,1,p);
```

### 9.3.34  epoint\_x

**Function:**  BOOL **epoint\_x**(x)

big x;

**Module:**  mrcurve.c

**Description:**  Tests to see if the parameter _x_ is a valid co-ordinate of a point on the curve. It is faster to test an _x_ co-ordinate first in this way, rather than trying to directly set it on the curve by calling **epoint_set**, as it avoids an expensive modular square root.

**Parameters:**  The integer coordinate _x_.

**Return value:**   TRUE if _x_ is the coordinate of a curve point, otherwise FALSE

**Restrictions:**   None

### 9.3.35  mul\_brick

**Function:**  int **mul\_brick**(binst,e,x,y)

ebrick \*binst;
big e,x,y;

**Module:**  mrebrick.c

**Description:**  Carries out a GF(_p_) elliptic curve multiplication using the precomputed values stored in the _ebrick_ structure.

**Parameters:**  A pointer to the current instance, a big exponent _e_ and a big number _w_. On exit (_x,y_) = _e.G_ _mod n_, where _G_ and _n_ are specified in the initial call to **ebrick_init.** If _x_ and _y_ are not distinct variables, only _x_ is returned.

**Return value:**  The least significant bit of _y_.

**Restrictions:**  Must be preceded by a call to **ebrick_init**.   

### 9.3.36  mul2\_brick

**Function:**  int **mul2\_brick**(binst,e,x,y)

ebrick2 \*binst;
big e,x,y;

**Module:**  mrec2m.c

**Description:**  Carries out a GF(2_<sup>m</sup>_)  elliptic curve multiplication using the precomputed values stored in the _ebrick2_ structure.

**Parameters:**  A pointer to the current instance, a big exponent _e_ and a big number _w_. On exit (_x,y_) = _e.G_, where _G_ is specified in the initial call to **ebrick2_init.** If _x_ and _y_ are not distinct variables, only _x_ is returned.

**Return value:**  The least significant bit of _y/x_.

**Restrictions:**  Must be preceded by a call to **ebrick2_init**.

### 9.3.37  point\_at\_infinity

**Function:**  BOOL **point\_at\_infinity**(p)

epoint \*p;

**Module:**  mrcore.c

**Description:**   Tests if an elliptic curve point is the "point at infinity".

**Parameters:**  An elliptic curve point _p_.

**Return value:**  TRUE if _p_ is the point-at-infinity, otherwise FALSE.

**Restrictions:**  The point must be initialised.

## 9.4  Encryption Routines

### 9.4.1  aes\_decrypt

Function:  mrz_unsign32 aes\_**decrypt**(a,buff)

aes \*a;
char \*buff;

**Module:**  mraes.c

**Description:**  Decrypts a 16 or _n_ byte input buffer in situ.

**Parameters:**  Pointer to an initialised instance of an _aes_ structure defined in _miracl.h_, and to the buffer of bytes to be decrypted. If the mode of operation is as a block cipher (**MR_ECB** or **MR_CBC**) then 16 bytes will be decrypted. If the mode of operation is as a stream cipher (**MR_CFB**_n_, **MR_OFB**_n_ or **MR_PCFB**_n_) then _n_ bytes will be decrypted.

**Return value:**  In **MR_CFB**_n_ and **MR_PCFB**_n_ modes the _n_ byte(s) that were shifted off the end of the input register as result of decrypting the _n_ input byte(s), otherwise 0.

### 9.4.2  aes\_encrypt

**Function:**  mr\_unsign32 **aes\_encrypt**(a,buff)

aes \*a;
char \*buff;

**Module:**  mraes.c

**Description:**  Encrypts a 16 or _n_ byte input buffer in situ.

**Parameters:**  Pointer to an initialised instance of an _aes_ structure defined in _miracl.h_, and to the buffer of bytes to be encrypted. If the mode of operation is as a block cipher (**MR_ECB** or **MR_CBC**) then 16 bytes will be encrypted. If the mode of operation is as a stream cipher (**MR_CFB**_n_, **MR_OFB**_n_ or **MR_PCFB**_n_) then a _n_ bytes will be encrypted.

**Return value:**  In **MR_CFB**_n_ and **MR_PCFB**_n_ modes the _n_ byte(s) that were shifted off the end of the input register as result of encrypting the _n_ input byte(s), otherwise 0.

### 9.4.3  aes\_end

**Function:**  void **aes\_end**(a)

aes \*a;

**Module:**  mraes.c

**Description:**  Ends an AES encryption session, and de-allocates the memory associated with it. The internal session key data is destroyed.

**Parameters:**  Pointer to an initialised instance of an _aes_ structure defined in _miracl.h_

**Return value:**  None

### 9.4.4  aes\_getreg

**Function:**  void **aes\_getreg**(a,ir)

aes \*a;
char \*ir;

**Module:**  mraes.c

**Description:**  Reads the current contents of the input chaining register associated with this instance of the AES. This is the register initialised by the IV in the calls to **aes_init**  and  **aes_reset**.

**Parameters: ** Pointer to an instance of the _aes_ structure, defined in _miracl.h_, and a character array to hold the extracted 16-byte data.

**Return value:**  None

### 9.4.5  aes\_init

**Function:**  BOOL **aes\_init**(a,mode,nk,key,iv)

aes \*a;
int mode,nk;
char \*key,\*iv;

**Module:**  mraes.c

**Description:**  Initialises an Encryption/Decryption session using the Advanced Encryption Standard (AES). This is a block cipher system that encrypts data in 128-bit blocks using a key of 128, 192 or 256 bits. See [Stinson] for more background on block ciphers.

**Parameters:**  Pointer to an instance of the _aes_ structure defined in _miracl.h,_ the _mode_ of operation to be used, an integer _nk_ which specifies the size of the Key in bytes, and pointers to the key itself and the optional Initialisation Vector (IV). The mode can be one of **MR_ECB** (Electronic Code Book), **MR_CBC** (Cipher Block Chaining), **MR_CFB**_n_ (Cipher Feed-back where _n_ is 1, 2 or 4), **MR_PCFB**_n_ (error Propagating Cipher Feed-back where _n_ is 1, 2 or 4) or **MR_OFB**_n_ (Output Feed-back where _n_ is 1, 2, 4, 8 or 16).  The value of _n_ indicates the number of bytes to be processed in each application. For more information on Modes of Operation, see [Stinson]. **MR_PCFB**_n_ is an invention of our own [Scott93]. See below.

The value of _nk_ can be 16, 24 or 32\. A 16 bytes initialisation vector _iv_ should be specified for all modes other than MR_ECB, in which case it can be NULL.

**Return value:**  TRUE if initialisation succeeded, otherwise FALSE.

![](\data\assets\images\cunks\9-1.png)

### 9.4.6  aes\_reset

**Function:**  void **aes_reset**(a,mode,iv)

aes \*a;
int mode;
char \*iv;

**Module:**  mraes.c

**Description:**  Resets the AES structure

**Parameters:**  Pointer to an instance of the _aes_ structure defined in _miracl.h_, an indication of the new _mode_ of operation, and a pointer to a (possibly new) initialisation vector _iv_. See above for the modes allowed.

**Return value:** None

### 9.4.7  shs\_init

**Function:**  void **shs\_init**(psh)

sha \*psh;

**Module:**  mrshs.c

**Description:**  Initialises an instance of the Secure Hash Algorithm SHA-1\. Must be called before new use.

**Parameters:**  Pointer to an instance of a structure defined in _miracl.h_

**Return value:**  None

### 9.4.8  shs\_hash

**Function:**  void **shs\_hash**(psh,hash)

sha \*psh;
char hash[20];

**Module:**  mrshs.c

**Description:**  Generates a twenty byte (160 bit) hash value into the provided array.

**Parameters:**  Pointer to the current instance, and pointer to array to be filled.

**Return value:**  None

### 9.4.9  shs\_process

**Function:**  void **shs\_process**(psh,ch)

sha \*psh;
int ch;

**Module:**  mrshs.c

**Description:**  Processes a single byte. Typically called many times to provide input to the hashing process. The hash value of all the processed bytes can be retrieved by a subsequent call to **shs_hash**.

**Parameters:**  Pointer to the current instance, and character to be processed.

**Return value:**  None

### 9.4.10  shs256\_init

**Function:**  void **shs256\_init**(psh)

sha256 \*psh;

**Module:**  mrshs256.c

**Description:**  Initialises an instance of the Secure Hash Algorithm SHA-256\. Must be called before new use.

**Parameters:**  Pointer to an instance of a structure defined in _miracl.h_

**Return value:**  None

### 9.4.11  shs256\_hash

**Function:**  void **shs256\_hash**(psh,hash)

sha256 \*psh;
char hash[32];

**Module:**  mrshs256.c

**Description:**  Generates a 32 byte (256 bit) hash value into the provided array.

**Parameters:**  Pointer to the current instance, and pointer to array to be filled.

**Return value:**  None

### 9.4.12  shs256\_process

**Function:**  void **shs256\_process**(psh,ch)

sha256 \*psh;
int ch;

**Module:**  mrshs256.c

**Description:**  Processes a single byte. Typically called many times to provide input to the hashing process. The hash value of all the processed bytes can be retrieved by a subsequent call to **shs256_hash**.

**Parameters:**  Pointer to the current instance, and character to be processed.

**Return value:**  None

### 9.4.13  shs384\_init

**Function:**  void **shs384\_init**(psh)

sha384 \*psh;

**Module:**  mrshs512.c

**Description:**  Initialises an instance of the Secure Hash Algorithm SHA-384\. Must be called before new use.

**Parameters:**  Pointer to an instance of a structure defined in _miracl.h_

**Return value:**  None

**Restrictions:**  The SHA-384 algorithm is only available if 64-bit data-type is defined.

### 9.4.14  shs384\_hash

**Function:**  void **shs384\_hash**(psh,hash)

sha384 \*psh;
char hash[48];

**Module:**  mrshs512.c

**Description:**  Generates a 48 byte (384 bit) hash value into the provided array.

**Parameters:**  Pointer to the current instance, and pointer to array to be filled.

**Return value:**  None

### 9.4.15  shs384\_process

**Function:**  void **shs512\_process**(psh,ch)

sha384 \*psh;
int ch;

**Module:**  mrshs512.c

**Description:**  Processes a single byte. Typically called many times to provide input to the hashing process. The hash value of all the processed bytes can be retrieved by a subsequent call to **shs384_hash**.

**Parameters:**  Pointer to the current instance, and character to be processed.

**Return value:**  None

### 9.4.16  shs512\_init

**Function:**  void **shs512\_init**(psh)

sha512 \*psh;

**Module:**  mrshs512.c

**Description:**  Initialises an instance of the Secure Hash Algorithm SHA-512\. Must be called before new use.

**Parameters:**  Pointer to an instance of a structure defined in _miracl.h_

**Return value:**  None

**Restrictions:**  The SHA-512 algorithm is only available if 64-bit data-type is defined.

### 9.4.17  shs512\_hash

**Function:**  void **shs512\_hash**(psh,hash)

sha512 \*psh;
char hash[64];

**Module:**  mrshs512.c

**Description:**  Generates a 64 byte (512 bit) hash value into the provided array.

**Parameters:**  Pointer to the current instance, and pointer to array to be filled.

**Return value:**  None

### 9.4.18  shs512\_process

**Function:**  void **shs512_process**(psh,ch)

sha512 \*psh;
int ch;

**Module:**  mrshs512.c

**Description:**  Processes a single byte. Typically called many times to provide input to the hashing process. The hash value of all the processed bytes can be retrieved by a subsequent call to **shs512_hash**.

**Parameters:**  Pointer to the current instance, and character to be processed.

**Return value:**  None

### 9.4.19  strong\_bigdig

**Function:**  void **strong\_bigdig**(rng,n,b,x)

csprng \*rng;
int n,b;
big x;

**Module:**  mrstrong.c

**Description:**  Generates a big random number of given length from the cryptographically strong generator _rng_.

**Parameters:** A pointer to the random number generator _rng_. A big number _x_ and two integers _n_ and _b_. On exit _x_ contains a big random number _n_ digits long to base _b_.

**Return value:**  None

**Restrictions:**  The base _b_ must be printable, that is 2 £ _b_ £ 256.

### 9.4.20  strong\_bigrand

**Function:**  void **strong_bigrand**(rng,w,x)

csprng \*rng;
big w,x;

**Module:**  mrstrong.c

**Description:**  Generates a cryptographically strong random big number _x_ using the random number generator _rng_ such that _0__£x < w_

**Parameters:**  Two big numbers _w_ and _x_, and a random number generator _rng_

**Return value:**   None

### 9.4.21  strong\_init

**Function:**  void **strong_init**(rng,rawlen,raw,tod)

csprng \*rng;
int rawlen;
char \*raw;
long tod;

**Module:**  mrstrong.c

**Description:**  Initialize the cryptographically strong random number generator _rng_.

**Parameters:**  A pointer to the random number generator _rng_. An array _raw_ of length _rawlen_ and a 32-bit time-of-day value _tod_. These two sources are used together to seed the generator. The former might be provided from random keystrokes, the latter from an internal clock. Subsequent calls to **strong_rng** will provide random bytes.

**Return value:**  None

**Example:**  See _test1363.c_ and _p1363.c_ for an example of use.  

### 9.4.22  strong\_kill

**Function:**  void **strong\_kill**(rng)

csprng \*rng;

**Module:**  mrstrong.c

**Description:**  Kills the internal state of the random number generator _rng_

**Parameters:**  A pointer to a random number generator

**Return value:**  None

### 9.4.23  strong\_rng

**Function:** int **strong_rng**(rng)

csprng \*rng;

**Module:**  mrstrong.c

**Description:**  Generates a sequence of cryptographically strong random bytes.

**Parameters:**  A pointer to a random number

**Return value:**  A random byte

## 9.5  Floating-Slash Routines

### 9.5.1  build

**Function:**  void **build**(x,gener)

flash x;
int (\*gener)();

**Module:**  mrbuild.c

**Description:**  Uses supplied generator of regular continued fraction expansion to build up a flash number _x_, rounded if necessary.

**Parameters:**  The flash number created, and the generator function.

**Return value:**  None

**Example:**

``` c
    //This will calculate the golden ratio _(1+__Ö5)/2_ in _x_ - very quickly!
    int phi(w,n)
    flash w;
    int n;
    { /* rcf generator for golden ratio */
        return 1;
    }
    ...
    build(x,phi);
```

### 9.5.2  dconv

**Function:**  void **dconv**(d,x)

double d;
flash x;

**Module:**  mrflash.c

**Description:**  Converts a double to flash format.

**Parameters:**  A double _d_ and a flash variable _x_. On exit _x_ will contain the flash equivalent of _d_.

**Return value:**  None

### 9.5.3  denom

**Function:**  void **denom**(x,y)

flash x;
big y;

**Module:**  mrcore.c

**Description:**  Extract the denominator of a flash number

**Parameters:**  A flash number _x_ and a big number _y_. On exit _y_ will contain the denominator of _x_.

**Return value:**  None

**Restrictions:**  None

### 9.5.4  facos

**Function:**  void **facos**(x,y)

flash x,y;

**Module:**  mrflsh3.c

**Description:**  Calculates arc-cosine of a flash number, using **fasin**.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=arccos(x)_.

**Return value:**  None

**Restrictions:**  _|x|_ must be less than or equal to 1.

### 9.5.5  facosh

**Function:**  void **facosh**(x,y)

flash x,y;

**Module:**  mrflsh4.c

**Description:**  Calculates hyperbolic arc-cosine of a flash number.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=arccosh(x)_.

**Return value:**  None

**Restrictions:**  _|x_| must be greater than or equal to 1.

### 9.5.6  fadd

**Function:**  void **fadd**(x,y,z)

flash x,y,z;

**Module:**  mrflash.c

**Description:**  Add two flash numbers.

**Parameters:**  Three flash numbers _x, y_ and _z_. On exit _z=x+y_.

**Return value:**  None

**Restrictions:**  None

### 9.5.7  fasin

**Function:**  void **fasin**(x,y)

flash x,y;

**Module:**  mrflsh3.c

**Description:**  Calculates arc-sin of a flash number, using **fatan**.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=arcsin(x)_.

**Return value:**  None

**Restrictions:**  _|x_| must be less than or equal to 1.  

### 9.5.8  fasinh

**Function:**  void **fasinh**(x,y)

  flash x,y;

**Module:**  mrflsh4.c

**Description:**  Calculates hyperbolic arc-sin of a flash number.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=arcsinh(x)_.

**Return value:**  None

### 9.5.9  fatan

**Function:**  void **fatan**(x,y)

flash x,y;

**Module:**  mrflsh3.c

**Desciption:**  Calculates the arc-tangent of a flash number, using _O(n<sup>2.5</sup>)_method based on Newton's iteration.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=arctan(x)_.

**Return value:**  None

### 9.5.10  fatanh

**Function:**  void **fatanh**(x,y)

flash x,y;

**Module:**  mrflsh4.c

**Desciption:**  Calculates the hyperbolic arc-tangent of a flash number.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=arctanh(x)_.

**Return value:**  None

**Restrictions:**  _x<sup>2</sup>_ must be less than 1

### 9.5.11  fcomp

**Function:**  int **fcomp**(x,y)

flash x,y;

**Module:**  mrflash.c

**Description:**  Compare two flash numbers.

**Parameters:**  Two flash numbers _x_ and _y_.

**Return value:**  Returns -1 if _y>x_, +1 if _x>y_ and 0 if _x=y_.

### 9.5.12  fconv

**Function:**  void **fconv**(n,d,x)

int n,d;
flash x;

**Module:**  mrflash.c

**Description:**  Convert a simple fraction to flash format.

**Parameters:**  Integers _n_ and _d_, and a flash number _x_.

On exit _x=n/d_

**Return value:**  None

### 9.5.13  fcos

**Function:**  void **fcos**(x,y)

flash x,y;

**Module:**  mrflsh3.c

**Description:**  Calculates cosine of a given flash angle, using **ftan**.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=cos(x)_.

**Return value:**  None

**Restrictions:**  None

### 9.5.14  fcosh

**Function:**  void **fcosh**(x,y)

flash x,y;

**Module:**  mrflsh4.c

**Description:**  Calculates hyperbolic cosine of a given flash angle.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=cosh(x)_.

**Return value:**  None

### 9.5.15  fdiv

**Function:**  void **fdiv**(x,y,z)

flash x,y,z;

**Module:**  mrflash.c

**Description:**  Divides two flash numbers.

**Parameters:**  Three big numbers _x, y_ and _z_. On exit _z=x/y_.

**Return value:**  None

### 9.5.16  fdsize

**Function:**  double **fdsize**(x)

flash x;

**Module:**  mrdouble.c

**Description:**  Converts a flash number to double format.

**Parameters:**  A flash number _x_.

**Return value:**  The value of the parameter _x_ as a double.

**Restrictions:** The value of _x_ must be representable as a double.

### 9.5.17  fexp

**Function:**  void **fexp**(x,y)

flash x,y;

**Module:**  mrflsh2.c

**Description:**  Calculates the exponential of a flash number using _O(n<sup>2.5</sup>)_ method.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=e<sup>x</sup>_.

**Return value:**  None

**Restrictions:**  None

### 9.5.18  fincr

**Function:**  void **fincr**(x,n,d,y)

big x,y;
int n,d;

**Module:**  mrflash.c

**Description:**  Add a simple fraction to a flash number.

**Parameters:**  Two flash numbers _x_ and _y_, and two integers _n_ and _d_.

On exit .

**Return value:**  None

**Restrictions:**  None

**Example:**

``` c
    //This subtracts two-thirds from the value of _x_.
    fincr(x,-2,3,x);
```

### 9.5.19  flog

**Function:**  void **flog**(x,y)

flash x,y;

**Module:** mrflsh2.c

**Description:**  Calculates the natural log of a flash number using _O(n<sup>2.5</sup>)_ method.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=log(x)_.

**Return value:**  None

**Restrictions:**  None

### 9.5.20  flop

**Function:**  void **flop**(x,y,op,z)

flash x,y,z;
int \*op;

**Module:**  mrflash.c

**Description:**  Perform primitive flash operation. Used internally.

**Parameters:**  Three flash numbers _x, y_ and _z_. On exit z_=Fn(x,y),_ where the function performed depends on the parameter _op_. See source listing comments for more details.

**Return value:**  None

**Restrictions:**  None

### 9.5.21  fmodulo

**Function:**  void **fmodulo**(x,y,z)

flash x,y,z;

**Module:**  mrflash.c

**Description:**  Find the remainder when one flash number is divided by another.

**Parameters:**  Three flash numbers _x, y_ and _z_. On exit _z=x mod y_;

**Return value:**  None

**Restrictions:**  None

### 9.5.22  fmul

**Function:**  void **fmul**(x,y,z)

flash x,y,z;

**Module:**  mrflash.c

**Description:**  Multiply two flash numbers.

**Parameters:**  Three flash numbers _x, y_ and _z_. On exit _z=x.y_

**Return value:**  None

**Restrictions:**  None

### 9.5.23  fpack

**Function:**  void **fpack**(n,d,x)

flash x;
big n,d;

**Description:**  Forms a flash number from big numerator and denominator.

**Parameters:**  A flash number _x_ and two big numbers _n_ and _d_.

On exit .

**Return value:**  None

**Restrictions:**  The denominator must be non-zero. Flash variable _x_ and big variable _d_ must be distinct. The resulting flash variable must not be too big for the representation.

### 9.5.24  fpi

**Function:**  void **fpi**(x)

flash x;

**Module:**  mrpi.c

**Description:**  Calculates p using Guass-Legendre _O(n<sup>2</sup>.log n)_ method. Note that on subsequent calls to this routine, p is immediately available, as it is stored internally. (This routine is disappointingly slow. There appears to be no simple way to calculate a rational approximation to p quickly).

**Parameters:**  A flash number _x_. On exit _x=__p._

**Return value:**  None

**Restrictions:**  None. Internally allocated memory is freed when the current MIRACL instance is ended by a call to **mirexit**.

### 9.5.25  fpmul

**Function:**  void **fpmul**(x,n,d,y)

flash x,y;
int n,d;

**Module:**  mrflash.c

**Description:**  Multiplies a flash number by a simple fraction.

**Parameters:**  Two flash numbers _x_ and _y_, and two integers _n_ and _d_.

On exit

**Return value:**  None

**Restrictions:**  None

### 9.5.26  fpower

**Function:**  void **fpower**(x,n,y)

flash x,y;
int n;

**Module:**  mrflsh1.c

**Description:**  Raises a flash number to an integer power.

**Parameters:**  Flash variables _x_ and _y_, and an integer _n_.

On exit _y=x<sup>n</sup>_.

**Return value:**  None

### 9.5.27  fpowf

**Function:**  void **fpowf**(x,y,z)

  flash x,y,z;

**Module:**  mrflsh2.c

**Description:**  Raises a flash number to a flash power.

**Parameters:**  Three flash numbers _x_, _y_ and _z_. On exit _z=x<sup>y</sup>_

**Return value:**  None

### 9.5.28  frand

**Function:**  void **frand**(x)

  flash x;

**Module:**  mrfrnd.c

**Description:**  Generates a random flash number.

**Parameters:**  A big number _x_. On exit _x_ contains a flash random number in the range _0 < x < 1_.

**Return value:**  None

### 9.5.29  frecip

**Function:**  void **frecip** (x,y)

flash x,y;

**Module:**  mrflash.c

**Description:**  Calculates reciprocal of a flash number.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=1/x_.

**Return value:**  None

### 9.5.30  froot

**Function:**  BOOL **froot**(x,m,y)

flash x,y;
int m;

**Module:**  mrflsh1.c

**Description:**  Calculates _m_-th root of a flash number using Newton's _O(n<sup>2</sup>)_ method.

**Parameters:**  Flash numbers _x_ and _y_, and an integer _m_.

On exit _y_ is the _m_-th root of _x_.

**Return value:**  TRUE for exact root, otherwise FALSE

### 9.5.31  fsin

**Function:**  void **fsin**(x,y)

flash x,y;

**Module:**  mrflsh3.c

**Description:**  Calculates sine of a given flash angle. Uses **ftan**.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=sin(x)_.

**Return value:**  None

### 9.5.32  fsinh

**Function:**  void **fsinh**(x,y)

flash x,y;

**Module:**  mrflsh4.c

**Description:**  Calculates hyperbolic sine of a given flash angle.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=sinh(x)_.

**Return value:**  None

### 9.5.33  fsub

**Function:**  void **fsub**(x,y,z)

flash x,y,z;

**Module:**  mrflash.c

**Description:**  Subtract two flash numbers.

**Parameters:**  Three flash numbers _x, y_ and _z_.

On exit _z=x-y_.

**Return value:**  None

### 9.5.34  ftan

**Function:**  void **ftan**(x,y)

  flash x,y;

**Module:**  mrflsh3.c

**Description:**  Calculates the tan of a given flash angle, using an _O(n<sup>2.5</sup>)_ method.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=tan(x)_.

**Return value:**  None

### 9.5.35  ftanh

**Function:**  void **ftanh**(x,y)

flash x,y;

**Module:**  mrflsh4.c

**Description:**  Calculates the hyperbolic tan of a given flash angle.

**Parameters:**  Two flash numbers _x_ and _y_. On exit _y=tanh(x)_.

**Return value:**  None

**Restrictions:**  None

### 9.5.36  ftrunc

**Function:**  void **ftrunc**(x,y,z)

flash x,z;
big y;

**Module:  mrflash.c

**Description:**  Separates a flash number to a big number and a flash remainder.

**Parameters:**  Flash numbers _x_ and _z_, and a big number _y_. On exit _y=int(x)_ and _z_ is the fractional remainder. If _y_ is the same as _z_, only _int(x)_ is returned.

**Return value:**  None

**Restrictions:**  None

### 9.5.37  numer

**Function:**  void **numer**(x,y)

flash x;
big y;

**Module:**  mrcore.c

**Description:**  Extract the numerator of a flash number.

**Parameters:**  A flash number _x_ and a big number _y_.

On exit _y_ will contain the numerator of _x_.

**Return value:**  None

**Restrictions:**  None

### 9.5.38  mround

**Function:** void **mround**(n,d,x)

flash x;
big n,d;

**Module:**  mrround.c

**Description:**  Forms a rounded flash number from big numerator and denominator. If rounding takes place the instance variable **EXACT** is set to FALSE. **EXACT** is initialised to TRUE in routine **mirsys**. This routine is used internally.

**Parameters:**  A flash number _x_ and two big numbers _n_ and _d_. On exit _x=R{n/d}_, that is the flash number _n/d_ rounded if necessary to fit the representation.

**Return value:**  None

**Restrictions:**  The denominator must be non-zero.
