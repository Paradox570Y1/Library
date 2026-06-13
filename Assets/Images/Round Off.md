In C++, you can round numbers using several methods depending on your specific requirements. Here are some common techniques:

### 1. Rounding to the Nearest Integer

You can use the `std::round()` function provided in the `<cmath>` header to round a floating-point number to the nearest integer.

cpp

Copy code

`#include <iostream> #include <cmath>  int main() {     double value = 5.65;     double roundedValue = std::round(value);     std::cout << roundedValue << std::endl; // Outputs 6     return 0; }`

### 2. Rounding Down (Floor)

To always round down to the nearest integer, you can use the `std::floor()` function.

cpp

Copy code

`#include <iostream> #include <cmath>  int main() {     double value = 5.65;     double roundedValue = std::floor(value);     std::cout << roundedValue << std::endl; // Outputs 5     return 0; }`

### 3. Rounding Up (Ceiling)

To always round up to the nearest integer, you can use the `std::ceil()` function.

cpp

Copy code

`#include <iostream> #include <cmath>  int main() {     double value = 5.65;     double roundedValue = std::ceil(value);     std::cout << roundedValue << std::endl; // Outputs 6     return 0; }`

### 4. Rounding to a Specific Number of Decimal Places

To round to a specific number of decimal places, you can create a custom function.

cpp

Copy code

`#include <iostream> #include <cmath>  double roundToDecimalPlaces(double value, int decimalPlaces) {     double scale = std::pow(10.0, decimalPlaces);     return std::round(value * scale) / scale; }  int main() {     double value = 5.6567;     double roundedValue = roundToDecimalPlaces(value, 2);     std::cout << roundedValue << std::endl; // Outputs 5.66     return 0; }`

### 5. Rounding Using `std::fixed` and `std::setprecision`

For rounding and formatting output, you can use `std::fixed` and `std::setprecision` from the `<iomanip>` header.

cpp

Copy code

`#include <iostream> #include <iomanip>  int main() {     double value = 5.6567;     std::cout << std::fixed << std::setprecision(2) << value << std::endl; // Outputs 5.66     return 0; }`

### Summary

- Use `std::round()` to round to the nearest integer.
- Use `std::floor()` to round down.
- Use `std::ceil()` to round up.
- Use a custom function to round to a specific number of decimal places.
- Use `std::fixed` and `std::setprecision` for rounding and formatting output.