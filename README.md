# bclibs

Mathematical functions for the GNU bc command-line calculator.

## General functions

The functions below depend on the bult-in sine, cosine, exponential and
logarithmic functions, so execute ``bc`` with the ``-l`` option. To add
functions simply add them to the command line when you run ``bc``. For
example,

  bc -l trigonometry.bc exponential.bc

### trigonometry.bc

Standard trigonometric functions.

* ``sin(x)``: sine of ``x``.
* ``cos(x)``: cosine of ``x``.
* ``tan(x)``: tangent of ``x``.
* ``sec(x)``: secant of ``x``.
* ``csc(x)``: cosecant of ``x``.
* ``cot(x)``: cotangent of ``x``.
* ``asin(x)``: arc sine of ``x``.
* ``acos(x)``: arc cosine of ``x``.
* ``atan(x)``: arc tangent of ``x``, in the interval (-π/2 rad, π/2 rad).
* ``atan2(x, y)``: arc tangent of ``y/x``, in the interval (-π rad, π rad).
* ``asec(x)``: arc secant of ``x``.
* ``acsc(x)``: arc cosecant of ``x``.
* ``acot(x)``: arc cotangent of ``x``.

### exponential.bc

Exponentials, logarithms, powers and hyperbolic functions.

* ``exp(x)``: exponential of ``x``.
* ``pow(x, y)``: ``x`` to the power of ``y``, for real numbers ``x`` and ``y``.
* ``log(x)``: natural logarithm of ``x``.
* ``log10(x)``: base 10 logarithm of ``x``.
* ``loga(x, a)``: base ``a`` logarithm of ``x``.
* ``sinh(x)``: hyperbolic sine of ``x``.
* ``cosh(x)``: hyperbolic cosine of ``x``.
* ``tanh(x)``: hyperbolic tangent of ``x``.
* ``sech(x)``: hyperbolic secant of ``x``.
* ``csch(x)``: hyperbolic cosecant of ``x``.
* ``coth(x)``: hyperbolic cotangent of ``x``.
* ``asinh(x)``: hyperbolic arc sine of ``x``.
* ``acosh(x)``: hyperbolic arc cosine of ``x``.
* ``atanh(x)``: hyperbolic arc tangent of ``x``.
* ``asech(x)``: hyperbolic arc secant of ``x``.
* ``acsch(x)``: hyperbolic arc cosecant of ``x``.
* ``acoth(x)``: hyperbolic arc cotangent of ``x``.

### complex.bc

Complex number arithmetic.

Represent a complex number *a* + *b*i with an array,

```
z[0] = a; z[1] = b;
```

``bc`` cannot return arrays from a function, so the return variable is given to
the function as an argument when it is a complex number. Supress output with
the dot dummy variable (e.g. ``. = printz(z[]);``).

* ``printz(z[])``: print ``z[]`` in rectangular form ``a + bi``.
* ``printzt(z[])``: print ``z[]`` in trigonometric form ``mod(z[]) * (cos(arg(z[])) + i sin(arg(z[])))``.
* ``re(z[])``, ``im(z[])``: real and imaginary part of ``z[]``.
* ``modz(z[])``: modulus of ``z[]``.
* ``argz(z[])``: principal value of the argument of ``z[]``.
* ``conj(z[], zconj[])``: conjugate of ``z[]``, stored in ``zconj[]``.
* ``add(z1[], z2[], z3[])``: add two complex numbers ``z1 + z2 = z3``.
* ``subtz(z1[], z2[], z3[])``: subtract two complex numbers ``z1 - z2 = z3``.
* ``prodz(z1[], z2[], z3[])``: multiply two complex numbers ``z1 z2 = z3``.
* ``divz(z1[], z2[], z3[])``: divide ``z1[]`` by ``z2[]``, ``z1/z2 = z3``.
* ``powz(z[], x, zpowx[])``: ``z[]`` to the power of ``x``, with real ``x``, ``z1^x = zpowx``.
``z^(1/n)`` calculates the first nth root, to obtain the remaining roots simply multiply by
``exp(2*k*pi/n)``, with ``k = 1, 2, 3, ..., n - 1``.
* ``powzz(z1[], z2[], z1powz2[])``: ``z1[]`` to the power of ``z2[]`` with complex z1 and z2,
stored in the variable ``z1powz2[]``.
* ``rootsz(z[], n)``: print the ``n`` nth roots of complex number ``z[]`` (integer ``n``).
* ``expz(z[], exp_z[])``: exponential of complex number ``z[]``, ``e^z = exp_z``.
* ``logz(z[], log_z[])``: principal value of the logarithm of ``z[]``, ``log(z) = log_z``.
* ``sinz(z[], sin_z[])``, ``cosz(z[], cos_z[])``, ``tanz(z[], tan_z[])``: sine, cosine and tangent
of ``z[]``, stored in the ``sin_z[]``, ``cos_z[]`` and ``tan_z[]`` variables, respectively.
* ``sinhz(z[], sinh_z[])``, ``coshz(z[], cosh_z[])``, ``tanhz(z[], tanh_z[])``: sine, cosine and tangent
of ``z[]``, stored in the ``sinh_z[]``, ``cosh_z[]`` and ``tanh_z[]`` variables, respectively.

### calculus.bc

Simple numerical derivatives and integrals. Set ``generic_f`` equal to the
function of interest before calculating derivatives or integrals. For example,
to calculate the derivative of ``x^2`` at ``x = 1`` with step size 0.01:

```
define generic_f(x) { return x^2; } diff(1, 0.01);
```

If you wish to do several operations with the same generic function, you do
not need to redefine it again. Here is an example to compare the precision of
Euler's integration algorithm to Simpson's:

```
define generic_f(x) { return x^2; } eul = integral(0, 1, 0.001);
sim = simpson(0, 1, 0.001);
print "Error:\n  Euler = ", 3*(1/3.0 - eul), " %\n  Simpson = ", 3*(1/3.0 - sim), " %\n";
```

* ``diff(x, dx)``: Derivative of ``generic_f`` at point ``x`` with numerical
step size ``dx``.
* ``diffn(x, dx)``: Nth derivative of ``generic_f`` at point ``x`` with
numerical step size ``dx``.
* ``integral(a, b, dx)``: Integral of ``generic_f`` from ``a`` to ``b`` with
numerical step size ``dx`` using Euler's algorithm.
* ``simpson(a, b, dx)``: Integral of ``generic_f`` from ``a`` to ``b`` with 
numerical step size ``dx`` using Simpson's algorithm.
