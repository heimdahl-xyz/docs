# Heimdahl.xyz REST API Transfer Tutorial

This tutorial demonstrates how to use our Transfers REST API to retrieve token transfer data across different blockchains, networks, and addresses.

## API Endpoint

```
https://api.heimdahl.xyz/v1/transfers/list/{path}
```

**Note**: This API requires authentication using a Bearer token.

## Path Format

The path follows one of these two patterns:

1. `{chain}.{network}.{token}.{from}.{to}.all`
2. `{chain}.{network}.{token}.{address}.all.all`

Where:
- `chain`: Blockchain (ethereum, polygon, base, binance, solana, arbitrum, tron)
- `network`: Network type (mainnet, testnet, goerli, etc.)
- `token`: Token symbol (USDT, USDC, WETH, etc.)
- `from`: Sender address (0x...)
- `to`: Recipient address (0x...)
- `address`: Single address to query (either as sender or receiver)
- The final parameter is currently set to `all` which is reserved for filter by amount bucket it belogns to (small, large or whale depending on particular tokens circulating supply)

## Example Usage

### Basic curl command

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/{path}"
```

### Examples by Chain and Token

#### USDC Examples

##### Ethereum

```bash
# Get all USDC transfers from a specific address on Ethereum mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/ethereum.mainnet.usdc.0xA89531c33C4DC46C8Eb0E2f0B16B70b204F3C657.all.all" | jq

# Get USDC transfers between two addresses on Ethereum mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/ethereum.mainnet.usdc.0xA89531c33C4DC46C8Eb0E2f0B16B70b204F3C657.0xB8c77482e45F1F44dE1745F52C74426C631bDD52.all" | jq
```

##### Polygon

```bash
# Get all USDC transfers from a specific address on Polygon mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/polygon.mainnet.usdc.0x7ceb23fd6bc0add59e62ac25578270cff1b9f619.all.all" | jq

# Get all USDC transfers between two addresses on Polygon mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/polygon.mainnet.usdc.0x7ceb23fd6bc0add59e62ac25578270cff1b9f619.0x2791bca1f2de4661ed88a30c99a7a9449aa84174.all" | jq
```

##### Base

```bash
# Get all USDC transfers from a specific address on Base mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/base.mainnet.usdc.0xd9aAEc86B65D86f6A7B5B1b0c42FFA531710b6CA.all.all" | jq
```

##### Arbitrum

```bash
# Get all USDC transfers from a specific address on Arbitrum One
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/arbitrum.one.usdc.0xFd086bC7CD5C481DCC9C85ebE478A1C0b69FCbb9.all.all" | jq
```

#### USDT Examples

##### Ethereum

```bash
# Get all USDT transfers from a specific address on Ethereum mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/ethereum.mainnet.usdt.0xdAC17F958D2ee523a2206206994597C13D831ec7.all.all" | jq

# Get all USDT transfers between two addresses on Ethereum mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/ethereum.mainnet.usdt.0xdAC17F958D2ee523a2206206994597C13D831ec7.0x6B175474E89094C44Da98b954EedeAC495271d0F.all" | jq
```

##### Tron

```bash
# Get all USDT transfers from a specific address on Tron mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/tron.mainnet.usdt.TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t.all.all" | jq
```

#### WETH Examples

##### Ethereum

```bash
# Get all WETH transfers from a specific address on Ethereum mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/ethereum.mainnet.weth.0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2.all.all" | jq

# Get all WETH transfers between two addresses on Ethereum mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/ethereum.mainnet.weth.0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2.0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D.all" | jq
```

##### Binance Smart Chain

```bash
# Get all WETH transfers from a specific address on Binance Smart Chain mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/binance.mainnet.weth.0x2170Ed0880ac9A755fd29B2688956BD959F933F8.all.all" | jq
```

##### Solana

```bash
# Get all USDC transfers from a specific address on Solana mainnet
curl -H "Authorization: Bearer YOUR_API_KEY" "https://api.heimdahl.xyz/v1/transfers/list/solana.mainnet.usdc.EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v.all.all" | jq
```

## Path Format Note

The current version of the API uses `all` for the transfer size bucket parameter:
- All paths end with `.all` to indicate all transfer sizes

## Response Format

The API returns transfer data in JSON format. Each transfer contains the following information:

```json
{
  "timestamp": 1740844573,
  "from_address": "0xEcd7Eef15713997528896Cb5db7ec316Db4C2101",
  "to_address": "0x39F5b252dE249790fAEd0C2F05aBead56D2088e1",
  "amount": 1.29e+18,
  "token_address": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
  "symbol": "WETH",
  "chain": "ethereum",
  "network": "mainnet",
  "tx_hash": "0x54180d7f37159043b2221f22c4479742a32cb86d72a17a6a9efccef3288e1e56",
  "decimals": 18,
  "position": 21953050
}
```

The response includes these key fields:
- `timestamp`: Unix timestamp of the transfer
- `from_address`: Sender address
- `to_address`: Recipient address
- `amount`: Transfer amount (in token units)
- `token_address`: Address of the token contract
- `symbol`: Token symbol (USDC, USDT, WETH, etc.)
- `chain`: Blockchain
- `network`: Network type (mainnet, testnet, etc.)
- `tx_hash`: Transaction hash
- `decimals`: Number of decimal places the token uses
- `position`: Block position
```
