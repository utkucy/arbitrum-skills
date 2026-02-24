#  Orbit Chains Example

```shell
docker run --rm -it -v /some/local/dir/arbitrum:/home/user/.arbitrum -p 0.0.0.0:8547:8547 -p 0.0.0.0:8548:8548 @@latestNitroNodeImage=offchainlabs/nitro-node:v3.9.4-7f582c3@@ --parent-chain.connection.url=  --chain.info-json= --chain.name= --node.feed.input.url= --execution.forwarding-target= --http.api=net,web3,eth --http.corsdomain=* --http.addr=0.0.0.0 --http.vhosts=*
```

- You can see an example of `--chain.info-json` in the section above.