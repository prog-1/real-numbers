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

> [!IMPORTANT]
> What is an absolute and a relative error of a floating-point number in base ten with four digits or precision?

### Absolute error
* The absolute error is $0.001$ for numbers with four digits of precision with the exponent $0$;
* the absolute error is $0.01$ for numbers with four digits of precision with the exponent $1$;
* the absolute error is $0.0001$ for numbers with four digits of precision with the exponent $-1$;
* etc.

### Relative eror

The relative error for fixed precision numbers is constant.

## Binary scientific notation

A binary number in the scientific notation is written in the following form:

$$m \cdot 2^p.$$

Examples:

* $101101.101_2 = 1\cdot2^5+0\cdot2^4+1\cdot2^3+1\cdot2^2+0\cdot2^1+1\cdot2^0+1\cdot2^{-1}+0\cdot2^{-2}+1\cdot2^{-3}=45.625$

* $0.2_{10} = $