# Real numbers

The real numbers include the rational numbers and irrational numbers.

The real numbers can be represented using

* simple fractions
* decimal fractions
* scientific notation.

## Scientific notation

A number in the scientific notation is written in the following form:

$$m \cdot 10^p.$$

The coefficient $m$ is a decimal fraction that is called the *mantissa*. The integer $p$ is called the exponent.

$$12.345 = \underbrace{12345}_\text{mantissa} \cdot 10^{\overbrace{-3}^\text{exponent}}$$

The scientific notation is used for representing very big or very small numbers, e.g.

* the speed of light: $299792458 \frac{m}{s} \approx 3 \cdot 10^8 \frac{m}{s}$
* the elementary charge: $−1.602176634 \cdot 10^{−19} C = -1.6 \cdot 10^{19}C$.

There is no unique way to represent the number in the scientific notation. For example, $−1.602176634 \cdot 10^{−19} C$ and $−16.02176634 \cdot 10^{−20} C$ represent the same number.

### Floating point

The term *floating point* refers to the fact that the number's radix point can
"float" anywhere to the left, right, or between the significant digits of the
number. This position is indicated by the exponent, so floating point can be
considered a form of scientific notation.

### Fixed point

In computing, fixed-point is a method of representing fractional (non-integer) numbers by storing a fixed number of digits
of their fractional part. Dollar amounts, for example, are often stored with exactly two fractional digits, representing
the cents (1/100 of dollar). More generally, the term may refer to representing fractional values as integer multiples of
some fixed small unit, e.g. a fractional amount of hours as an integer multiple of ten-minute intervals. Fixed-point number
representation is often contrasted to the more complicated and computationally demanding floating-point representation.

### Normalized scientific notation

A number is *normalized* when it is written in
scientific notation with one non-zero decimal digit before the decimal point.
Thus, a real number, when written out in normalized scientific notation, is as
follows:

$$\pm d_0 . d_1 d_2 d_3 \dots \times 10^n,$$

where $n$ is an integer, $d_0, d_1, d_2, d_3, \ldots,$ are the digits of the number in base 10, and $d_0$ is not zero. 

A method of representing fractional numbers by storing a fixed number of digits of their fractional part is called the *fixed-point*.

> [!IMPORTANT]  
> What is a normalized scientific notation form for the numbers 64, 0.16, 1000, 0?

