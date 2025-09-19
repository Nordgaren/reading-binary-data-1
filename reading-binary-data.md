# Reading Binary Data 1
An upskill challenge focusing on reading and interpreting binary data.

## Why does reading binary data matter?
Binary data, which is data represented with 1's and 0's (a.k.a Base-2), is the foundation for all digital computing. The 
computer software you are using right now, wether it be on your phone, laptop, or desktop, is all stored, read, and written
in binary. Even the letters of this document are stored as a binary encoding, or a number representation, that corresponds
to a letter in the alphabet! While there are a lot of tools out there to help decode and look at binary data in a human
readable format, it is important to understand how it is stored and how it is read. Let's look at some examples, and then
look at how we can convert binary to hexadecimal and back!

Specifically, we use a type of binary number system called "two's complement", which is a system where the most significant
bit is used to indicate whether the number is positive or negative. That means the final bit in the number is 0 for positive
numbers and 1 for negative numbers.

## What is Base-2, Base-10, and Base-16?
Base-2 is a system of representing numbers with only 2 digits, 1 and 0. Represented by a preceding `0b` (`0b1010` == `10`)
Base-10 is a system of representing numbers with only 10 digits, 0 through 9. Represented by a preceding `0d` (`0d10` == `10`)
Base-16 is a system of representing numbers with only 16 digits, 0 through 9 and A through F. Represented by a preceding `0x` (`0xA` == `10`)

Let's look at the first 16 digits of the Hindu-Arabic numeral system, and their corresponding binary and hexadecimal
representations.


|  Dex | Hex | Binary |
|-----:|----:|:------:|
|  0d0 | 0x0 |  0b0   |
|  0d1 | 0x1 |  0b1   |
|  0d2 | 0x2 |  0b10  |
|  0d3 | 0x3 |  0b11  |
|  0d4 | 0x4 | 0b100  |
|  0d5 | 0x5 | 0b101  |
|  0d6 | 0x6 | 0b110  |
|  0d7 | 0x7 | 0b111  |
|  0d8 | 0x8 | 0b1000 |
|  0d9 | 0x9 | 0b1001 |
| 0d10 | 0xA | 0b1010 |
| 0d11 | 0xB | 0b1011 |
| 0d12 | 0xC | 0b1100 |
| 0d13 | 0xD | 0b1101 |
| 0d14 | 0xE | 0b1110 |
| 0d15 | 0xF | 0b1111 |

The numbers in each row are the same, but the binary and hexadecimal representations are represented in different columns.
One thing you may have noticed is that one hexidecimal digit represents 4 bits of binary data perfectly. This will come in
handy later, when we want to convert larger numbers from binary to hexadecimal and back. 4 digits in binary is a "nibble",
where as 8 digits in binary is a byte. That means you can represent a byte with only two hexidecimal digits (At least on 
most modern CPUs)!

## Ascii
Ascii is the `American Standard Code for Information Interchange`. Ascii is also the base of UTF-8 (IDK if that's historically
accurate, the AI just told me when I asked about the backwards compatibility). There is an interesting pattern in the letters 
of the alphabet.

### Standard ASCII Table letters [A-Fa-f]
... 0x0 - 0x40 skipped ...

| Hex | Dec | Binary     |  Char   | Description                     |
|----:|----:|:-----------|:-------:|:--------------------------------|
|  41 |  65 | `01000001` |   `A`   | Uppercase letter A              |
|  42 |  66 | `01000010` |   `B`   | Uppercase letter B              |
|  43 |  67 | `01000011` |   `C`   | Uppercase letter C              |
|  44 |  68 | `01000100` |   `D`   | Uppercase letter D              |
|  45 |  69 | `01000101` |   `E`   | Uppercase letter E              |
|  46 |  70 | `01000110` |   `F`   | Uppercase letter F              |

... 0x47-0x60 skipped ...

| Hex | Dec | Binary     |  Char   | Description                     |
|----:|----:|:-----------|:-------:|:--------------------------------|
|  61 |  97 | `01100001` |   `a`   | Lowercase letter a              |
|  62 |  98 | `01100010` |   `b`   | Lowercase letter b              |
|  63 |  99 | `01100011` |   `c`   | Lowercase letter c              |
|  64 | 100 | `01100100` |   `d`   | Lowercase letter d              |
|  65 | 101 | `01100101` |   `e`   | Lowercase letter e              |
|  66 | 102 | `01100110` |   `f`   | Lowercase letter f              |

