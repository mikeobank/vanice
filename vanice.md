# Vanice

A character set and encoding for displaying public keys using an ambiguous alphabet and additional emoji set. Allowing for concise displaying of vanity names within public keys. And brute force searching for any desired name.

## Character set
| index | prime | secondary | emoji |
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
- convert vanity name to prime name
- generate Schnorr key pair
- encode public key to base32 prime characters (prime key)
- check if prime key starts with prime name
when match found:
- SHA256 digest prime key (hash)
- encode hash to base32 emojis 
- append first n emojis to vanity name (n = 10 - length(vanity name) minimum 3)

## Example

```
private key: Uint8Array(32) [
   23, 230, 166, 137,  45, 132,  95, 107,
  110, 232, 219,  95,  58,  47, 235,   8,
   59, 248, 149, 240, 238, 154, 149,  86,
  120, 206,  94, 134,  24, 228,  20,  32
]
public key: Uint8Array(32) [
  226, 170,  19, 161, 220,  38, 102,
   41, 161, 254, 231, 186,  65,  85,
  195,  44, 151, 243, 241, 155, 236,
   24, 210,  48, 167, 149, 148, 251,
  229,  78, 112,  73
]
VAN178EV4SK2K8FXVXW42NE35JBY7VCUWGCD4C57JPAFQSAEE14G
Vani🚗☀️⭐👍
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
| 15     | 32<sup>15</sup> | 3,78e22
| 16     | 32<sup>16</sup> | 1.21e24

## Outsource searching

When using XPubs derived from a seed, it's possible to outsource the searching of vanity names without having to reveal the seed. 2_147_483_648 public keys can be derived per single XPub. And also 2_147_483_648 XPubs can be created from a single seed. That means on average one XPub will reveal any 6 letter name, and a single seed to contain any 12 letter name.

## To be decided
- final character set
- final emoji set, plus order (indices)
- recommended length of fingerprint / total length (vanity name + fingerprint)
- seperator character between name and fingerprint?