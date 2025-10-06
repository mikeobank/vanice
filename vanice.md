# Vanice

## Decentralized Naming

A way to encode vanity names within public keys. Plus an additional fingerprint encoded with emoji characters. Allowing for unique names, where duplicates (conflicting name + fingerprint pairs) will be exponentialy hard to find (brute force).

### Example
**Vanice☁️☕️❤️☁️**
- primary key: VAN1CEKTGGWMWMRBP2PCBR2MJMGKXMHS709JSVT7HTFTFSCJWN7G2
- fingerprint: ☁️☕️❤️☁️☁️😀👍☀️❤️🙏💡👑🔥☁️🍴☕️🔥🎄👍⭐✒️🙏⭐💪🏁❤️🎁☃️🍴✒️☁️☀️☁️⭐🏠🙏❤️🙏👑😀🔑🌙⭐🔑🔥☕️☁️⏰☁️🌙🎁🎁
- public key (Schnorr): 02e2aa163a7a843b4ed30bb0acc5e05495213f523938132cf3478e9fa7e592ed4f

### Character set
| index | primary | secondary | fingerprint | Unicode codepoint |
| ----- | ------- | --------- | ----------- | ----------------- |
| 0 | 0 | Oo_ | 😀 | U+1F600
| 1 | 1 | IiLl | ✒️ | U+2712
| 2 | 2 | Zz | 🍴 | U+1F374
| 3 | 3 | | ❤️ | U+2764
| 4 | 4 | | 💪 | U+1F4AA
| 5 | 5 | | ⭐ | U+2B50
| 6 | 6 | | 👍 | U+1F44D
| 7 | 7 | | 🙏 | U+1F64F
| 8 | 8 | | ☃️ | U+26C4	
| 9 | 9 | | 🏁 | U+1F3C1
| 10 | A | a | ✈️ | U+2708
| 11 | B | b | ⚽ | U+26BD
| 12 | C | c | 🚗 | U+1F697
| 13 | D | d | 🌙 | U+1F319
| 14 | E | e | ⚡️ | U+26A1	
| 15 | F | f | 🔥 | U+1F525
| 16 | G | g | 🎁 | U+1F381	
| 17 | H | h | 🏠 | U+1F3E0
| 18 | J | j | 🔑 | U+1F511
| 19 | K | k | 👑 | U+1F451
| 20 | M | m | 🎵 | U+1F3B5
| 21 | N | n | 💡 | U+1F4A1	
| 22 | P | p | 🎉 | U+1F389
| 23 | Q | q | ☕️ | U+2615
| 24 | R | r | 🚀 | U+1F680
| 25 | S | s | ☀️ | U+2600
| 26 | T | t | 🎄 | U+1F384
| 27 | U | u | ☔️ | U+2614
| 28 | V | v | 🌸 | U+1F338
| 29 | W | w | 🦋 | U+1F98B
| 30 | X | x | ☁️ | U+2601
| 31 | Y | y | ⏰ | U+23F0	

### Computation
- Convert vanity name to primary name
- Generate key pair (Schnorr)
- Encode public key to primary key using base 32 primary characters (the sign bit (0x02 or 0x03) is moved to the end)
- Check if primary key starts with primary name
**When a match is found**:  

- SHA256 digest public key (hash)
- Encode hash to base 32 fingerprint 
- Append the first n emojis to the vanity name (n = 10 - length(vanity name), minimum 3)

### Difficulty

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

### Outsource mining

When using XPubs derived from a seed, it's possible to outsource the searching of vanity names without having to reveal the seed. 2,147,483,648 public keys can be derived per single XPub. And also 2,147,483,648 XPubs can be created from a single seed. That means on average one XPub will reveal any 6-letter name, and a single seed could contain any 12-letter name.

### To be decided
- Final character set
- Final emoji set, plus order (indices)
- Recommended length of fingerprint / total length (vanity name + fingerprint)
- Should the name or length of name be digested into the fingerprint?
- Allow for ambiguous emojis?
- Registries. Preferably distributed, decentralized. Web, Desktop, iOS, Android.
