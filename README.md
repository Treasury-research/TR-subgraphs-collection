# ERC20 Balance Subgraph


## To setup and deploy


### mainnet

```
npx graph-compiler \
  --config subgraphconfig.json \
  --include node_modules/@openzeppelin/subgraphs/src/datasources \
  --export-schema \
  --export-subgraph
graph auth ...
yarn build
yarn deploy --studio xxx // xxx you create subgraph name
```

## reference
>[openzeppelin-subgraphs](https://github.com/OpenZeppelin/openzeppelin-subgraphs)