If you notice, the 5th bit:  
![B binart.png](https://github.com/Nordgaren/reading-binary-data-1/blob/main/B%20binart.png?raw=true)

Bit 5 is set for lowercase letters, and not set for uppercase ones. You may see bitwise operations setting and testing this
bit in particular on ASCII and UTF-8 strings. Especially when doing case-insensitive comparisons. 

### Standard ASCII Table letters [U-Zu-z]
... 0x0 - 0x54 skipped ...

| Hex | Dec | Binary | Char | Description |
|---:|---:|:---|:----:|:------------|
| 55 | 85 | `01010101` | `U` | Uppercase letter U |
| 56 | 86 | `01010110` | `V` | Uppercase letter V |
| 57 | 87 | `01010111` | `W` | Uppercase letter W |
| 58 | 88 | `01011000` | `X` | Uppercase letter X |
| 59 | 89 | `01011001` | `Y` | Uppercase letter Y |
| 5A | 90 | `01011010` | `Z` | Uppercase letter Z |

... 0x5B - 0x74 skipped ...

| Hex | Dec | Binary | Char | Description |
|---:|---:|:---|:----:|:------------|
| 75 | 117 | `01110101` | `u` | Lowercase letter u |
| 76 | 118 | `01110110` | `v` | Lowercase letter v |
| 77 | 119 | `01110111` | `w` | Lowercase letter w |
| 78 | 120 | `01111000` | `x` | Lowercase letter x |
| 79 | 121 | `01111001` | `y` | Lowercase letter y |
| 7A | 122 | `01111010` | `z` | Lowercase letter z |

## Windows error codes
Let's look at another encoding system, this time with HRESULT, or modern Windows error codes. These articles disagree on
the naming, despite being 9 months apart. It's clear from both articles that there are bits at the top end of the number 
that are used to indicate what kind of error, and more info about where/how it originated. Also suprising to see that the 
last bit always indicates success or not. This is interesting because of "two's complement" binary guaranteeing that
the most significant bit is always 0 for positive numbers, and 1 for negative numbers. We can then test of the status is 
less than 0 to see if all we are worried about is whether it was successful! We can also still output more info in the status
code, even if it was a success.

02/02/21
https://learn.microsoft.com/en-us/windows/win32/com/structure-of-com-error-codes

11/16/21
https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a

![Windows Error Code Bits.png](https://github.com/Nordgaren/reading-binary-data-1/blob/main/Windows%20Error%20Code%20Bits.png?raw=true)

## Binary to Decimal and back
Okay, so now we get to the technique. It's quite simple, actually. When you have a binary number, you just need to add the
value of the exponent for each bit that is set. 

![Binary Exponents.png](https://github.com/Nordgaren/reading-binary-data-1/blob/main/Binary%20Exponents.png?raw=true)

So for our example of `B` up above, aka `0b01000010`, we can see that we add 64 and 2, and get the decimal value of 66. If
we want to go back, we can just subtract the highest power of 2 that is less than or equal to the decimal value. For example,
`0d119` we can subtract 64 (55), which means the 7th bit is set, then we subtract 32 from 55, then we subtract 16 from 23 (7),
we can't subtract 8 from 7, so we get the next highest number we can subtract, which is 4 (3). Then we can subtract 3 (1),
and we can end by subtracting 1, which leaves us with `01110111` or `w`. This can be done for any size number, but the more
bytes you add, the harder the math. Hex is similar, but you can give me any set of bytes in binary and I can convert it to
hex in my head, no problem! Here's how!

## Binary to Hexadecimal and back!
So, hexadecimal is actually much simpler to convert to binary and back. Just like decimal, you can add the value of the exponent,
but you only have to worry about one "nibble," aka four bits, at a time!

You might just notice the pattern, here:
![Binary Exponents Hex.png](https://github.com/Nordgaren/reading-binary-data-1/blob/main/Binary%20Exponents%20Hex.png?raw=true)

But we can look at this even simple than that!
![Binary Exponents Hex simplified.png](https://github.com/Nordgaren/reading-binary-data-1/blob/main/Binary%20Exponents%20Hex%20simplified.png?raw=true)

So, let's look at a 4 byte number:`1011111011101111`.

From left to right, let's look at it four bits, or a "nibble" at a time!
> `1011`: We have 8 + 0 + 2 + 1 -> B  
> `1110`: We have 8 + 4 + 2 + 0 -> E  
> `1110`: We have 8 + 4 + 2 + 0 -> E  
> `1111`: We have 8 + 4 + 2 + 1 -> F  

Now everyones favorite hexadecimal number `11011110101011011011111011101111`
> `1101`: We have 8 + 4 + 0 + 1 -> D  
> `1110`: We have 8 + 4 + 2 + 0 -> E  
> `1010`: We have 8 + 0 + 2 + 0 -> A  
> `1101`: We have 8 + 4 + 0 + 1 -> D  
> `1011`: We have 8 + 0 + 2 + 1 -> B  
> `1110`: We have 8 + 4 + 2 + 0 -> E  
> `1110`: We have 8 + 4 + 2 + 0 -> E  
> `1111`: We have 8 + 4 + 2 + 1 -> F  

## Challenge
Convert this MD5 hash from binary to hexadecimal. That is your flag. It is the exact number you get from converting this 
hexadecimal, and there is no other conversions here (ASCI text, etc.)
`11011111100010010011111000100111011101111011100100101011010000010101010011000001111010010010101101000011110110010001001101100001`

Turn it format: `flag{8e7438bd0182ce6b3dc8f72eab27dd6a}`


