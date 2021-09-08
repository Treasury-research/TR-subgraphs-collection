# ERC20 Balance Subgraph


## To setup and deploy

## Graph Explorer

### 
```
yarn 
yarn global add @graphprotocol/graph-cli
yarn run prepare:mainnet // prepare:mainnet || prepare:mainnet
npx graph-compiler \
  --config subgraphconfig.json \
  --include node_modules/@openzeppelin/subgraphs/src/datasources \
  --export-schema \
  --export-subgraph
cd generated
graph auth <ACCESS_TOKEN> // 
graph deploy --studio  xxx // xxx you create subgraph name
```

## Legacy Explorer
```
yarn 
yarn global add @graphprotocol/graph-cli
yarn run prepare:mainnet // prepare:mainnet || prepare:mainnet
npx graph-compiler \
  --config subgraphconfig.json \
  --include node_modules/@openzeppelin/subgraphs/src/datasources \
  --export-schema \
  --export-subgraph
cd generated
graph auth --product hosted-service <ACCESS_TOKEN>
graph deploy --product hosted-service <GITHUB_USER>/<SUBGRAPH NAME>  
```


## Query examples
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


### Deply Host

* [erc20-mainnet](https://api.thegraph.com/subgraphs/name/treasury-research/erc20-distribution-tr-creation)
* [erc20-polygon](https://api.thegraph.com/subgraphs/name/treasury-research/erc20-polygon-tr-creation)
* [bep20-bsc](https://api.thegraph.com/subgraphs/name/treasury-research/bep20-bsc-tr-creation)
* [erc20-fantom](https://api.thegraph.com/subgraphs/name/treasury-research/erc20-fantom-tr-creation)

## reference
>[openzeppelin-subgraphs](https://github.com/OpenZeppelin/openzeppelin-subgraphs)
>[thegraph](https://thegraph.com/docs/developer/quick-start)
