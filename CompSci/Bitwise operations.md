[Bithacks](https://graphics.stanford.edu/~seander/bithacks.html) is a great resource.

# Left Shift
`<<` operator in Java moves all `x` bits `y` places to the left. For example:

`1 << 5` == 32, where in binary:

`00000001 << 5` == `00100000`

### How can you quickly compute $2^x$?

Left shift by `x`: `1 << x`

### Compute `0110` + `0110`

This is equivalent to $0110 * 2$ which is equal to `0110 << 1` = `1100`

# Negate

This is the `~` operator, e.g. `~0110`.

A number `XOR` it's negated value is always `1`, so `1011 ^ (~1011)` = `1111`  .

`~0` is a sequence of `1`s, so `~0 << 2 ` = `...11111100`.

`~(1 << 5)` = `~(00100000)` = `11011111`

# Tricks

`x ^ 0s` = `x`
`x & 0s` = `0`
`x | 0s` = `x`

`x ^ 1s` = `~x`
`x & 1s` = `x`
`x | 1s` = `1s`

`x ^ x` = `0`
`x & x` = `x`
`x | x` = `x`

# XOR

$a \oplus a \oplus b = 0 \oplus b = b$

# Two's Complement
Numbers are represented as positive or negative using a sign bit. A two's complement is the "opposite" number when the sign bit is flipped:

| Positive Values | Negative Values |
| - | - |
| 7 -> 0111 | -1 -> 1111 |
| 6 -> 0110 | -2 -> 1110 |
| 5 -> 0101 | -3 -> 1101 |
| 4 -> 0100 | -4 -> 1100 |
| 3 -> 0011 | -5 -> 1011 |
| 2 -> 0010 | -6 -> 1010 |
| 1 -> 0001 | -7 -> 1001 |
| 0 -> 0000 |  |

Notice how the left and right side always sum to $2^3$.

The binary representation of `-K` as an N-bit number is $concat(1, 2^{N-1} - K)$. 

Note that a sequence of all `1`s is equal to -1.