> [!IMPORTANT]
> How floating-point numbers (literals) [are represented](https://go.dev/ref/spec#Floating-point_literals) in Go?

> [!IMPORTANT]
> What are advantages of the scientific notation?

## Precision

A floating point number stored in a computer uses a fixed precision. For example, $12.34$ is a floating-point number in base ten with four digits of precision; $12.345$ is not a floating-point number in base ten with four digits of precision. In a floating-point arithmetic with four base-ten digits of precision, the sum $12.34 + 1.001 = 13.341$ might be rounded to $13.34$.

* Absolute error: $|X_\text{true} - X_\text{observed}|$.
* Relative error: $\frac{|X_\text{true} - X_\text{observed}|}{X_\text{true}}$.

### Relative error

The relative error for fixed precision numbers is constant.

## Binary scientific notation

A binary number in the scientific notation is written in the following form:

$$m \cdot 2^p.$$

2-base $\leftrightarrow$ 10-base conversion examples:

* $101101.101_2 = 1\cdot2^5+0\cdot2^4+1\cdot2^3+1\cdot2^2+0\cdot2^1+1\cdot2^0+1\cdot2^{-1}+0\cdot2^{-2}+1\cdot2^{-3}=45.625$

* $0.2_{10} = \frac{1}{5}_2 =\ ?$
  * $0.2 \cdot 2 = 0.4 + \textbf{0}$
  * $0.4 \cdot 2 = 0.8 + \textbf{0}$
  * $0.8 \cdot 2 = 0.6 + \textbf{1}$
  * $0.6 \cdot 2 = 0.2 + \textbf{1}$
  * $0.2 \cdot 2 = 0.4 + \textbf{0}$
  * $0.4 \cdot 2 = 0.8 + \textbf{0}$
  * $0.2_{10} = 0.(0011)_2$

### Exercises
* $0.1101_2 = \ ?_{10}$ 
* $0.7_{10} = \ ?_2$
* $10.10101_2 = \ ?_{10}$
* $22.589_{10} = \ ?_2$
* $-1.10101_2 = \ ?_{10}$
* $7.875_{10} = \ ?_2$
* $101.1011_2 = \ ?_{10}$
* $253.75_{10} = \ ?_2$

## Single precision (`float32`)

* [Wikipedia: Single-precision floating-point format](https://en.wikipedia.org/wiki/Single-precision_floating-point_format)
* [Exposing floating point](https://ciechanow.ski/exposing-floating-point/)
* https://float.exposed/
* [Float32 Go playground demo](https://go.dev/play/p/ppV7IGUk9SX)
* [Another Go playground demo](https://goplay.tools/snippet/q82DkD5aKLK)

## Subnormal numbers

* [Wikipedia: Subnormal numbers](https://en.wikipedia.org/wiki/Subnormal_number)

## Double precision (`float64`)

* [Wikipedia: Double-precision floating-point format](https://en.wikipedia.org/wiki/Double-precision_floating-point_format)

## Extended precision (80 bits)

Note: Go doesn't support it!

* [Wikipedia: Extended precision](https://en.wikipedia.org/wiki/Extended_precision)

## Errors

Let's consider this example (https://go.dev/play/p/1UrxY17kz6R):

```go
const delta = 1e-6
var sum float32 = 1e6
for i := 0; i < 1e6; i++ {
		sum += delta
}
fmt.Printf("%F\n", sum)           // ???
fmt.Printf("%F\n", 1e6+delta*1e6) // ???
```

### Hypothetical machine

Let's image a hypothetical decimal floating point processor, which uses 5 decimal digits to represent a number. The first digit is an exponent with delta 5, and the next four digits represent the number with the decimal point always being after the first digit. We event won't store it.

Examples:

1. $1=1.000 \cdot 10^{0} \therefore exp=0+5=5, m=1.000 \therefore x=51000$.
2. $12.34=1.234 \cdot 10^{1} \therefore exp=1+5=6,  m=1.2345 \therefore x=61234$
3. $0.012=1.2 \cdot 10^{-2} \therefore exp=-2+5=3, m=1.200 \therefore x=31200$

Let's introduce some operations:

```
1) 1234+4321=5555
   81234
   84321
   -----
   85555    =5555

2) 12.34+43.21=55.55
   61234
   64321
   -----
   65555      =55.55

3) 1.234+43.21=44.444
   51234
   64321
   -----
   6_1234
   64321
   ------
   644444
   64444      =44.44

4) 10000x0.0001+1.000=2
   11000   12000  ...  49999       51000
   11000   11000       11000       51000
   -----   -----       49999       _____
   12000   13000       4   1000    52000 = 2
                       ________
                       51000

5) 1+10000*0.0001=2
   51000         51000   ... It's always 1
   11000         11000
   _____         _____
   51000         .....
   5    1000     51000 = 1
   _________
   51000
```
### Exercises

<!-- solution: https://go.dev/play/p/J5kb08-uH5C -->

1. Compare $\frac{a \cdot b + c}{a \cdot b + d}$ and $\frac{a+\frac{c}{b}}{a+\frac{d}{b}}$ with $a=10^{-323}, c=4 \cdot 10^{-323}, d=8 \cdot 10^{-323}$ and $b=5.7$.
2. Compare $x+\sqrt{x^2-1}$ and $\frac{1}{x-\sqrt{x^2-1}}$ around $10^7$ to $7 \cdot 10^7$ range.

### Errors grow

$$\begin{cases}
  x+10y=11 \\
  100x+1001y=1101 \\
\end{cases}$$

$$x=11-10y$$

$$100 \cdot (11-10y)+1001y=1101$$

$$1100-1000y+1001y=1101$$

$$1100+y=1101$$

$$\begin{cases}
x=11-10y=11-10=1 \\
y=1101-1100=1
\end{cases}$$

But let's add $10^{-2}$ to the right side:

$$\begin{cases}
  x+10y=11.01 \\ 
  100x+1001y=1101 
\end{cases}$$

$$x=11.01-10y$$

$$100 \cdot (11.01-10y)+1001y=1101$$

$$1101-1000y+1001y=1101$$

$$y=0$$

$$\begin{cases}
    x=11.01 \\
    y=0
\end{cases}$$

# Bisection Method Algorithm

Follow the below procedure to get the solution for the continuous function:

For any continuous function $f(x)$,

-   Find two points, say $a$ and $b$ such that $a < b$ and $f(a)* f(b)$ < 0
-   Find the midpoint of $a$ and $b$, say $t$
-   $t$ is the root of the given function if $f(t) = 0$; else follow the next step
-   Divide the interval $[a, b]$ – If $f(t)*f(a) <0$, there exist a root between $t$ and $a$  
    – else if $f(t) *f (b) < 0$, there exist a root between $t$ and $b$
-   Repeat above three steps until $|a-b| < \epsilon$.

The bisection method is an approximation method to find the roots of the given equation by repeatedly dividing the interval. This method will divide the interval until the resulting interval is found, which is extremely small.

## Exercises

- $x^3-2x=5$
- $3x^4-4x^3-12x^2=5$
- $x-5sin(x)=3.5$
- $(1+x)e^{ax}=b$ with some $a$ and $b$ e.g. $3; 5$ and $-2; -8$

# Examples 

* [Checking for equality](https://go.dev/play/p/lKdvVM72C-Y)
* [Epsilon](https://go.dev/play/p/iUP37yY5Cdt)
* [Arithmetic expressions](https://go.dev/play/p/-MKUWeDBml7)
* [Precision](https://go.dev/play/p/l-LAjux3JAm)
* [The odometer that stopped](https://go.dev/play/p/CLmsmYeYQDS)
   * https://float.exposed/0x48800000
* [Subnormal numbers precision Go playground demo](https://go.dev/play/p/zYLUSFOpyDX)
* [Deep Space Kraken](https://wiki.kerbalspaceprogram.com/wiki/Deep_Space_Kraken)
  * [YT](https://www.youtube.com/watch?v=bfuoMhhye4g)
