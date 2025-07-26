# ModInt

A modular arithmetic template library for competitive programming. Supports both fixed modulus and dynamic modulus operations.

## Features
- Fixed modulus arithmetic with `ModInt<P>` and `ModInt64<P>`
- Dynamic modulus arithmetic with `DynModInt<Id>`
- All basic arithmetic operations (+, -, *, /)
- Modular inverse calculation
- Comparison operators
- I/O stream operators

## Usage Examples

```cpp
#include "ModInt.cpp"

void example() {
    // Fixed modulus example (MOD = 1000000007)
    using Mint = ModInt<MOD>;  // or use the predefined alias 'Z'
    
    // Basic operations
    Mint a = 5;
    Mint b = 3;
    
    // Arithmetic
    Mint sum = a + b;      // 8
    Mint diff = a - b;     // 2
    Mint prod = a * b;     // 15
    Mint quot = a / b;     // 5 * b^(-1) mod MOD
    
    // Compound assignments
    a += b;                // a = 8
    a -= b;                // a = 5
    a *= b;                // a = 15
    a /= b;                // a = 5
    
    // Input/Output
    std::cout << sum << "\n";  // prints the value directly
    std::cin >> a;             // reads value into a ModInt
    
    // Powers using the power function
    Mint p = power(a, 3);  // a^3
    
    // Dynamic modulus example
    using DMint = DynModInt<0>;  // 0 is the Id, can be any unique number
    
    // Set the modulus for this type
    DMint::setMod(998244353);
    
    DMint x = 10;
    DMint y = 3;
    
    DMint res = x * y;     // multiplication modulo 998244353
    DMint inv = y.inv();   // multiplicative inverse of y
    
    // Comparing values
    bool eq = (x == y);    // false
    auto cmp = (x <=> y);  // std::strong_ordering
}

// Example: Computing large factorial modulo M
Mint factorial(int n) {
    Mint result = 1;
    for(int i = 1; i <= n; i++) {
        result *= i;
    }
    return result;
}

// Example: Computing modular exponentiation
Mint power_mod(Mint base, long long exp) {
    return power(base, exp);
}

// Example: Computing binomial coefficients
Mint nCr(int n, int r) {
    if (r > n) return 0;
    Mint num = 1;
    Mint den = 1;
    for(int i = 0; i < r; i++) {
        num *= (n - i);
        den *= (i + 1);
    }
    return num / den;
}
```

## Time Complexity
- All basic arithmetic operations: O(1)
- Modular inverse: O(log M) where M is the modulus
- Power function: O(log N) where N is the exponent

## Space Complexity
- O(1) per ModInt instance

## Notes
- All operations are constexpr-enabled for compile-time evaluation
- The fixed modulus version uses template parameters for better optimization
- The dynamic modulus version uses Barrett reduction for fast multiplication
- Supports both signed and unsigned input values
- Automatically handles negative values in modular arithmetic

## Common Moduli
```cpp
const int MOD = 1000000007;  // 1e9 + 7
const int mod = 998244353;   // 998244353
```
