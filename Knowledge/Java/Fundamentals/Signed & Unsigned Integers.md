
# Focus on Binary Storage and Signed vs. Unsigned Numbers

Numbers are stored in memory using a binary system in the form of index based data structure. Each cell can contain a binary digit, `0` and `1` . The memory is like a grid of cells. Each cell does contain a binary digit, as one bit is roughly equivalent to `1`  and an empty cell in the memory signifies `0` . A single binary digit can only hold two possible values: a `0` and a `1` .

Multiple bits held together can hold multiple permutations — 2 bits can hold 4 possible values, 3 can hold 8, and so on. For instance, the maximum number 8 bits can hold (`11111111` in binary) is `255` in the decimal system. So, the numbers from `0`  to `255` can fit within 8 bits.

It is all good, but this way, we can only host positive numbers (or **Unsigned integers**). They are called _unsigned integers_. Unsigned integers are whole number values that are all positive and do not attribute to negative values. For this very reason, we would ask one of the 8 bits to hold information about the sign of the number (**positive** or **negative**). This leaves us with just 7 bits to actually count out a number. The maximum number that these 7 bits can hold ( `1111111` ) is `127` in the decimal system.

Altogether, using this method, 8 bits can hold numbers ranging from `-128`  to `127`  (including zero) — a total of `256` numbers. Not a bad pay-off one might presume. The opposite to an unsigned integer is a **_signed integer_** that have the capability of holding both positive and negative values.

But, what about larger numbers. You would need significantly more bits to hold larger numbers. That's where Java's numeric types come into play. Java has multiple numeric types — their size dependent on the number of bits that are at play.

In Java, numbers are dealt with using data types specially formulated to host numeric data. But before we dive into these types, we must first set some concepts in stone. Just like you did in high school (or even primary school), numbers in Java are placed in clearly distinct groups and systems. As you'd already know by now, number systems includes groups like the _integer_ numbers (`0, 1, 2 ... ∞` ); _negative integers_ ( `0, -1, -2 ... -∞` ) or even _real_ and _rational_ numbers **value of Pi**, `¾, 0.333~`, etcetera). Java simply tends to place these numbers in two distinct groups, **Integers** (`-∞ ... 0 ... ∞` ) and **floating-point** numbers (any number with decimal points or fractional representation). For the moment, we would only look into integer values as they are easier to understand and work with.

## 2’s complement of a Binary number
2’s complement of a binary number is 1 added to the 1’s complement of the binary number. Note that 1’s complement is simply flip of given binary number.

There are two sorts of Binary numbers complement 1's complement and 2's complement. Invert the supplied integer to get the 1's complement of a binary number. The 1's complement of the binary number `110010` , for example, is `001101` . To acquire the 2's complement of a binary number, add 1 to the least significant bit of the provided value (LSB). For example, the binary number ( `110010` ) 2's complement is ( `001101` ) + `1` = `001110` .

### Why do we use 2's complement over 1's complement ?

The **main difference** between `1′ s complement`  and `2′ s complement`  is that 1′ s complement has two representations of `0 (zero)` .

1. `00000000` : which is positive zero`(+0)` and
2. `11111111` : which is negative zero `(-0)`

Whereas in 2′ s complement, there is only one representation for zero — `00000000 (0)` because if we add `1` to `11111111 (-1)` , we get `100000000` , which is nine bits long. Since only eight bits are allowed, the left-most bit is discarded(or overflowed), leaving `00000000 (-0)` which is the same as positive zero. This is the reason why 2′ s complement is generally used.
