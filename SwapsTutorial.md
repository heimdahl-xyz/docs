
# Heimdahl.xyz REST API Swaps Tutorial

This tutorial demonstrates how to use our Swaps REST API to retrieve swap data across different blockchains, tokens, and pairs.

## API Endpoint

```
https://api.heimdahl.xyz/v1/swaps/list/{path}
```

**Note**: This API requires authentication using a Bearer token.

## Path Format

The path follows this pattern:

```
{chain}.{network}.{token1}.{token2}.all
```

Where:
- `chain`: Blockchain (ethereum, polygon, base, binance, solana, arbitrum, tron)
- `network`: Network type (mainnet, testnet, etc.)
- `token1`: First token symbol (USDC, USDT, WETH, etc.)
- `token2`: Second token symbol (USDC, USDT, WETH, etc.)
- The final parameter is `all`, reserved for size bucket filtering (not currently active).

## Example Usage

### Basic curl command

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/swaps/list/{path}?page=0&pageSize=2"
```

### Example Query

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/swaps/list/all.mainnet.usdc.weth.all?page=0&pageSize=2" | jq
```

## Response Format

The API returns swap data in JSON array format. Each swap entry contains:

```json
[
  {
    "chain_name": "ethereum",
    "tx_hash": "0x3e78165e95accac994192c573fc3e34a93b79fe101fde33a1dd53c2f28e7e44d",
    "timestamp": 1741969405,
    "token1_address": "0x5050e08626c499411B5D0E0b5AF0E83d3fD82EDF",
    "token1_symbol": "USDC",
    "token1_decimals": 6,
    "token2_address": "0x88e6A0c2dDD26FEEb64F039a2c41296FcB3f5640",
    "token2_symbol": "WETH",
    "token2_decimals": 18,
    "token1_sender": "0x5050e08626c499411B5D0E0b5AF0E83d3fD82EDF",
    "token2_sender": "0x88e6A0c2dDD26FEEb64F039a2c41296FcB3f5640",
    "token1_amount": 24957115193,
    "token2_amount": 12947804764536934000,
    "price_token1_in_token2": 1927517107,
    "price_token2_in_token1": 518802139766881000000000000
  },
  {
    "chain_name": "ethereum",
    "tx_hash": "0x8713e0df807c48d9396e5b017f73e896c4502f7d904328c5c556886744c328a4",
    "timestamp": 1741969405,
    "token1_address": "0xA69babEF1cA67A37Ffaf7a485DfFF3382056e78C",
    "token1_symbol": "USDC",
    "token1_decimals": 6,
    "token2_address": "0xE0554a476A092703abdB3Ef35c80e0D76d32939F",
    "token2_symbol": "WETH",
    "token2_decimals": 18,
    "token1_sender": "0xA69babEF1cA67A37Ffaf7a485DfFF3382056e78C",
    "token2_sender": "0xE0554a476A092703abdB3Ef35c80e0D76d32939F",
    "token1_amount": 7309553024,
    "token2_amount": 3794441433022390000,
    "price_token1_in_token2": 1926384463,
    "price_token2_in_token1": 519107176671927460000000000
  }
]
```

### Field Descriptions:

- `chain_name`: Blockchain name
- `tx_hash`: Transaction hash of the swap
- `timestamp`: Unix timestamp of the swap
- `token1_address`: Contract address of the first token
- `token1_symbol`: Symbol of the first token
- `token1_decimals`: Number of decimal places for token1
- `token2_address`: Contract address of the second token
- `token2_symbol`: Symbol of the second token
- `token2_decimals`: Number of decimal places for token2
- `token1_sender`: Address sending token1
- `token2_sender`: Address sending token2
- `token1_amount`: Amount of token1 swapped
- `token2_amount`: Amount of token2 swapped
- `price_token1_in_token2`: Price of token1 denominated in token2 (scaled number)
- `price_token2_in_token1`: Price of token2 denominated in token1 (scaled number)

## Pagination Parameters

- `page`: The page number (starting from 0)
- `pageSize`: Number of results per page

---

For more examples or support, visit [Heimdahl.xyz](https://heimdahl.xyz).
