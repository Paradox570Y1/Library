- The `cmath` library in C++ provides a collection of functions for performing mathematical operations. 
- It is included in the C++ standard library and can be used by including the header `<cmath>`. 
- This library offers functions for a variety of mathematical computations, including basic arithmetic, trigonometry, exponential and logarithmic functions, power functions, and more. Below are some key points and commonly used functions from the `cmath` library:

### Important Functions
- __tgamma()__
	- When you want to calculate the factorial of an integer n, you can use the `tgamma` function by passing n+1 to it, since Γ(n+1)=n!.
	- The `tgamma` function returns a `double` value.
	- The function works for non-integer values as well, making it useful for various mathematical computations beyond just integer factorials.
	- The `tgamma` function is part of the `<cmath>` library, so you need to include this header to use it.
	- For very large values of `n`, the result can be very large, and you may encounter precision or overflow issues depending on the range of the `double` type in your system.

### Commonly Used Functions

Here are some of the commonly used functions available in the `cmath` library:

1. **Trigonometric Functions**
    
    - `double sin(double x)`: Returns the sine of `x` (measured in radians).
    - `double cos(double x)`: Returns the cosine of `x` (measured in radians).
    - `double tan(double x)`: Returns the tangent of `x` (measured in radians).
    - `double asin(double x)`: Returns the arc sine of `x`.
    - `double acos(double x)`: Returns the arc cosine of `x`.
    - `double atan(double x)`: Returns the arc tangent of `x`.
    - `double atan2(double y, double x)`: Returns the arc tangent of `y/x`, considering the signs of both arguments to determine the correct quadrant.
2. **Hyperbolic Functions**
    
    - `double sinh(double x)`: Returns the hyperbolic sine of `x`.
    - `double cosh(double x)`: Returns the hyperbolic cosine of `x`.
    - `double tanh(double x)`: Returns the hyperbolic tangent of `x`.
3. **Exponential and Logarithmic Functions**
    
    - `double exp(double x)`: Returns the value of e raised to the power of `x`.
    - `double log(double x)`: Returns the natural logarithm (base e) of `x`.
    - `double log10(double x)`: Returns the common logarithm (base 10) of `x`.
    - `double sqrt(double x)`: Returns the square root of `x`.
4. **Power Functions**
    
    - `double pow(double base, double exponent)`: Returns the value of `base` raised to the power of `exponent`.
    - `double cbrt(double x)`: Returns the cube root of `x`.
5. **Rounding and Remainder Functions**
    
    - `double ceil(double x)`: Returns the smallest integer value greater than or equal to `x`.
    - `double floor(double x)`: Returns the largest integer value less than or equal to `x`.
    - `double fmod(double x, double y)`: Returns the remainder of the division of `x` by `y`.
6. **Absolute Value and Sign Functions**
    
    - `double fabs(double x)`: Returns the absolute value of `x`.
    - `double abs(double x)`: Also returns the absolute value of `x`.