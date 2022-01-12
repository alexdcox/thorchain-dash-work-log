# Thorchain Dash Work Log

To see the official sponsorship of this work see 
<a href="https://trello.com/c/CDKTVi9x/152-thorchain-integration" target="_blank">Trello - Dash Incubator</a>.

Here's the main thorchain/thornode
<a href="https://gitlab.com/thorchain/thornode/-/merge_requests/1931" target="_blank">Dash PR</a>
and the
<a href="https://gitlab.com/thorchain/thornode/-/issues/982" target="_blank">issue</a>.

As of 2022 this log has transitioned to github for markdown formatting to save time on the write-up and for readability. 
For prior work see the 
<a href="https://docs.google.com/document/d/19tk90whX6KYG4DcwtDMND3SL6Ig9BYPm_rahroRRaUQ" target="_blank">Google Doc</a>.

**Update: 12th Jan 2022**  
The bulk of the work has already been completed - at least on the main thorchain/thornode repository.  
Heimdall requested updates to the Node Launcher, which are done but untested. I'm waiting on fixes to other chains before
going back to that.
He also requested updates to the smoke tests, which still need to be done.  

Aside from that I'm just keeping the Dash PR updated in alignment with the official develop branch so that it remains valid, ready to be merged after Doge, Terra and Atom.

**Repositories**  
<a href="https://gitlab.com/thorchain/thornode" target="_blank">Thorchain Thornode</a>  
<a href="https://gitlab.com/thorchain/devops/node-launcher" target="_blank">Thorchain Node Launcher</a>  
<a href="https://gitlab.com/thorchain/heimdall" target="_blank">Thorchain Smoke Tests - Heimdall</a>  
<a href="https://github.com/thorchain/thorchain-explorer" target="_blank">Thorchain Explorer</a>  
<a href="https://github.com/alexdcox/thorchain-cluster" target="_blank">My Local/Dev Thorchain Launcher</a>  
<a href="https://github.com/alexdcox/thorchain-dash-core" target="_blank">My Thorchain Dash Docker Image</a>  
<a href="https://github.com/alexdcox/thorchain-dashd-txscript" target="_blank">My Thorchain Dash Txscript</a>  
<a href="https://github.com/alexdcox/dashutil" target="_blank">My Dashutil</a>  
<a href="https://github.com/alexdcox/dashd-go" target="_blank">My Dashd</a>  

