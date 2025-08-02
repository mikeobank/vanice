# Vanice Registry

## Key / Value

```
{ vanity name }: [
    { 
        key: PrimeKey 
        signature: Schnorr Signature
    }: String
]
```

## Database fields
- key: PrimeKey
- signature: Signature
- vanity_name: VanityName
- content: String
- datetime: Datetime
- tombstone: Boolean?

## API Endpoints

- write key, vanity name + value
- retrieve key (by vanity name + (partial) fingerprint)
- tombstone key

- mine vanity name
  - via XPub, proof for empty XPub
  - how to escrow?

