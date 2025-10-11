# Vanice

To distribute name, primary key and arbitrary data, there will be 3 types of messages (CREATE, SET, TOMBSTONE). That can be reduced into a CRDT state.

## Messages

- CREATE
- SET
- TOMBSTONE

### Create Message

```Typescript
type CreateMessage = {
  primaryKey: PrimaryKey
  name: Name
  type: "CREATE"
  hash: Hash
  signature: Signature
}
```
```
VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03
Vanice
```
```JSON
{
  "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
  "name": "Vanice",
  "type": "CREATE",
  "hash": "b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5",
  "signature": "3ce0d64d9d4d45a71861959221a42f094b97c9e653bbea3fffb6823b32b0850d67dccbb4542034ebfcd832675d09af732e4214842eb3b41e1b6c607e1d4373fe"
}
```

### Set Message

```Typescript
type SetMessage = {
  primaryKey: PrimaryKey
  name: Name
  previousHash: Hash
  type: "SET"
  hash: Hash
  signature: Signature
}
```
```
VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03
Vanice
b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5
SET
any text 
https://vanice.cloud/
line 3
```
```JSON
{
  "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
  "name": "Vanice",
  "previousHash": "b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5",
  "type": "SET",
  "body": "any text\nhttps://vanice.cloud/\nline 3\n",
  "hash": "f968c6a46b3d872e0e94bbda1413fe749dd197e4d76499632006efee39963892",
  "signature": "b3fc98fc7f07405e5ee40faa1fe946a633905dc75862f5cae635d1749032ffc56aae72ea9d0aea5ef7de9621a185f45f1821e2f23791e1f89572a8129bc21889"
}
```

### Tombstone Message
```Typescript
type TombstoneMessage = {
  primaryKey: PrimaryKey
  name: Name
  previousHash: Hash
  type: "TOMBSTONE"
  hash: Hash
  signature: Signature
}
```
```
VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03
Vanice
f968c6a46b3d872e0e94bbda1413fe749dd197e4d76499632006efee39963892
TOMBSTONE
```
```JSON
{
  "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
  "name": "Vanice",
  "previousHash": "f968c6a46b3d872e0e94bbda1413fe749dd197e4d76499632006efee39963892",
  "type": "TOMBSTONE",
  "hash": "d8608d2cd3d081bc62dbee4565967421138f167a0e4dc02c42e4afa3d2f118b7",
  "signature": "4dd230e2bb8d5cbda022ccdf3cc5fc96430bf5a1c20998efd7e4687fb4740f373978a45d0859f0b712e70fb0e167c50fe516026728e4127566e2b06306316918"
}
```

### Reduced State Object

```JSON
{
  "publicKey": [
      3, 226, 170,  22,  57, 214,  30, 162,
     13,  44,  29, 187, 157, 180,  29,  46,
    119,  22, 159, 168,   7,  69,  26, 215,
    176, 245, 217,  61, 113,   6, 168, 135,
     86
  ],
  "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
  "name": "Vanice",
  "fingerprint": [
    13, 28, 27, 26, 18,  3,  8,  5, 13, 19, 21,
     5, 23, 21,  3, 26, 24, 29, 18, 14, 16, 29,
    15,  5,  4, 30,  9, 27, 16, 12, 24, 13, 19,
    25, 21, 28,  7, 12, 15, 27, 16, 26, 26,  6,
    13, 17, 19,  3, 26, 29, 19,  0
  ],
  "fingerprintDisplay": "🌙🌸☔️🎄🔑❤️☃️⭐🌙👑💡⭐☕️💡❤️🎄🚀🦋🔑⚡️🎁🦋🔥⭐💪☁️🏁☔️🎁🚗🚀🌙👑☀️💡🌸🙏🚗🔥☔️🎁🎄🎄👍🌙🏠👑❤️🎄🦋👑😀",
  "tombstone": true,
  "messages": [
    {
      "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
      "name": "Vanice",
      "type": "CREATE",
      "hash": "b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5",
      "signature": "3ce0d64d9d4d45a71861959221a42f094b97c9e653bbea3fffb6823b32b0850d67dccbb4542034ebfcd832675d09af732e4214842eb3b41e1b6c607e1d4373fe"
    },
    {
      "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
      "name": "Vanice",
      "previousHash": "b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5",
      "type": "SET",
      "body": "any text\nhttps://vanice.cloud/\nline 3\n",
      "hash": "f968c6a46b3d872e0e94bbda1413fe749dd197e4d76499632006efee39963892",
      "signature": "b3fc98fc7f07405e5ee40faa1fe946a633905dc75862f5cae635d1749032ffc56aae72ea9d0aea5ef7de9621a185f45f1821e2f23791e1f89572a8129bc21889"
    },
    {
      "primaryKey": "VAN1CEEP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03",
      "name": "Vanice",
      "previousHash": "f968c6a46b3d872e0e94bbda1413fe749dd197e4d76499632006efee39963892",
      "type": "TOMBSTONE",
      "hash": "d8608d2cd3d081bc62dbee4565967421138f167a0e4dc02c42e4afa3d2f118b7",
      "signature": "4dd230e2bb8d5cbda022ccdf3cc5fc96430bf5a1c20998efd7e4687fb4740f373978a45d0859f0b712e70fb0e167c50fe516026728e4127566e2b06306316918"
    }
  ]
}
```