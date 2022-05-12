<img src="https://hv4gxzchk24cqfezebn3ujjz6oy2kbtztv5vghn6kpbkjc3vg4rq.arweave.net/j4aZoqGl_74nkEfO7bZabRkat6NS88g1HQcO3OJmlMQ">
<h1 align="center">Project ArLink 🔗</h1>
<p align="center">A tag specification for linking Arweave wallets to other cryptocurrency wallets</p>

## User-Interface

You can find a UI for ArLink on the [Arweave Permaweb](https://arweave.net/CodqSDWXY5CALyMf9oFLCtTDRYdW4lV9X9O7j-73g1U) or at [arlink.tateberenbaum.com](https://arlink.tateberenbaum.com).

## Why?........

I created ArLink with the intentions of establishing a way to get a user's Ethereum wallet address from the Arweave. By having Arweave users link their accounts to other blockchains, profit-sharing communities can choose to pay out users in other cryptocurrencies not on the *weave*.

## Tag Specification

See [this](https://viewblock.io/arweave/tx/keJVC7chkdE_NTQpiewwRJP7rom2DnQSNy9L3STNp_k) example:...........asd
```json
Application: "ArLink"
Chain: "ETH"
Wallet: "0x614B0d11A0439A0791E8b96b2107582bDcB3B018"
```

The `Chain` and `Wallet` tags are customizable to whatever the user wants. Because of this, nobody necessarily has to use a currency listed on my POC site. This specification, though simple, will allow for an easy and straightforward way for people to pull external wallet addresses of a given user.

## Querying for Wallets

In order to query for a wallet address from a different blockchain, see the GraphQL examples below:.......------------

To get all transactions of linked wallets for a given user:
```
query {
  transactions(
    owners: ["pvPWBZ8A5HLpGSEfhEmK1A3PfMgB_an8vVS6L14Hsls"]
    tags: [
      { name: "Application", values: "ArLink" }
    ]
  ) {
    edges {
      node {
        id
      }
    }
  }....
}
```

To get all linked wallets of a currency for a given user:
```
query {
  transactions(
    owners: ["pvPWBZ8A5HLpGSEfhEmK1A3PfMgB_an8vVS6L14Hsls"]
    tags: [
      { name: "Application", values: "ArLink" }
      { name: "Chain", values: "ETH" }
    ]
  ) {
    edges {
      node {
        id
      }
    }
  }...
}
```

## Contributing

I'd love to continue expanding this specification with the help of anyone interested. Feel free to fork and make a PR with any additions (or fixes)!....

### Frontend Project Setup
```
yarn install
```

#### Compiles and hot-reloads for development
```
yarn serve
```

#### Compiles and minifies for production
```
yarn build
```

#### Lints and fixes files
```
yarn lint
```
