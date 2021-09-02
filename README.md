# ERC20 Balance Subgraph


## To setup and deploy


### mainnet

```
yarn 
yarn global add @graphprotocol/graph-cli
npx graph-compiler \
  --config subgraphconfig.json \
  --include node_modules/@openzeppelin/subgraphs/src/datasources \
  --export-schema \
  --export-subgraph
cd generated
graph auth ...
graph deploy --studio  xxx // xxx you create subgraph name
```
### Query examples
1. Total supply and biggest token holders
```
{
  erc20Contract(id: "<token-address-in-lowercase>") {
    totalSupply {
      value
    }
    balances(orderBy: valueExact, orderDirection: desc, where: { account_not: null }) {
      account {
        id
      }
      value
    }
  }
}
```

2. Most recent transfers with transaction id
```
{
  erc20Contract(id: "<token-address-in-lowercase>") {
    transfers(orderBy: timestamp, orderDirection: desc) {
      from { id }
      to { id }
      value
      transaction { id }
    }
  }
}
```
3. All indexed ERC20 balances for a account
```
{
  account(id: "<user-address-in-lowercase>") {
    ERC20balances {
      contract{ name, symbol, decimals }
    	value
    }
  }
}
```




## reference
>[openzeppelin-subgraphs](https://github.com/OpenZeppelin/openzeppelin-subgraphs)
