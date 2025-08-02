# Vanice

A character set and encoding for displaying public keys using an ambiguous alphabet plus an additional emoji set. This allows for concise display of vanity names within public keys with an additional fingerprint. Resulting in the possibility to brute force searching for any desired name.

## Character set
| index | primary | secondary | fingerprint |
| ----- | ----- | --------- | ----- |
| 0 | 0 | Oo_ | 😊 |
| 1 | 1 | IiLl | 🖋️ | 
| 2 | 2 | Zz | 🍴 |
| 3 | 3 | | ❤️ |
| 4 | 4 | | 💪 |
| 5 | 5 | | ⭐ |
| 6 | 6 | | 👍 |
| 7 | 7 | | 🙏 |
| 8 | 8 | | ☃️ |
| 9 | 9 | | 🏁 |
| 10 | A | a | ✈️ |
| 11 | B | b | ⚽ |
| 12 | C | c | 🚗 |
| 13 | D | d | 🌙 |
| 14 | E | e | ⚡ |
| 15 | F | f | 🔥 |
| 16 | G | g | 🎁 |
| 17 | H | h | 🏠 |
| 18 | J | j | 🔑 |
| 19 | K | k | 👑 |
| 20 | M | m | 🎵 |
| 21 | N | n | 💡 |
| 22 | P | p | 🎉 |
| 23 | Q | q | ☕ |
| 24 | R | r | 🚀 |
| 25 | S | s | ☀️ |
| 26 | T | t | 🌲 |
| 27 | U | u | ☂️ |
| 28 | V | v | 🌸 |
| 29 | W | w | 🦋 |
| 30 | X | x | ☁️ |
| 31 | Y | y | ⏰ |

## Computation
- Convert vanity name to primary name
- Generate Schnorr key pair
- Encode public key to primary key using base 32 primary characters (the sign bit (0x02 or 0x03) is moved to the end)
- Check if primary key starts with primary name
#### When a match is found:
- SHA256 digest primary key (hash)
- Encode hash to base 32 fingerprint 
- Append the first n emojis to the vanity name (n = 10 - length(vanity name), minimum 3)

## Example

```
vanity name: Vani
private key: Uint8Array(32) [
  111, 177,  9,   3, 170, 166,  77, 168,
  121,  97, 98, 136, 231, 146, 199,   4,
   48,  64, 75, 188,  12, 241,   2,  21,
  196, 144, 56, 255, 255,  53,  50,  52
]
public key: Uint8Array(33) [
    3, 226, 170,  21, 111,  84,  61, 196,
  160,  73, 204, 193,  18, 122, 107,  67,
   50,  69, 162,  29,  41, 221,  14, 199,
  218, 138, 161, 233, 158,  16, 104, 190,
   94
]
primary key: VAN1AUTM7Q2A0JECR497MTT3692T4799UM7CFPMAM7MSV438QSF03
fingerprinted name: Vani✈️⚡👍☁️🎵🙏
```

## Calculations

Calculations
------------
| length | base32 | 1 of n |
| ------ | ------ | ------ |
| 1      | 32<sup>1</sup> | 32
| 2      | 32<sup>2</sup> | 1_024
| 3      | 32<sup>3</sup> | 32_768
| 4      | 32<sup>4</sup> | 1_048_576
| 5      | 32<sup>5</sup> | 33_554_432
| 6      | 32<sup>6</sup> | 1_073_741_824
| 7      | 32<sup>7</sup> | 34_359_738_368
| 8      | 32<sup>8</sup> | 1_099_511_627_776
| 9      | 32<sup>9</sup> | 35_184_372_088_832
| 10     | 32<sup>10</sup> | 1_125_899_906_842_624
| 11     | 32<sup>11</sup> | 36_028_797_018_963_970
| 12     | 32<sup>12</sup> | 1_152_921_504_606_847_000
| 13     | 32<sup>13</sup> | 3.69e19
| 14     | 32<sup>14</sup> | 1.18e21
| 15     | 32<sup>15</sup> | 3.78e22
| 16     | 32<sup>16</sup> | 1.21e24

## Outsource searching

When using XPubs derived from a seed, it's possible to outsource the searching of vanity names without having to reveal the seed. 2,147,483,648 public keys can be derived per single XPub. And also 2,147,483,648 XPubs can be created from a single seed. That means on average one XPub will reveal any 6-letter name, and a single seed could contain any 12-letter name.

## To be decided
- Final character set
- Final emoji set, plus order (indices)
- Recommended length of fingerprint / total length (vanity name + fingerprint)
- Registry. Preferably distributed, decentralized.