**Log (Continued)**  
[04.01.2022 Tuesday 2hrs](#04012022-tuesday)  
[05.01.2022 Wednesday 4hrs](#05012022-wednesday)  
[11.01.2022 Tuesday 4hrs](#11012022-tuesday)  
[12.01.2022 Wednesday TBD](#12012022-wednesday)  

### 04.01.2022 Tuesday

Having a check-in and seeing if there's anything that needs to be done for the
outstanding PR...  
Merged 179 new commits from develop into dash branch.  
Checking files changed...  

```
gitk --left-right 5d9b2f586...ca6e86412 -- ./bifrost/pkg/chainclients/bitcoin
```

As far as I can tell, it looks like they've just added some extra metrics to the
bifrost clients in `sendNetworkFee`. Updating the Dash PR...  

Running tests again...
```
go test -tags mocknet ./bifrost/pkg/chainclients/dash
```
All passing.

Alright lets test a manual swap again.
- Rebuilding image
- Starting network

### 05.01.2022 Wednesday

- Rebuilding image
- Rebuilding again with bash + socat
- Starting local cluster
- Tail logs and open shells
- Send dash deposit

```
dash-cli listunspent

dash-cli createrawtransaction \
  '[{"txid": "031dc9d7b163b1656a643b5839c04ec0b748b16c0f7bee8b17ddd7739f29f99a", "vout": 0}]' \
  '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 400.0, "ydFKYkx59HaefVJV82qmoiDkCpYKwQ2FGb": 99.99, "data": "6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}'

dash-cli signrawtransaction 02000000019af9299f73d7dd178bee7b0f6cb148b7c04ec039583b646a65b163b1d7c91d030000000000ffffffff0300902f50090000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0a1fc53020000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

dash-cli sendrawtransaction 02000000019af9299f73d7dd178bee7b0f6cb148b7c04ec039583b646a65b163b1d7c91d0300000000484730440220258f648bf6793689a56be46eff28b046d515a97a3ad1540c26742d17f7cf1821022051135251bdf109ef0e143ec57bc3917200361d736eb47d2aecc5780b3dbcf4c101ffffffff0300902f50090000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0a1fc53020000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000
```
- Send rune deposit

```
printf "hat pony twist patient select coffee rhythm erosion soul occur speed athlete carry top present curious slide left enjoy mirror kit dinner switch scout\npassword\n" | thornode keys add alex \
  --keyring-backend=file \
  --recover

echo "password" | thornode tx thorchain send tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv 1200000000000rune \
  --from thornode1 \
  --keyring-backend=file \
  --chain-id thorchain \
  --yes

echo "password" | thornode tx thorchain deposit 100000000000 RUNE "add:dash.dash:yhp44PJ2CChozWpVd787M3cuQ8uFC8j8Gx" \
  --from alex \
  --keyring-backend=file \
  --chain-id thorchain \
  --yes
```

Bifrost is seeing the dash transaction, but it's not being sent off to thorchain.  
Need to get some debugging going for this:

- Reset bifrost with dash config
- Modify docker-compose script commenting out bifrost
- Drop and restart cluster

Seeing a lot of this error:

> fail to get mimir: Status code: 501 Not Implemented returned

```
curl -I localhost:1317/thorchain/mimir/key/HaltChainGlobal
```

```
HTTP/1.1 501 Not Implemented
Access-Control-Allow-Origin: *
Content-Type: application/json
X-Server-Time: 1641414779
Date: Wed, 05 Jan 2022 20:32:59 GMT
Content-Length: 68
```

So that's where this is coming from. Hmmm. Going to fetch develop again and see
if I've missed anything.

I think the `add-genesis-account` command might be broken.
> THORChain add-genesis-account

Yes, it is. The logic of that command accesses a flag that has not been defined
which causes it to fail.

The `FlagKeyringBackend` is part of the Cosmos sdk. It should be defined on a
command with `AddTxFlagsToCmd`. The `AddGenesisAccountCmd` in `thorchain` uses
`AddQueryFlagsToCmd` instead, which doesn't include the keyring backend.

Solutions:
- use the tx flags
- manually add the keyring backend flag

```
./thornode --log_level debug --trace --home $(pwd)/_adc/.thornode init
```

Getting this error from the dash client during `getblock`:

> JSON value is not a boolean as expected

```
curl -X POST
curl -i --user thorchain --data-binary '{"jsonrpc": "1.0", "method": "getblock", "params": ["6d4fbda39d33b254aa731a29c0065cd1591e9b27a3c0c8b1ce209c5918e015ea", 2]}' http://127.0.0.1:19898/
curl -i --user thorchain --data-binary '{"jsonrpc":"1.0","method":"getblock","params":["40dec2868e53a33568e6ad1853f68a18ead67ab9db27620bea998b26381c0a0a",3],"id":8}' http://127.0.0.1:19898/
```

Wow that took a lot of debugging. The second argument to `getblock` was set to
`"2"` which caused the boolean error. The really misleading thing here is that
`true` works, but we actually need `2` (notice the lack of quotes - as an
integer) so that it passes both the boolean convertion/check AND causes the
response to contain additional transaction data. Really unclear error there, I
was looking for a boolean.

Now that's out the way lets get back to the swap...

```
alias thornode="$(pwd)/thornode --log_level debug --trace --home \"$(pwd)/_adc/.thornode\""
```

> error occurred: insufficient funds

I think this could be my fault.

```
thornode query bank balances tthor1zzja0wl7etldc4caprkfjwd74k68qqvfl32tj5
```
```
1200000000000
    100000000
```

I need to add another 5 significant digits to `add_genesis_account`.


### 11.01.2022 Tuesday

Trying a swap ASAP.  
Running `bifrost` from goland.  
Running `thornode` via a cli script.  
Sending a dash tx to thornode.  

```
dash-cli listunspent

dash-cli createrawtransaction \
  '[{"txid": "52bdcd718cf1782a364539277d26bf1c4a67b2bbc7c372589a0227472e3f10f7", "vout": 0}]' \
  '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 400.0, "ydFKYkx59HaefVJV82qmoiDkCpYKwQ2FGb": 64.28, "data": "6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}'

dash-cli signrawtransaction 0200000001f7103f2e4727029a5872c3c7bbb2674a1cbf267d273945362a78f18c71cdbd520000000000ffffffff0300902f50090000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988ac007f237f010000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

dash-cli sendrawtransaction 0200000001f7103f2e4727029a5872c3c7bbb2674a1cbf267d273945362a78f18c71cdbd520000000049483045022100ddfd734eb1dff719d12ff1a06d3ab586f397365f0ac58afdde29198c76202c93022043d10394f0e2bd2e3f2ef74b45bef0b3bad4a914925a41b46703d38447c5a52201ffffffff0300902f50090000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988ac007f237f010000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000
```

```
ERR fail to send to THORChain
fail to send the tx to thorchain:
fail to broadcast to THORChain,code:6
log:
gitlab.com/thorchain/thornode/common/cosmos.ErrUnknownRequest
  /Users/adc/go/src/gitlab.com/thorchain/thornode/common/cosmos/cosmos.go:92
gitlab.com/thorchain/thornode/x/thorchain/types.(*MsgObservedTxIn).ValidateBasic
  /Users/adc/go/src/gitlab.com/thorchain/thornode/x/thorchain/types/msg_observed_txin.go:38
github.com/cosmos/cosmos-sdk/baseapp.validateBasicTxMsgs
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/baseapp/baseapp.go:496
github.com/cosmos/cosmos-sdk/baseapp.(*BaseApp).runTx
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/baseapp/baseapp.go:612
github.com/cosmos/cosmos-sdk/baseapp.(*BaseApp).CheckTx
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/baseapp/abci.go:229
github.com/tendermint/tendermint/abci/client.(*localClient).CheckTxAsync
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/abci/client/local_client.go:98
github.com/tendermint/tendermint/proxy.(*appConnMempool).CheckTxAsync
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/proxy/app_conn.go:126
github.com/tendermint/tendermint/mempool.(*CListMempool).CheckTx
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/mempool/clist_mempool.go:288
github.com/tendermint/tendermint/rpc/core.BroadcastTxSync
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/rpc/core/mempool.go:36
reflect.Value.call
  /usr/local/Cellar/go/1.17.2/libexec/src/reflect/value.go:543
reflect.Value.Call
  /usr/local/Cellar/go/1.17.2/libexec/src/reflect/value.go:339
github.com/tendermint/tendermint/rpc/jsonrpc/server.makeJSONRPCHandler.func1
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/rpc/jsonrpc/server/http_json_handler.go:100
github.com/tendermint/tendermint/rpc/jsonrpc/server.handleInvalidJSONRPCPaths.func1
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/rpc/jsonrpc/server/http_json_handler.go:124
net/http.HandlerFunc.ServeHTTP
  /usr/local/Cellar/go/1.17.2/libexec/src/net/http/server.go:2046
net/http.(*ServeMux).ServeHTTP
  /usr/local/Cellar/go/1.17.2/libexec/src/net/http/server.go:2424
github.com/tendermint/tendermint/rpc/jsonrpc/server.maxBytesHandler.ServeHTTP
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/rpc/jsonrpc/server/http_server.go:234
github.com/tendermint/tendermint/rpc/jsonrpc/server.RecoverAndLogHandler.func1
  /Users/adc/go/pkg/mod/github.com/tendermint/tendermint@v0.34.8/rpc/jsonrpc/server/http_server.go:207
net/http.HandlerFunc.ServeHTTP
  /usr/local/Cellar/go/1.17.2/libexec/src/net/http/server.go:2046
net/http.serverHandler.ServeHTTP
  /usr/local/Cellar/go/1.17.2/libexec/src/net/http/server.go:2878
net/http.(*conn).serve
  /usr/local/Cellar/go/1.17.2/libexec/src/net/http/server.go:1929
request is not an inbound observed transaction: unknown request" module=observer service=bifrost
```

Is DASH on the inbound list?  
Nope. That'll be why.  

Ah another thing for the migration list until the PR gets merged:  
Move chain from previous `manager_network` version and add to the latest one.

The latest network manager is not being used.  
Where is the thornode version actually determined from?  

Looks like it is read from the docker iamge tag as part of the makefile madness
and set in `thorchain.node_accounts.0.version` in `genesis.json`.  
Can I confirm?  

Manually setting `0.76.0` as this is the highest filename `_vXX` suffix.  
Thornode just crashes. No error.  

If I add dash to the network manager v1 will it work? Yep.

-----

@heimdall#4596 Hey happy new year! Hope you enjoyed the holidays. I'm doing my regular check-in with the dash PR and I've stumbled across a new problem.

How do I have the dash chain registered by default for a fresh node - and listed in the `inbound_addresses` list - without modifying `manager_network_v1`?

`supportChains` lists the same chains for each version. I originally just added dash to all the network managers but you asked me to change it to just the last manager, but doing it that way 

-----

Before I send that and bother heimdall I'll spend another 30mins on this...  

Trying to set the node id via the cli.  
> Error: wrong ID: no ID

Alright the version is actually set using linker/build flags. Now that I've found
those I can just `go build ...` and `thornode version` and it shows `0.78.0`.
That's crucial. Alright now will it select the appropriate network manager?  

Yes! So I wont need to bug heimdall with the above.

Saw the dev plan on the dash channel: DOGE -> TERRA -> ATOM

Explained the 2-4-1 nature of having dash/decred considered:

-----

I've been updating both the dash and decred PRs, so if one passes the other is
likely not far off. Worth nothing the community could get 2 chains in rapid
succession if dash or decred is voted next.

-----

Jiminy cricket! One of the tests failed. `TestVaultSorBySecurity` in `keeper_vault_test`.  
Odd, is this also broken on the official dev channel?  

```
go test -tags mocknet ./x/thorchain/keeper/v1 -check.f ^KeeperVaultSuite.TestVaultSorBySecurity$
```

Yes it is.

```
pool1
  asset           BNB
  balance rune    100
  balance asset   100

vault1
  totalValue: 0.00000000
  totalBond: 700.00000000
  diff: 700.00000000

vault 2
  totalValue: 1000.00000000
  totalBond: 700.00000000
  diff: -300.00000000

vault 3
  totalValue: 100.00000000
  totalBond: 700.00000000
  diff: 600.00000000
```

Order from lowest to highest should go: `2, 3, 1` but test requires `2, 1, 3`.  
Should I create a PR for that?  

I went ahead and done did that:  
[Thornode PR 2068](https://gitlab.com/thorchain/thornode/-/merge_requests/2068#note_807789772)

### 12.01.2022 Wednesday

Spent 1.5hrs on admin and getting the new work log repo sorted out. That will save
time in future.

The 2068 PR has two approvals, Heimdall and Eridanus, but has already fallen behind
develop. Updating again... Now I need two more approvals, at least one from dev
and one from security.


