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

Aside from that I'm just keeping the Dash PR updated in alignment with the
official develop branch so that it remains valid, ready to be merged after
Doge, Terra and Atom.

**Update: 13th March 2022**

Been blocked by a request from TC devs to replace `github.com/alexdcox`
dependencies with official channel repos, in this case `github.com/dashevo`.
This involved putting in a pull-request to have the changes I need merged into
the official project. Unfortunately, it wasn't maintained in the first place
and all of the chain specific info still related to bitcoin. My changes updated
the chain identifiers from bitcoin to dash but this broke many tests. These
needed to be fixed before maintainers would be happy to include my code, which
took a lot of extra time. Just waiting for that PR to actually be merged in now
before I can move on...

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
[12.01.2022 Wednesday 7hrs](#12012022-wednesday)  
[13.01.2022 Thursday 7hrs](#13012022-thursday)  
[14.01.2022 Friday 7hrs](#14012022-friday)  
[19.01.2022 Wednesday 7hrs](#19012022-wednesday)  
[20.01.2022 Thursday 7hrs](#20012022-thursday)  
[21.01.2022 Friday 7hrs](#21012022-friday)  
[24.01.2022 Monday 2.5hrs](#24012022-monday)  
[26.01.2022 Wednesday 5.5hrs](#26012022-wednesday)  
[27.01.2022 Thursday 2hrs](#27012022-thursday)  
[28.01.2022 Friday 2hrs](#28012022-friday)  
[03.02.2022 Thursday 7hrs](#03022022-thursday)  
[08.02.2022 Tuesday 7hrs](#08022022-tuesday)  
[09.02.2022 Wednesday 2hrs](#09022022-wednesday)  
[10.02.2022 Thursday 7hrs](#10022022-thursday)  

[14.02.2022 Monday 2hrs](#14022022-monday)  
[24.02.2022 Thursday 1hr](#24022022-thursday)  
[25.02.2022 Friday 1hr](#25022022-friday)  
[29.02.2022 Monday 0hrs](#29022022-monday)  
[01.03.2022 Tuesday 1hr](#01032022-tuesday)  
[02.03.2022 Wednesday 5hrs](#02032022-wednesday)  
[04.03.2022 Friday 7hrs](#04032022-friday)  
[07.03.2022 Monday 1hr](#07032022-monday)  

[29.03.2022 Tuesday 7hrs](#29032022-tuesday)  
[20.04.2022 Wednesday 0hrs](#20042022-wednesday)  
[21.04.2022 Thursday 7hrs](#21042022-thursday)  
[22.04.2022 Friday 2hrs](#22042022-friday)  
[27.04.2022 Wednesday 2hrs](#27042022-wednesday)  
[02.05.2022 Monday 7hrs](#02052022-monday)  
[03.05.2022 Tuesday 7hrs](#03052022-tuesday)  
[09.05.2022 Monday 0hrs](#09052022-monday)  
[10.05.2022 Tuesday 7hrs](#10052022-tuesday)  
[11.05.2022 Wednesday 7hrs](#11052022-wednesday)  
[12.05.2022 Thursday 7hrs](#12052022-thursday)  
[13.05.2022 Friday 4hrs](#13052022-friday)  
[17.05.2022 Tuesday 2hrs](#17052022-tuesday)  
[18.05.2022 Wednedsay 4hrs](#18052022-wednesday)  
[20.05.2022 Friday 7hrs](#20052022-friday)  
[21.05.2022 Saturday 3.5hrs](#21052022-saturday)  
[22.05.2022 Sunday 1hr](#22052022-sunday)  

[23.05.2022 Monday 7h](#23052022-monday)  
[24.05.2022 Tuesday 0h](#24052022-tuesday)  
[06.07.2022 Wednesday 3h 30m](#06072022-wednesday)  
[07.07.2022 Thursday 7h 15m](#07072022-thursday)  
[08.07.2022 Friday 1h](#08072022-friday)  
[14.07.2022 Thursday 7h](#14072022-thursday)  
[15.07.2022 Friday 7h 20m](#15072022-friday)  
[21.07.2022 Thursday 7h](#21072022-thursday)  
[22.07.2022 Friday 7h](#22072022-friday)  



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

Okay looking at Heimdall, the smoke testing repo.
```
make build
make test
```
52/52 tests passed.

Now to add Dash. Oh wait, there's this.

```
make smoke
```

> Retrying (Retry(total=5, connect=5, read=6, redirect=None, status=None)) after connection broken by 'NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7faa18962280>: Failed to establish a new connection: [Errno 111] Connection refused')': /thorchain/lastblock

Will it connect to my local cluster? No. It's a kubernetes thing.  
Right ok back to testing the node-launcher then.  

Do I have enough space on my desktop pc for k8s?  
I actually found a 400GB virtualbox image called k8s.  
It's just one machine but perhaps that will be enough?  
Couldn't remember the root password but I did manage to connect from my work laptop using my ssh key. Nice!  
Got to a point where I need to know the sudo password. I can't remember.  
Boot into recovery mode, then root shell, then force change passwords to `p` (nice and easy)  

Updated kube config to point to new vm assigned ip.  
Forgot for a moment that all clusters are listed in the same config file.  
Hmm lens can't get in:

> Cannot read property 'resetAfterIndex' of null

An update sorted it.  
Right now I'm in a cluster. It's doing things. What's it doing? Ahhhhh.  

There's a thornode service in there, apparently running on the testnet and
trying to catch up to the latest block.

Do the helm charts have a mocknet option?

Important note: you can see the nextChurnHeight on midgard like:  
https://testnet.midgard.thorchain.info/v2/network

You can see the current block height under `scannerHeight` here:  
https://testnet.midgard.thorchain.info/v2/health

```
So I'm on block       1137241  
and the testnet is on  992979
```

Time for a restart I think. Now how in dante's inferno do I do that again?

```
kubectl exec -it -n thornode-testnet thornode-77445588c5-ljbxh "--" sh
make status
```

> Unable to connect to the server: dial tcp: lookup 2F13ABBFD4CF1C7A2FE0D77382F51892.yl4.us-west-2.eks.amazonaws.com on 192.168.1.1:53: no such host

It's using my aws config rather than my microk8s config.

Just catching up to develop `Updating 6f921d4..b97f03b`.  

Ah something's coming back to me. I may have established that microk8s is not
suitable for the node-launcher in its current state due to it requiring access
to aws network components. I think I switched over to using aws for simplicity,
but that was before I worked out how to override the scripts.

That's right, there's a `kube-scripts` folder in my `thorchain-cluster` repo. I
think that's where I left off with this. Oh check out my log from `03.11.2021`.
Heimdall said testnet wouldn't work right now. There have been many commits
since then so going to try...

Okay now there's something called `stagenet`. What is that!?  
Initial commit Dec 05, 2021  
https://gitlab.com/thorchain/thornode/-/merge_requests/2019  
https://gitlab.com/thorchain/thornode/-/issues/1211  

That PR/issue is really helpful to follow. We'll have to walk the same path in
order to deploy dash to chaosnet.

Updated `node-launcher` for dash to reflect the new stagenet changes and doge
config, PR:  
https://gitlab.com/thorchain/devops/node-launcher/-/merge_requests/361

Now `make status` retuned for testnet:
```
API         http://:1317/thorchain/doc/
RPC         http://:26657
MIDGARD     http://:8080/v2/doc

CHAIN       SYNC       BLOCKS
THOR        85.505%    1,153,617/1,349,182
```

The IP isn't set correctly. Using the k8s host IP doesn't work.  

Still, this is good.

Side note: my `[bugfix] correct expected vault sort order in keeper_vault_test`
was merged in :)

Looks like there's a lot of progress getting Doge merged in atm.

> testnet is broken due to binance full node can't find peers to sync
- heimdall

Lets try dash on my own `stagenet` then... I'm going to have to update my
thornode gitlab docker image too.  

So I ran `make install`, selected `stagenet` with `validator` node type. Got the
error:

> :: Mnemonic generation failed. Please try again.

The code is in `core.sh`:
```
create_mnemonic() {
  local mnemonic
  if ! kubectl get -n "$NAME" secrets/thornode-mnemonic >/dev/null 2>&1; then
    echo "=> Generating THORNode Mnemonic phrase"
    mnemonic=$(kubectl run -n "$NAME" -it --rm mnemonic --image=registry.gitlab.com/thorchain/thornode --restart=Never --command -- generate | grep MASTER_MNEMONIC | cut -d '=' -f 2 | tr -d '\r')
    [ "$mnemonic" = "" ] && die "Mnemonic generation failed. Please try again."
    kubectl -n "$NAME" create secret generic thornode-mnemonic --from-literal=mnemonic="$mnemonic"
    echo
  fi
}
```

```
kubectl run -n "thornode-stagenet" -it --rm mnemonic --image=registry.gitlab.com/thorchain/thornode --restart=Never --command -- generate
```

Well that worked, I think the arguments to cut and tr probably are inconsistent
with the versions I have bundled with macos.

```
echo 'export MASTER_MNEMONIC=urge wife assault steel sphere parade royal cabin tiger endless say error onion thunder provide husband cannon enforce few orient toast measure wish purchase' | \
grep MASTER_MNEMONIC | cut -d '=' -f 2 | tr -d '\r'
```

Oh that worked just fine. Ah they're running in the docker container, right?

```
kubectl run -n "thornode-stagenet" -it --rm mnemonic --image=registry.gitlab.com/thorchain/thornode --restart=Never --command -- generate | grep MASTER_MNEMONIC | cut -d '=' -f 2 | tr -d '\r'

mnemonic=$(kubectl run -n "thornode-stagenet" -it --rm mnemonic --image=registry.gitlab.com/thorchain/thornode --restart=Never --command -- generate | grep MASTER_MNEMONIC | cut -d '=' -f 2 | tr -d '\r')
echo $mnemonic
```

Works fine. Perhaps we should just try again...

I don't think this is using my image either.
Also not quite sure how I got around the humongous hd space requirements of the
PVCs.

Need to search `cpu`, `memory` and `Gi` within `gd HEAD add-dash2` to see how I
changed the specs to fit micro k8s. It'd be nice to have either mocknet with
minimal specs or an entirely different kind of network which is designed to run
on a k8s cluster of 1 machine, i.e. development.

Alright that's my day.

### 13.01.2022 Thursday

Cluster stuck in a familiar place, waiting on external ip.

```
kubectl -n thornode-stagenet get svc "thornode" -o jsonpath='{.spec.type}'
# ClusterIP

kubectl get nodes --selector=kubernetes.io/role!=master -o jsonpath='{.items[0].status.addresses[?(@.type=="ExternalIP")].address}'
```

Both `gateway` and `thornode` are blocked by the `init-external-ip`

> Failed to pull image "registry.gitlab.com/alexdcox/thornode:stagenet-0.78.1":
  rpc error: code = NotFound desc = failed to pull and unpack
  image "registry.gitlab.com/alexdcox/thornode:stagenet-0.78.1": failed to
  resolve reference "registry.gitlab.com/alexdcox/thornode:stagenet-0.78.1":
  registry.gitlab.com/alexdcox/thornode:stagenet-0.78.1: not found

Fair enough.

`cat ./version`
> 0.79.0

```
cd build/docker; DOCKER_BUILDKIT=0 docker build --build-arg TAG=stagenet -t registry.gitlab.com/alexdcox/thornode -f Dockerfile ../..; cd -
docker tag registry.gitlab.com/alexdcox/thornode registry.gitlab.com/alexdcox/thornode:stagenet-0.79.0
docker push registry.gitlab.com/alexdcox/thornode:stagenet-0.79.0
```

Pushed.

Reaching cluster memory capacity.

`thornode-stack/values.yaml`
```
bifrost:
  fullnameOverride: bifrost
  service:
    type: NodePort
  persistence:
    size:
      stagenet: 10Gi
  resources:
    limits:
      cpu: 0.5
      memory: 0.5Gi
    requests:
      cpu: 0.5
      memory: 0.5G
```

Using that kind of approach for all services in that one file. Monitoring
cpu/mem requests vs limits as the pods spin up...  

I'm at about 1/2 capacity with the above.  
Watching the ip init...  
> configmap/thornode-external-ip created

Really??  
No. It's empty. Maybe that's ok?  
Forgot to update the image version.  
Thornode is quite slow with those settings, doubled cpu/mem.  

Quick segway responding to Brian Foster about TC and the Dash Wallet...

---

Good point, not the entire ledger. Just since the last churn (max approx 3 days). It'd make more sense to keep it all in-memory to reduce the overhead per observed tx - rather than scanning since the last churn. Might be small but still, it bumps up the memory requirement and cpu overhead per thornode.

Also, the thornode vault keys are split and shared between "churned in" nodes. They'd have to group sign (tx2) So (tx1) would have to propagate the TC network. Fees should be covered by (tx1a). Might need a system for moving responsibility for pending transfers over to new thornodes if they straddle a churn cycle - would have to consult the TC devs.

All this additional complexity is asking a lot from the TC devs when technically what they have already is working perfectly, it's just the wallets/clients which need to tailor their transactions. I don't see them going for it.

The more I think on this the more I believe the path of least resistance to be a proxy sitting in the middle between wallets and thornode, with one rpc endpoint for chosing the source/destination chain + payout address, which returns a one-time use deposit address (or standard/current BIP70 protocol url).

It's a centralised solution, but the easiest.

Another option is to do everything on the front-end, perhaps within an embedded webapp. That would need to make external calls to fetch transaction data in order to format the thornode deposit transactions. Also the webapp server would be centralised, unless everything is embedded in the wallets, which adds bloat and complicates updates accross multiple apks with different maintainers.

I spoke with Ash, he's going to write up a google doc with strategies.

---

> if they straddle a churn cycle

Actually if we allow this then it would be the whole ledger of pending (tx1s) that we need to hold in-memory. Unless they expire.

---

Enough digressing.  

> Missing PEER / SEEDS

Hmmmm. Genesis node?  

WOW. Everything is actually running except the bifrost.
It's stuck on `init-dash` with the message `waiting for dash` a
bambinozillion times.

```
sh -c until curl -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@http://dash-daemon:19898 > /dev/null;
  do echo waiting for dash;
sleep 2;
done
```

```
curl -i --user thorchain --data-binary '{"jsonrpc": "1.0", "method": "getblockchaininfo"}' http://dash-daemon:19898/
curl -i --user thorchain --data-binary '{"jsonrpc": "1.0", "method": "getblockchaininfo"}' http://dash-daemon:9998/
```

Probably just need to update the `bifrost` `init-dash` startup container for `stagenet`.  
bifrost > values > dashDaemon > stagenet  

Bumping up bifrost stats too, very slow.

Times up for today, going to add extra time until these init containers finish
cause it took so long to get here I'd rather not kill it...  

```
curl -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@http://dash-daemon:9998
```

Ah. Look at the url. That's not good.  
Okay +20mins for finding that, now I'm wrapping up for today.  


### 14.01.2022 Friday

Cluster start...  

I used `microk8s reset` yesterday thinking that was a good idea.  
Now I'm missing `calico-ipam` whatever that is.

```
microk8s enable dns
```

Going to bump up the cpu/mem of my microk8s.  
Already giving it use of all my cores.  
Doubled the mem from 10GB to 20GB. Lets see how this plays out...  

That's a whole lot better. 4mins in from fresh I have everything green except
bifrost, which is currently still going through the init container sequence.  

Will it get stuck on dash?  
Yes.  
Fixed the uri  
Now getting stuck on ethereum. It's not running. Setting `ethereumDaemn.enabled`
to false. (why is this not the default?)

ALL GREEN.

Can I run the network explorer against that?  
Need to expose the services first...  

```
kubectl -n thornode-stagenet expose deployment thornode --name=thornode
curl 10.1.77.49:1317/node_info
```

That works but I have to ssh into the node to run curl, and it's hovering around
full cpu utilisation so using the terminal is extremely slow.  
Changed `NodePort` to `HostPort` so that the actual node/vm exposes the ports.  

microk8s ingress addon is actually already enabled along with:

```
dashboard            # The Kubernetes dashboard
dns                  # CoreDNS
ha-cluster           # Configure high availability on the current node
ingress              # Ingress controller for external access
metrics-server       # K8s Metrics Server for API access to service metrics
openfaas             # openfaas serverless framework
storage              # Storage class; allocates storage from host directory
```

```
kubectl apply -f ./kubernetes/definitions/thornode-ingress.yaml
```

`curl localhost/thornode`
> 503 Service Temporarily Unavailable


> * spec.rules[0].http.paths[0].pathType: Required value: pathType must be specified
> * annotations.kubernetes.io/ingress.class: Invalid value: "public": can not be set when the class field is also set

Need to use the same namespace for the ingress controller and target service,
even though the default ingress controller launches in its own namespace `ingress`
and has access to all `kind: Ingress` configurations by default.

`curl localhost/thornode/node_info`
```
{
  "code": 12,
  "message": "Not Implemented",
  "details": [
  ]
}
```

Looks like a dashd rpc response to me. I wonder if the path rewriting hasn't
been configured properly.

```
curl 10.1.77.49:1317/node_info
curl localhost/thornode/node_info
```

Getting a response when called directly but `Not Implemented` via the ingress.  
Trying `networking.k8s.io/v1beta1` instead of `networking.k8s.io/v1`  

> Warning: networking.k8s.io/v1beta1 Ingress is deprecated in v1.19+, unavailable in v1.22+; use networking.k8s.io/v1 Ingress

I don't think that'll be it.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$2
spec:
  ingressClassName: public
  rules:
    - http:
        paths:
          - path: /thornode(/|$)(.*)
            pathType: ImplementationSpecific
            backend:
              service:
                name: thornode
                port:
                  number: 1317
```

Had to use regex match `/thornode(/|$)(.*)` and rewrite `/$2` config.

What about from my laptop now?: `curl 192.168.1.111/thornode/node_info`.

Now THAT is a thing of beauty! Works nicely.

Moving on to actually inspecting the health of the pods. Bifrost has 21 restarts.  

```
{
  "level": "fatal",
  "service": "bifrost",
  "module": "bifrost",
  "error": "Get \"http://binance-daemon:27147/status\": dial tcp: lookup binance-daemon on 10.152.183.10:53: no such host",
  "chain_id": "BNB",
  "time": "2022-01-15T01:09:49Z",
  "message": "fail to load chain"
}
```

It's still configured to look for binance-daemon despite me disabling it. Hmm.

Here's a good example of something that loses me:  
Every chain requires an init container to be defined on the bifrost k8s config.  
Without these, bifrost will start and crash, because it can't connect to them.  
I think that's the only reason for them.  
Instead of all this extra infrastructure, this could be solved in go within the 
bifrost with a config variable like `attemptNodeReconnectDuringStartup` or the
opposite `failFastIfNodeUnreachable`. If it dials a node that hasn't started or
isn't quite up and running it will wait, patiently, until everything is ok. 
Something along those lines would make the bifrost startup FASTER AND SIMPLER.

I dont think the `make install` causes the pod to rethink it's init config.


### 19.01.2022 Wednesday

Both Dash and Decred are being prioritised now. Awesome news!

Will continue with Dash for now as it's the one I updated last and alternate.
This is Leena's list:
- [ ] Review the UTXO Bifrost Logic List @Pluto (9R)  and make sure Dash meets all logic requirements
- [ ] Submit to @Hildisv??ni??ttar for a vulnerability review
- [ ] Submit your node-launcher update to @Fandral for a review
- [ ] Submit your xchain-dash PR to @veado 
- [ ] Identify a THORChain ecosystem wallet who will flagship your launch and work to get it integrated. 
- [ ] Launch DASH on stagenet

Messaged Pluto (9R) asking if he's the person to talk to regarding point one.
I need to ask what his flow is.

Let's do a quick pull dev and see if I can actually run the tests and get a swap
passing locally. Min requirement.

`git pull origin develop`
`Updating 3e7cb1c5d..9d08b2d7a`

`git merge develop`

Comparing dash `client.go` to doge `client.go`:
- TODO: What should the `reportSolvency` block interval be for dash? DOGE is 10, LTC is 5.
- Dogecoin `sendNetworkFee` signature is `blockResult *btcjson.GetBlockVerboseTxResult`, every other client is `height int`.
- Dash `sendNetworkFee` is very different to the one in Doge. Seems to be identical to BTC.
- Doge `GetGauge` not used?? Is this intentional?
- Dash `removeFromMemPoolCache(tx.Txid)` Doge `removeFromMemPoolCache(tx.Hash)` am I introducing a bug here?
- `getHighestFeeRate` was copied from LTC, does DASH really need this? Nope. Not used.

Now `signer.go`.
- All the other clients now have `getMaximumUtxosToSpend`, dash doesn't.
- `estimateTxSize` doesn't seem to have been updated for dash (same as BTC + DOGE)

  For the trustwallet, dash fee calculations would use the default fee calculator.
  Lets work through and see how far off we are:

  `printf 'swap:bch.bch:qp3wjpa3tjlj042z2wv7hahsldgwhwy0rq9sywjpyy' | hexdump -v -e '/1 "%02x"'`

  ```
  overhead                                       10
  per input                           148
  1 inputs                            148 * 1 = 148
  per output                          34
  2 p2pkh outputs (deposit, change)   34 * 2  =  68
  memo                                swap:bch.bch:qp3wjpa3tjlj042z2wv7hahsldgwhwy0rq9sywjpyy
  memo hex                            737761703a6263682e6263683a717033776a706133746a6c6a3034327a32777637686168736c646777687779307271397379776a707979
  memo length (bytes)                 55
  1 op_return/memo output             9 + 55  =  64

  total                                       = 290
  ```

  Looking back at my logs for dash:
  ```
  sendrawtransaction   bytes
  11.01.2022           261
  05.01.2022           260
  22.09.2021           261
  ```

  Looks like we've estimated a bit more than necessary, something to come back
  to perhaps.

Pushed commit:
`Update dash to match latest develop conventions, add solvency checker and signer cache`

Re-running tests.

> FAIL: client_test.go:666: DashSuite.TestGetMemPool
> fail to parse memo: MEMO

`go test -tags mocknet ./bifrost/pkg/chainclients/dash -check.f DashSuite.TestGetMemPool`

The transaction in the raw mempool fixture is somehow now passing the
`txInItem.IsEmpty` check within `getMemPool`. Ah it goes back to the `isMemPool`
variable being always set to `true` and passed in from `getMemPool`. I put this
check back, but I actually think it needs to be removed, again. It makes sense
for the chains with RBF but that logic doesn't apply to dash.

Re-running tests. Now we're sitting pretty.

Need to update `dashd-go` `TxRawResult` to also include:
- chainlock bool
- instantlock bool
- instantlock_internal bool

New `dashd-go` commit is: `8df79283143b9ce4f895186d425dd8f8bbae3f86`

`go get -u github.com/alexdcox/dashd-go`
`go get -u github.com/alexdcox/dashd-go@8df79283143b9ce4f895186d425dd8f8bbae3f86`

Oops introduced a typo in that commit, force-overwrite. New commit:
eec5a1af50e410b5ab906f978116e90db76ac5d9

`go get -u github.com/alexdcox/dashd-go@eec5a1af50e410b5ab906f978116e90db76ac5d9`

Better. Now adding the `chainlock` check in `ignoreTx`.

Re-running tests. OK.

Trying a swap (hopefully uninterrupted from this point)

Rebuild docker image `./_adc/docker-build-image.sh`.  
Uncomment `thornode1` in docker compose and start network.  

> COPY failed: file not found in build context or excluded by .dockerignore:
  stat Users/adc/go/src/github.com/alexdcox/thorchain-cluster/scripts: file
  does not exist

Ah. Yes. Perhaps I can just add it as another symlink?  

Nope. Was easier to just create a custom `Dockerfile` with just `apk add bash
socat` and run off the previous image.


```
dash-cli listunspent

dash-cli createrawtransaction \
  '[{"txid": "f732f9950b8f94701fc511958e7d5c02c032d6ba45ae72774e0aefc619690174", "vout": 0}]' \
  '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 464.0, "ydFKYkx59HaefVJV82qmoiDkCpYKwQ2FGb": 0.28, "data": "6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}'

dash-cli signrawtransaction 020000000174016919c6ef0a4e7772ae45bad632c0025c7d8e9511c51f70948f0b95f932f70000000000ffffffff0300d0a7cd0a0000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988ac003fab01000000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

dash-cli sendrawtransaction 020000000174016919c6ef0a4e7772ae45bad632c0025c7d8e9511c51f70948f0b95f932f70000000047463043021f0e6b9bf36c809955e8749be7a664f2b4d6fa6c99a3bcfbb4550b0f9aeeb0dd022014c02361f4b4ce469f9cc3d38ff4f71c4f94579e3765d23bf7ffeaab6459fc4f01ffffffff0300d0a7cd0a0000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988ac003fab01000000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000
```
> f11782c88232daf4b57f4dd2d81d33d1a71894a872f78b5cb054e2d300b32b9f

```
printf "hat pony twist patient select coffee rhythm erosion soul occur speed athlete carry top present curious slide left enjoy mirror kit dinner switch scout\npassword\n" | thornode keys add alex \
  --keyring-backend=file \
  --recover

echo "password" | thornode tx thorchain send tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv 1200000000000rune \
  --from thorchain \
  --keyring-backend=file \
  --chain-id thorchain \
  --yes

echo "password" | thornode tx thorchain deposit 100000000000 RUNE "add:dash.dash:yX6kD415WGpwwDkb1AEgJettjj775KSSUZ" \
  --from alex \
  --keyring-backend=file \
  --chain-id thorchain \
  --yes
```

> out of gas in location: ValuePerByte; gasWanted: 200000, gasUsed: 200123: out of gas

```
 1200000000000 rune balance
  100000000000 rune deposit
```

`thornode query bank balances tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv`
`dash-cli getaddressbalance '{"addresses": ["ydnHXynWVSJFsnRGYsnCG4rjxcjEViQYSN"]}'`

They both have value, more than enough. Does the deposit address need to
correspond also to a thornode account with value? Is that what that's saying?

Not sure why this happens or what I can do to fix it. It's come up from time to
time and restarting the cluster and doing the exact same steps seems to resolve
it. Will try that now...

Same answer. Okay going to try using the same thorchain key for tc and dash
addresses, although I feel like I didn't have to do this before.

Okay using the good ol' `crypto-tool` we have:

```
hat pony twist patient select coffee rhythm erosion soul occur speed athlete carry top present curious slide left enjoy mirror kit dinner switch scout

private key hex   9f5a1d81ddda2a6c27e949d501b63308486f22a349717b13d657c52df9b5572f
public key hex    0252e0f092042649eb84346301f334e8aa01ff9eaf2e5df235a0a74b5e3e2d7baf

address           tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv

account           tthorpub1addwnpepqffwpuyjqsnyn6uyx33srue5az4qrlu74uh9mu345zn5kh3794a67d6ex33
validator         tthorvpub1addwnpepqffwpuyjqsnyn6uyx33srue5az4qrlu74uh9mu345zn5kh3794a67ta9hyu
consensus         tthorcpub1addwnpepqffwpuyjqsnyn6uyx33srue5az4qrlu74uh9mu345zn5kh3794a67hlpfvq

dash.mainnet          XmU9C6ve4jAsbUq3SJvHGdUYTScjXkiL79
dash.test|regnet      yX6kD415WGpwwDkb1AEgJettjj775KSSUZ
dash.test|regnet.wif  cSvThVecyYSCPzispSGLyUQdMRjqderB5XUu4JtrKUNBmAE8rbd4

dcr.mainnet       DSdhiFyWfUNCceEU6BaZyr1oTJ2FrhbsGuG
dcr.simnet        SSh65TU6a2SaZEVkS3nmEayskmM5axzK315
dcr.wif           PsURL3aH3P2pWoVYVTxYrCBRSkbT4ciFsg322UUZZrfrdEtYo7NY2
```


```
dash-cli importprivkey cSvThVecyYSCPzispSGLyUQdMRjqderB5XUu4JtrKUNBmAE8rbd4
dash-cli sendtoaddress yX6kD415WGpwwDkb1AEgJettjj775KSSUZ 1000
dash-cli getaddressbalance '{"addresses": ["yX6kD415WGpwwDkb1AEgJettjj775KSSUZ"]}'
dash-cli listunspent 1 99999999 '["yX6kD415WGpwwDkb1AEgJettjj775KSSUZ"]'

dash-cli createrawtransaction \
  '[{"txid": "f5bab5f20a00ae8953d7dc0416032c8fe758743dcc57ccbc42c9e3809da35338", "vout": 1}]' \
  '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 100.0, "ydFKYkx59HaefVJV82qmoiDkCpYKwQ2FGb": 899.99, "data": "6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}'

dash-cli signrawtransaction 02000000013853a39d80e3c942bccc57cc3d7458e78f2c031604dcd75389ae000af2b5baf50100000000ffffffff0300e40b54020000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0c15bf4140000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

dash-cli sendrawtransaction 02000000013853a39d80e3c942bccc57cc3d7458e78f2c031604dcd75389ae000af2b5baf5010000006a4730440220369c222c13aaa6a5a485839b2c508e93f661540dd99cbc4951371ac6af225b24022045a2376a365f955f869b66a9f460497b7a2c1f21a7077f071bdfab00d87cb3b701210252e0f092042649eb84346301f334e8aa01ff9eaf2e5df235a0a74b5e3e2d7bafffffffff0300e40b54020000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0c15bf4140000001976a914b9b2614e78b0da13a970c627bb3d7f5ac1a97fab88ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

dash-cli getaddressbalance '{"addresses": ["yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR"]}'
```

> 13f48956a4d451da2ca39da0416c39b66ed8d422e7a8dea914b6e8833192f21f

Still getting:
> out of gas in location.

Could it be that the dash has been sent but thornode is unaware of it?

Alright I'm going to give my brain a rest, 20mins left on the clock. 6h 40m
logged. Will spill the 20m over to tomorrow.

### 20.01.2022 Thursday

So I'm lifting off from a brand new cluster again and trying to get swaps
working. Last attempt stalled at `out of gas in location`.

Waiting for new cluster to startup...  

Asked heimdall for help with the out of gas issue. He said to use a `--gas` flag.

```bash
######################################
# Create + Fund Thornode Wallet
######################################

# thornode1
# ---------

printf "hat pony twist patient select coffee rhythm erosion soul occur speed athlete carry top present curious slide left enjoy mirror kit dinner switch scout\npassword\n" | thornode keys add alex \
  --keyring-backend file \
  --recover

echo "password" | thornode tx thorchain send tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv 1200000000000rune \
  --from thorchain \
  --keyring-backend file \
  --chain-id thorchain \
  --yes

######################################
# Create Dash Pool
######################################

# thornode1
# ---------

echo "password" | thornode tx thorchain deposit 100000000000 RUNE "add:dash.dash:yX6kD415WGpwwDkb1AEgJettjj775KSSUZ" \
  --from alex \
  --keyring-backend file \
  --chain-id thorchain \
  --gas 1000000 \
  --yes

# dash1
# ---------

dash-cli importprivkey cSvThVecyYSCPzispSGLyUQdMRjqderB5XUu4JtrKUNBmAE8rbd4
dash-cli sendtoaddress yX6kD415WGpwwDkb1AEgJettjj775KSSUZ 1000
dash-cli listunspent 1 99999999 '["yX6kD415WGpwwDkb1AEgJettjj775KSSUZ"]'

# `printf 'add:dash.dash:tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv' | hexdump -v -e '/1 "%02x"'`
# 6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76

dash-cli createrawtransaction \
  '[{"txid": "0ab375e71973bf814caab71334ce52a867af2544285ca8975d04102ec7b72c56", "vout": 1}]' \
  '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 100.0, "yX6kD415WGpwwDkb1AEgJettjj775KSSUZ": 899.99, "data": "6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}'

dash-cli signrawtransaction 0200000001562cb7c72e10045d97a85c284425af67a852ce3413b7aa4c81bf7319e775b30a0100000000ffffffff0300e40b54020000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0c15bf4140000001976a9147642779266a6eb356af5e324520fecfe1e0d4a5888ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

dash-cli sendrawtransaction 0200000001562cb7c72e10045d97a85c284425af67a852ce3413b7aa4c81bf7319e775b30a010000006a47304402200cb4ffb8d60a14b57fb0ecfb0f93d688965242eea5c1fc8eb96251f82e80faa3022036dd119884f24400b6ea1c1f85b3f582ddb1ba688456412b85020115c8ddfdc901210252e0f092042649eb84346301f334e8aa01ff9eaf2e5df235a0a74b5e3e2d7bafffffffff0300e40b54020000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0c15bf4140000001976a9147642779266a6eb356af5e324520fecfe1e0d4a5888ac00000000000000003c6a3a6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

######################################
# Create BCH Pool
######################################

# bitcoincash1
# ------------

bitcoin-cli -rpcuser=thorchain -rpcpassword=password -regtest getnewaddress
bitcoin-cli -rpcuser=thorchain -rpcpassword=password -regtest generatetoaddress 100 qrf8p5d6dnr7slrjvaztf8mkanxvdq0spgnv82439c
bitcoin-cli listunspent 1 99999999 '["qrf8p5d6dnr7slrjvaztf8mkanxvdq0spgnv82439c"]'

# echo "$(printf 'add:bch.bch:tthor1wep80ynx5m4n26h4uvj9yrlvlc0q6jjcsvnsmv' | hexdump -v -e '/1 "%02x"')"
# 6164643a6263682e6263683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76

bitcoin-cli createrawtransaction \
  '[{"txid": "fd5fe5faa4eeca8a3ec755f05e19c88775be27318131b4f4281ca9909546827d", "vout": 0}]' \
  '{"qqg2t4amlm90ahzhr5ywexfeh6kmguqp3y82lhg5fm": 10, "qr4s3xj5nt96dw3fy4r8dwge4vfqtg3h5vsc0gjfut": 39.99, "data": "6164643a6263682e6263683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}'

bitcoin-cli signrawtransactionwithwallet 02000000017d82469590a91c28f4b431813127be7587c8195ef055c73e8acaeea4fae55ffd0000000000ffffffff0300ca9a3b000000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0e55bee000000001976a914eb089a549acba6ba29254676b919ab1205a237a388ac00000000000000003a6a386164643a6263682e6263683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000

bitcoin-cli sendrawtransaction 02000000017d82469590a91c28f4b431813127be7587c8195ef055c73e8acaeea4fae55ffd000000006a473044022058dc5910b6d11cdcf4126e3c48901b73539797f7f528b2cb8ee595a4b037f8b40220085ef6f277a347c46d08aded6ebe3b1c64d515d905fa7ca9d7e54f034bb7e2ab412102767ef9a810c6bbab4b4a44211e0700779ec88ff4783de07d54b80cf612470814ffffffff0300ca9a3b000000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0e55bee000000001976a914eb089a549acba6ba29254676b919ab1205a237a388ac00000000000000003a6a386164643a6263682e6263683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d7600000000


# thornode1
# ---------

echo "password" | thornode tx thorchain deposit 100000000000 RUNE "add:bch.bch:qrf8p5d6dnr7slrjvaztf8mkanxvdq0spgnv82439c" \
  --from alex \
  --keyring-backend file \
  --chain-id thorchain \
  --gas 1000000 \
  --yes

######################################
# Swap BCH to DASH
######################################

# dash1
# -----

dash-cli getnewaddress

# bitcoincash1
# ------------

# echo "$(printf 'swap:dash.dash:yYzF2f15MUajWPWQaNG5D8FHiF888fAwPa' | hexdump -v -e '/1 "%02x"')"
# 737761703a646173682e646173683a79597a46326631354d55616a57505751614e47354438464869463838386641775061

bitcoin-cli listunspent

bitcoin-cli createrawtransaction \
  '[{"txid": "f44c3e609b88bf0e707fd6dae4e445c53cc3e2d2c53c5da4f8dc7466980113ba", "vout": 0}]' \
  '{"qqg2t4amlm90ahzhr5ywexfeh6kmguqp3y82lhg5fm": 1, "qr4s3xj5nt96dw3fy4r8dwge4vfqtg3h5vsc0gjfut": 48.99, "data": "737761703a646173682e646173683a79597a46326631354d55616a57505751614e47354438464869463838386641775061"}'

bitcoin-cli signrawtransactionwithwallet 0200000001ba1301986674dcf8a45d3cc5d2e2c33cc545e4e4dad67f700ebf889b603e4cf40000000000ffffffff0300e1f505000000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0ce0024010000001976a914eb089a549acba6ba29254676b919ab1205a237a388ac0000000000000000336a31737761703a646173682e646173683a79597a46326631354d55616a57505751614e4735443846486946383838664177506100000000

bitcoin-cli sendrawtransaction 0200000001ba1301986674dcf8a45d3cc5d2e2c33cc545e4e4dad67f700ebf889b603e4cf4000000006a4730440220446e19bdd4b25f3b974f32c2c42d70ad33c8e6381b405f135433e9d5f799d801022034fed473c28266cf5e4d8d1b8aaffffa2000e2136b7323a534705039905f642b412102767ef9a810c6bbab4b4a44211e0700779ec88ff4783de07d54b80cf612470814ffffffff0300e1f505000000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988acc0ce0024010000001976a914eb089a549acba6ba29254676b919ab1205a237a388ac0000000000000000336a31737761703a646173682e646173683a79597a46326631354d55616a57505751614e4735443846486946383838664177506100000000

# dash1
# -----

dash-cli getaddressbalance '{"addresses": ["yYzF2f15MUajWPWQaNG5D8FHiF888fAwPa"]}'

######################################
# Swap DASH to BCH
######################################

# bitcoincash1
# ------------

bitcoin-cli getnewaddress

# dash1
# -----

# echo "$(printf 'swap:bch.bch:qqpr38mj472ghs0d3msqllnzjjn0f20e7g49dmxn2e' | hexdump -v -e '/1 "%02x"')"
# 737761703a6263682e6263683a7171707233386d6a3437326768733064336d73716c6c6e7a6a6a6e306632306537673439646d786e3265

dash-cli listunspent

dash-cli createrawtransaction \
  '[{"txid": "9b150be21a88b7eeb779eeb33f6f1045b459cba107c758b02c9602bb4c0852c3", "vout": 0}]' \
  '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 2, "ygqx6u6aL2Q5peGEBGe2MWCeqZQWFLTpqd": 170.57, "data": "737761703a6263682e6263683a7171707233386d6a3437326768733064336d73716c6c6e7a6a6a6e306632306537673439646d786e3265"}'

dash-cli signrawtransaction 0200000001c352084cbb02962cb058c707a1cb59b445106f3fb3ee79b7eeb7881ae20b159b0000000000ffffffff0300c2eb0b000000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988ac402aadf8030000001976a914e12769fd384419e76253148bef3101e2e8ea3fb588ac0000000000000000396a37737761703a6263682e6263683a7171707233386d6a3437326768733064336d73716c6c6e7a6a6a6e306632306537673439646d786e326500000000

dash-cli sendrawtransaction 0200000001c352084cbb02962cb058c707a1cb59b445106f3fb3ee79b7eeb7881ae20b159b000000004847304402203745cc51dd97492e825f52b1787f88d0f64b93c5802e94b7ee14cbb7070cfcfe022052dacb88f8741a335880533e12a4b7672930cab811fa83abc6db5773894c6b1801ffffffff0300c2eb0b000000001976a91410a5d7bbfecafedc571d08ec9939beadb470018988ac402aadf8030000001976a914e12769fd384419e76253148bef3101e2e8ea3fb588ac0000000000000000396a37737761703a6263682e6263683a7171707233386d6a3437326768733064336d73716c6c6e7a6a6a6e306632306537673439646d786e326500000000


```

> {
>   "level": "error",
>   "error": "fail swap, not enough fee",
>   "msg": "753CDFEC1CC156005F6F04A46D4EE04245B8EF37587098896F246D01435AB5D0: ygqx6u6aL2Q5peGEBGe2MWCeqZQWFLTpqd ==> yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR (Memo: swap:bch.bch:qqpr38mj472ghs0d3msqllnzjjn0f20e7g49dmxn2e) 100000000 DASH.DASH (gas: [1571429 DASH.DASH])",
>   "time": "2022-01-20T22:52:49Z",
>   "message": "fail to swap"
> }

Was simply the out transaction not being large enough to cover fees. Doubled the
dash, everything a-ok.

Right. Now back to the notorious `node-launcher`. Trying on my local k8s with
just a dash and bch node. I left off with the ingress setup. Was trying to disable
every other node using config in `thornode-stack/values.yaml`, also modify the
usage requirements so things fit on my local machine.

`make install`
- stagenet
- genesis

Looking at the terraform diff it's clear I forgot to modify `bifrost/values.yaml`
as well...

I've modified my `bifrost.sh` startup script for my own `thorchain-cluster`. It
removes chains when generating the bifrost config file, to keep things clean.

Going to do the same with my `node-launcher` PR and propose the ability to
opt-out of chains.

Allows something like this:
```
LTC_HOST=none DOGE_HOST=none ETH_HOST=none BTC_HOST=none BINANCE_HOST=none ./bifrost-test.sh
```

Rebuilding image...  

`docker push registry.gitlab.com/alexdcox/thornode:stagenet-0.79.1`

If I continue with my `bifrost chain opt-out` feature, I'll need to update the
`node-launcher` to automatically set the bifrost host to none for all chains
where the daemon is disabled.
TODO: The above!

Don't even need to bother with setting up an ingress controller as lens provides
a way to do this quite easily.

```
docker run \
  --rm \
  -it \
  --name dash \
  --network host \
  --entrypoint bash \
  registry.gitlab.com/alexdcox/dash-core

# TODO: Find an easier way to get the host ip for the `rpcconnect` flag...
# apt install iputils-ping net-tools
# ping host.docker.internal
# 192.178.65.2

dash-cli \
  -rpcconnect=192.168.65.2 \
  -rpcuser=thorchain \
  -rpcport=56334 \
  -rpcpassword=password \
  getblockcount
```

Works! NICE.

`http://localhost:56641/thorchain/inbound_addresses`

> {
>   "error": "internal"
> }

O dear.  
Lots of errors happening on `thornode`. Most notably:  
`expected tthorpub, got sthorpub`  
It thinks we're running on testnet?  
I think this may be due to the way I actually built the container, unfortunately.  
Pretty annoying that you have to build the container at the binary level for the target network.  

Better. There's an inbound address. Can I set the network explorer up against this?  
No. There's no midgard. Added to `stagenet.yaml`. Running `make install`

> Error: UPGRADE FAILED: failed to create resource: Service "midgard-headless"
  is invalid: spec.ports[0].nodePort: Forbidden: may not be used when `type`
  is 'ClusterIP'

Don't think the `node-launcher` has been used with `NodePort` setup for a while.  
Lots of bugs with it.  

How about now?  

Also, for some reason, doge keeps sneaking back in. Need to pay attention to
that when I continue on from here tomorrow...

Ouch, 8 mins to spin up midgard. Perhaps I'll move back to using aws tomorrow.

```
kubectl -n thornode-stagenet get pods
kubectl -n thornode-stagenet exec --stdin --tty dash-daemon-7fd4cbdbf-f5w5j -- /bin/bash
```

Right, so stagenet probably isn't the way to go for me atm either.  
Moving to testnet.  

Right that's my day. Was tweaking configuration at the end there. I'm sometimes
confused as to when to use `testnet` and when to use `mocknet` in the helm
charts. They're becoming a bit like the makefile madness in my mind. Too much
composition. I get that it's nice to be able to configure things, I'd just
rather have copy-and-paste separate directories with static and
complete "recipes" than follow multiple variables down through inheritance and
overwritable paths down to the actual resulting values. Maybe I just don't know
helm enough, or maybe it would seriously reduce the cognitive load and make
everything easier. Who knows.

### 21.01.2022 Friday

Starting with the `cluster launcher` targeting aws...

```
export AWS_REGION=us-west-2
```

cluster name: thorchain  
cluster region us-west-2  

Now I need to set my default cluster.  
Already done.  

> Error: unable to build kubernetes objects from release manifest: unable to
  recognize "": no matches for kind "ServiceMonitor" in
  version "monitoring.coreos.com/v1"

Probably have to restore the NodePort/ClusterIP stuffs?

Redoing / dev checklist:
- [ ] comment out git clean/pull in `Makefile`
- [ ] update `thornode-stack` docker image versions (see `tag:`)
- [ ] enable/disable desired daemons in `thornode-stack/<network>.yaml`
- [ ] enable midgard for whatever network you're launching like:

     `thornode-stack/values.yaml` OR `thornode-stack/<network>.yaml`
     ```
      midgard:
        enabled: true
     ```

 - [ ] (optional) change disk/memory/cpu requirements as desired in `thornode-stack/values.yaml`
```
dash-daemon:
  fullnameOverride: dash-daemon
  service:
    type: NodePort
  persistence:
    size:
      testnet: 10Gi
  resources:
    limits:
      cpu: 0.5
      memory: 0.5Gi
    requests:
      cpu: 0.5
      memory: 0.5Gi
```

- [ ] update `bifrost/values.yaml` to disable unwanted chains:
```
litecoinDaemon:
  enabled: false
  mainnet: none
  testnet: none
  mocknet: none
  stagenet: none
```

- [ ] (temporary) Think the bifrost dashDaemon needs to be stripped of `http://` prefix
```
dashDaemon:
  enabled: true
  mainnet: dash-daemon:9998
  testnet: dash-daemon:19998
  mocknet: dash-daemon:19898
  stagenet: dash-daemon:9998
```

- [ ] Find and replace official image with development image:
`registry.gitlab.com/thorchain/thornode`
`registry.gitlab.com/alexdcox/thornode`

-----

Right I've just checked out the original `add-dash` branch on `node-launcher`.  
I'm using the default `cluster-launcher` setup.  
So in theory, this should be good to go.  

In practise, I'll at least have to update the docker image versions again...

I got the `no matches for kind "ServiceMonitor"` error again.

Pulling in changes from `master` (there is no `develop`)

AH. Just noticed this:

```
{{- if not .Values.dogecoinDaemon.enabled }}
- name: DOGE_DISABLED
  value: "true"
{{- end}}
```

It's very new, and it facilitates the "omit out of a chain" feature that I
added. Unfortunately, it only works for doge. I'd like to start a new thorchain
using an arbitrary list of chains. Hmmmm. I can either redo what I have and
carry that accross all chains in this new style, or replace the new style with
my bifrost config method. I think it's usually best to go with the flow of the
primary maintainers.

Lets first see what the limitations are using a hybrid of both.  
NOTE: `bifrost/templates/deplotment` is where the merge conflict was.  
Getting seriously blocked by that "ServiceMonitor" problem. Focusing on that.  

`make tools`

Perfect, now I'm getting a proper helm diff.  
`dogecoin-daemon` is in the list.  

There's a very subtle typo `condition: dogecoin-daemon.enabledd`.  
Could that be it?  
Yeah, that was it.  

Alright now working through the issues with the default config.

Wow, another aws node was automatically spun up. Will that one handle bifrost?
It did. Auto aws bill spanking.  
Love it.  
Waiting for bifrost do its finishing touches...  
Oh `init-binance` is running.  
That's never going to work because I disabled binance.  
The binance init config in `bifrost/templates`

Big ol list of problems:
- bifrost insufficient cpu
  (this one auto resolves, although the cpu reservation is so astronomical that
  it forces a new node to be created without a single node having more than 40%
  cpu utilisation, are we absolutely sure we can't squeeze the bifrost in
  without spinning up another node?)
- typo in dogecoin definition
- init-binance doesn't have a `.enabled` conditional block
- init-dash stuck on `waiting for dash`


```
curl -sL \
  --fail \
  --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' \
  -H "content-type: text/plain;" http://thorchain:password@localhost:19998
```

```
curl -sL \
  --fail \
  --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' \
  -H "content-type: text/plain;" http://thorchain:password@localhost:62909
```

```
curl -i -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@dash-daemon:19998
curl -i -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@localhost:19998
curl -i -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@172.20.240.220:19998
curl -i -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@localhost:19998
curl -i -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@localhost:62909

curl -i -sL http://thorchain:password@localhost:19998
curl -i -sL http://thorchain:password@dash-daemon:19998
curl -i -sL http://thorchain:password@172.20.240.220:19998
curl -i -sL http://thorchain:password@10.0.18.158:19998
```

`netstat -npl tcp` confirms it: `127.0.0.1:19998`

The rpc port is bound for local traffic only. The way `lens/kube` configures
port forwarding to my machine must be some kind of ssh tunnel where the pod
thinks my traffic is actually local. That would explain how I can reach the
endpoint from my dev laptop but not from within the aws node using the pod
cluster ip.

Okay so just need to find the dash config responsible and update.

`cat ~/.dashcore/dash.conf` has
```
rpcbind=0.0.0.0
rpcallow=10.0.0.0/8
```

My node ip is `10.0.18.158`

Can I open up two shells into that pod via my terminal (not lens)  
Ah yes it was `krew` for `kubectl`, I already have it.  

```
kubectl node-shell ip-10-0-25-41.us-west-2.compute.internal
docker ps | grep dash
docker inspect 2a87c39e8f74
netstat -nplt
docker exec -it 2a87c39e8f74 bash
```

I think the problem is with `dashd`, which is confusing because I've set
`rpcbind`. What do the dash docs say on it?

```
mkdir /tmp/dash

dashd \
  -regtest \
  -datadir=/tmp/dash \
  -rpcbind=0.0.0.0:7777 \
  -rpcallowip=0.0.0.0/32 \
  -printtoconsole
```

That works as expected. Port 7777 open to external traffic from any foreign
address.

```
rm -rf /tmp/dash/
mkdir /tmp/dash
cp ~/.dashcore/dash.conf /tmp/dash/
apt update && apt install vim
vi /tmp/dash/dash.conf
```

Oh. I think it just clicked. The `rpcbind` address of `0.0.0.0` was outside the
`rpcallowip` CIDR range to start with, so perhaps it recognised a dodgy config
and just defaulted to `127.0.0.1`?

```
dashd -datadir=/tmp/dash -conf=/tmp/dash/dash.conf
```

Nope.

AHHHH
> Warning: Config setting for -rpcbind only applied on regtest network when in [regtest] section.

Alright that'll be it then. IMHO this is an unnecessary hoop to jump through.
Configuration at the global level should just be accepted. Config at a lower
level should override. We're being overly safe in requiring that to be network
specific.

Rebuilding `registry.gitlab.com/alexdcox/dash-core` with updated scripts...  
Uploading to gitlab registry...  

Don't forget, the k8s node will NOT fetch the new image unless the tag changes.

```
docker pull registry.gitlab.com/alexdcox/dash-core
```

```
docker ps --filter name=k8s_dash-daemon -q
docker logs -f $(docker ps --filter name=k8s_dash-daemon -q) | head -n 1000
docker exec -it $(docker ps --filter name=k8s_dash-daemon -q) bash
```

Well, it's running... It restarted 3 times before calming down and cooperating.  

```
curl -i -sL --fail --data-binary '{"jsonrpc": "1.0", "id": "node-status", "method": "getblockchaininfo", "params": []}' -H "content-type: text/plain;" http://thorchain:password@dash-daemon:19998
```

Oops was in:  
`~/go/src/github.com/alexdcox/thorchain-dash-core`  
needed:  
`~/go/src/gitlab.com/thorchain/devops/dash-core`  

Rebuilding... uploading... downloading...  restarting pod...  Okay dash debug
logs are insane. Trillions of debug lines speeding past your eyes at the speed
of light. I'm disabling that and restarting. This is going to cane disk io and
space.

Rebuilding... uploading... downloading...  restarting pod...

```
docker run --rm -it registry.gitlab.com/alexdcox/dash-core bash
```

```
docker inspect $(docker ps  | awk '{print $2}' | grep -v ID) | jq .[].RepoTags
```
It's not using `latest`.

`make destroy-aws`
Will have to come back to this later g2g...

Right coming back to this. The cluster didn't shutdown cleanly, as usual. Do I
have a checklist somewhere? Couldn't find it. Lets work through...

You can go into `AWS Resource Groups > Tag Editor` and search all tags with:  
```
key                                        value
Name                                       thorchain
kubernetes.io/created-for/pvc/namespace    thornode-testnet
ebs.csi.aws.com/cluster                    true
```

Thornode vpc is `vpc-0cb4...`

Reworked my aws teardown checklist a bit.

Two blatant issues with the AWS Resource Groups Tag Editor / tag features. Why
on earth haven't these been added / addresses already?
1) When creating a group, you can only do AND tag matching, you can't do OR tag
matching. Solution: have OR matching, and multiple "sets" of tags.
2) When searching for leftover resources, the eventually consistent nature of
the service means you match loads of resources which no longer exist.
Solution: double check the resources exist, obviously. Either silently in the
background, or at the press of a button.  
Grrr.

It's worth noting you can use this to scan ALL RESOURCES FOR ALL REGIONS in one
place. That is decent. Okay I think I'm back to a clean region. There are 12
default resources (of any type).

Spinning up the cluster...

`waiting for dash`

```
kubectl node-shell ip-10-0-38-182.us-west-2.compute.internal
docker exec -it $(docker ps --filter name=k8s_dash-daemon -q) bash
apt install net-tools
netstat -nplt
```
```
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:19998         0.0.0.0:*               LISTEN      16/dashd
```

`cat ~/.dashcore/dash.conf`

It has the `rpc`

`docker logs -f $(docker ps --filter name=k8s_dash-daemon -q) | head -n 1000`

> Binding RPC on address ::1 port 19998 failed.

Oh. Why?

Will regtest work?

```
dashd -datadir=/tmp/dash -conf=/tmp/dash/dash.conf
```

Yep. I copied the exact same configuration and just changed `testnet` to
`regtest` and it worked. They're all being run from the `root` user, no
difference there.

Right I'm going to modify the docker image on the actual k8s node so that I can
iterate quickly and hopefully trial-and-error a solution quickly.


```
docker run \
  -it \
  --rm \
  --name temp \
  --entrypoint bash \
  --network host \
  registry.gitlab.com/alexdcox/dash-core:v0.17.0.3

apt update && apt install net-tools iputils-ping vim -y
vi /scripts/entrypoint-testnet.sh

docker commit temp registry.gitlab.com/alexdcox/dash-core:v0.17.0.3
```

All I did was change it to regtest, as with I did earlier. Want to rule out
binding too quickly / before the network interfaces are ready or something like
that.

```
docker rm -f $(docker ps --filter name=k8s_dash-daemon -q)
docker ps --filter name=k8s_dash-daemon -q
docker logs -f $(docker ps --filter name=k8s_dash-daemon -q) | head -n 1000
docker exec -it $(docker ps --filter name=k8s_dash-daemon -q) netstat -nplt
docker exec -it $(docker ps --filter name=k8s_dash-daemon -q) cat /dash/.dashcore/dash.conf
```

> WARNING: option -rpcallowip was specified without -rpcbind; this doesn't usually make sense  

(love the hint, wish you could see I've clearly set that)

> libevent: getaddrinfo: address family for nodename not supported  
> Binding RPC on address ::1 port 19998 failed.  

```
docker run \
  --rm  \
  registry.gitlab.com/alexdcox/thornode
```

Need to continue with that docker run command on monday. For some reason
`testnet` is not playing ball when it comes to reading `rpcbind` and
`rpcallowip`. Maybe there's a bug there. I'm running the latest version of dash
so if there is a fix it hasn't been released yet.

Things I've already tried:
- switching from testnet to regtest (which works as expected)
- adding `rpcbind` and `rpcallowip` to both global and network level config within config file.

Some things to try:
- passing flags directly on the command line
- messing with docker network and ports (although the `WARNING` log makes me think this is a dash issue)
- looking for these config vars in the dashpay/dashd source code (bug hunt)

`make destroy-aws`

audi5k.


### 24.01.2022 Monday

Ah need to fully clear the previous cluster. Some NIs left over.
Okay fresh cluster.

Back to trying to get `testnet` rpc port configured properly with dash.

Is there a fast way to get the name of the node which is running the dash service?

```
kubectl -n thornode-testnet get services --filter dash-daemon
kubectl -n thornode-testnet get services dash-daemon
kubectl -n thornode-testnet get pods dash-daemon

# get the namespace (testnet/mainnet/stagenet)
kubectl get namespaces | awk '/thornode-*/{print $1}'

# get the node name
kubectl get pods -o wide -n thornode-testnet | awk '/dash-daemon*/{print $7}'

# all-in-one shell into whatever node is running the dash pod
kubectl node-shell $(kubectl get pods -o wide -n $(kubectl get namespaces | awk '/thornode-*/{print $1}') | awk '/dash-daemon*/{print $7}')
```

Ahh found it. Network needs to be `test` not `testnet`. Just needed a fresh pair of eyes.

Sweet, cluster is ALL GREEN.

Unfortunately, there's not a configuration for `mocknet` on the node-launcher
any more. I'd like it back so I can test a swap. Perhaps not worth the effort
though, it'll get tested soon enough.

Going to clean up what I have and push.
Separating into specific commits:
- Allow binance daemon to be disabled
- Fix dashDaemon urls in bifrost values
- Fix typo in dogecoin-daemon

Okay merge request updated:
https://gitlab.com/thorchain/devops/node-launcher/-/merge_requests/361

Just 2.5 hours clocked for today on dash. Going to switch over to Decred and get
it up to this step before switching back to dash.

### 26.01.2022 Wednesday

I've received some troubling feedback from Pluto for the `thornode` repo:
- He asked me to revert a bugfix in `pubkey2address` which added mocknet support
- `dashd-go` he wants me to have my changes merged into the official `dashd-go`.

Looks like I need to get my changes added to the official repo:
`github.com/dashevo/dashd-go`

Will need to talk with QuantumExplorer. Ahh, discord is having an api outage.  
And the world grinds to a halt.

I remember having some github related problems before trying to for the dashd-go
project. That's why my repo isn't technically a fork, it's a modified clone.
Getting my changes into the original might be tricky.

github.com/dashevo/dashd-go  
github.com/alexdcox/dashd-go  

Maybe I'll delete my dashd-go and change it to dashd-go-clone or something.  
Then fork the official dashd-go.

> You've already forked dashd-go
> alexdcox/btcd

Damn. That was the issue. Github thinks I've forked `dashevo/dashd-go` to
`alexdcox/btcd` when that is forked from `btcsuite/btcd`, as you would expect.
It even says that if you click through to `alexdcox/btcd`. What the hell?

Oh this is why:  
github.com/btcsuite/btcd -> github.com/alexdcox/btcd  
github.com/btcsuite/btcd -> github.com/dashevo/dashd-go  

So I can replace alexdcox/btcd with dashevo/dashd-go  
`mv btcd btcd-backup`  
Just going to leave that there for now and delete my `btcd` repo.  

I want to do something like this:
```
git difftool HEAD..file://../dashd-go-clone
```

Maybe I can add it as a remote?

```
git remote add clone ../dashd-go-clone
git remote update
git diff master remotes/clone/master
```

NICE. Now with the difftool?

```
git difftool master remotes/clone/master
```

Okay 250 off files. Fun times. Need to make sure I replace:  
github.com/btcsuite/btcd  
with  
github.com/dashevo/dashd-go  


The problem I'm having is there's a circular dep between btcsuite/btcd and
btcsuite/btcutil which essentially means you have to recreate both, updating
one and not the other will just break because at some point it uses a function
from the other which in turn calls back to the current package which is now
at a different package path.

I could try including `dashutil/btcutil` IN `dashd-go/btcd`. Then I could do a
find and replace:  
`btcsuite/btcutil` -> `dashevo/dashd-go/dashutil`

Can these be left as the original btcsuite ones?  
btcsuite/btclog  
btcsuite/btcec  
btcsuite/btcwallet  
btcsuite/btcrpcclient  
btcsuite/go-socks  
btcsuite/goleveldb  
btcsuite/websocket  
btcsuite/Paymetheus  
btcsuite/snappy-go  

Right fixed those paths. Running tests. Lots of failures. I see from July last
year that I already commented out a load of broken tests.

Maybe we can fix all the broken copyright years?  
Find  
[Cc]opyright( \(c\))? (\d+-\d+|\d+, ?\d+|\d+).*(dashevo|Dash Core)  
Replace:  
Copyright (c) 2022-2032 The $3  

I didn't bother in the end, seems silly to worry about it. If it were me I'd
remove all those copyright banners. Seems very 1990s to copy that into every
single file when you can just have a `LICENSE` at the root directory. It's not
as if adding it to every single goddamn file makes a blind bit of difference
anyway, apart from bloating the entire project.

Oh interesting. alex@akselrod.org ported some code form Decred back in 2017, it
made its way into Dash. They're more closely related than I knew.

- add chainlock/instantlock
- remove client.BackendVersion getinfo (no longer part of dashd)
- Update chainparams for Dash, remove simnet
  This originally included getting `go test` working.  
  New plan, I'm not going to comment out the broken tests. I'll just ignore them.
- Remove getinfo rpc command
  Just wanted to double check this was the right thing to do:
  `dash-cli getinfo`
  > This call was removed in version 0.16.0. Use the appropriate fields from:

Okay I have a PR here:  
https://github.com/dashevo/dashd-go/pull/5

Was going to write this but I think maybe it's a bit much:

It's worth noting that `dashevo/dashd-go` was intentionally a full dash node
written in golang, however I don't think the project was ever finished and it
hasn't been maintained. There are many things that would need addressing to
meet the original project goals. My PR just changes as little as possible in
order to meet the needs of the Thorchain integration including:
- changing package paths to match the fork url
- updating chaincfg params
- removing rpc calls that are no longer available
- adding struct fields for the newer chainlock/instantsend features
For this reason I'm not sure how it will be received...

I'm just going to wait to see what comes back from that PR... hopefully a green
light.

Wrote a message on the Dash discord under dash-core-group. Prompting for info.

Run out of things to do for now...

### 27.01.2022 Thursday

Brian Foster Requested:  
TODO: Take a look at adding dash to the TC LP Calculator:  
https://science.flipsidecrypto.com/thorchain/  

Right so reworking the `thorchain-integration` branch of `dashd-go` so there is
a single commit with the find and replace, along with a script to do that work
so they can reproduce it.

```
gco -b thorchain-integration2
git reset HEAD^1 --hard
git reset HEAD^1 --soft
```

Remove simnet  

```
btcsuite/btcd      dashevo/dashd-go
btcsuite/btcuitl   dashevo/dashd-go/dashutil
```

`gd thorchain-integration2 thorchain-integration`

- [ ] Add package dashevo/dashd-go/dashutil

  ```
  gco thorchain-integration -- dashutil
  gcam "Add package dashevo/dashd-go/dashutil"
  ```

- [ ] Update package paths: btcsuite/btcd to dashevo/dashd-go and btcsuite/btcutil to dashevo/dashd-go/dashutil

  Command on mac:
  ```
  find . -type f -name '*.go' -exec gsed -i "s+btcsuite/btcd+dashevo/dashd-go+g" {} \;
  find . -type f -name '*.go' -exec gsed -i "s+btcsuite/btcutil+dashevo/dashd-go/dashutil+g" {} \;
  find . -type f -name '*.go' -exec gsed -i "s+btcutil\\.+dashutil.+g" {} \;
  ```
  
  Commit message (sed not gsed):
  ```
  Update package paths: btcsuite/btcd to dashevo/dashd-go and btcsuite/btcutil to dashevo/dashd-go/dashutil
  
  This commit can be reproduced with the following commands:
  find . -type f -name '*.go' -exec sed -i "s+btcsuite/btcd+dashevo/dashd-go+g" {} \;
  find . -type f -name '*.go' -exec sed -i "s+btcsuite/btcutil+dashevo/dashd-go/dashutil+g" {} \;
  find . -type f -name '*.go' -exec sed -i "s+btcutil\\.+dashutil.+g" {} \;
  ```

- [ ] Update chainparams for dash

  ```
  git show --stat 69ecae80
  ```

  ```
  gd thorchain-integration2 thorchain-integration -- '*.go'
  ```

  These are the only main changes:
  - chaincfg/params.go
  - cmd/btcctl/config.go
  - wire/protocol.go

  Going to convert the decimal representations to hex to match the original
  format.

  ```
  git difftool thorchain-integration2..thorchain-integration -- chaincfg/params.go cmd/btcctl/config.go wire/protocol.go
  gcam "Update chainparams for dash"
  ```

- [ ] Remove getinfo rpc command

  - rpcclient/infrastructure.go
  - rpcclient/wallet.go

  ```
  git difftool thorchain-integration2..thorchain-integration -- rpcclient/infrastructure.go rpcclient/wallet.go
  gcam "Remove getinfo rpc command"
  ```

+2hrs. Most of today was other admin.

### 28.01.2022 Friday

Still being blocked by: https://github.com/dashevo/dashd-go/pull/6

Need to address these questions:

--------------------------------------------------------------------------------

Hi @xodus3 just been looking at your patch for bifrost. Looks fine, although I'm
not an expert on Dash specifics. So just putting it to you some hypotheticals
that all need to be covered off that are dangerous. Make sure these are not
possible:

> Can a customer send a tx that Bifrost observes inbound to an asgard vault, but
  the customer can later spend or remove. Like a coin on a string in a vending
  machine. Examples include observing in mempool then user replace-by-fee the
  tx elsewhere. 

Dash doesn't support RBF. After talking with the Dash devs I'm going to switch
the chainclient from chainlock-only to behave the same way other clients
do *until* we see a chainlock - in which case we can immediately consider the
transaction confirmed.

> Can a user send poisoned tokens that cannot be spent by asgard later. For
  example timelocked. Is there anything dash-specific here?

Dash supports locktime, but the bifrost client is set to ignore transactions
which have a non-zero locktime (as is the case with the other clients) There's
also sequence number, but it's my understanding sequence numbers only come into
play when locktime is used.

> Can the user specify an address to send outbound that is not observed by
  Bifrost. For example user does a swap from BTC to DASH and
  specifies "eviladdress" that is a real address but Bifrost doesn't see the tx
  outbound. Resulting in TC trying again and user getting a double-spend
  output. Examples here might include custom address formats for fast payments
  or something the dash client recognises but Bifrost isn't looking for when
  scanning blocks. OR fast payments not even included in a block... but sent.
  Or a txOut goes into a block with no chainlock, and is not observed (is that
  a thing?)

There aren't any custom addresses.  

We're going to adopt the bitcoin "weighted confirmation requirement by
transaction size" approach by default, and drop the confirmation requirement
completely if and when we see the block for that transaction becoming
chainlocked.

I've got to restore some of the typical chainclient code here.

> Similar for outbounds: Replace By Fee would allow a THORChain node to have
  their outbound "observed" as being sent, but then be able to steal from
  customer.

We're covered here. No RBF.

> There is no way for a recipient to "block" incoming funds?

Nope.

> Have the supply chain attack surface area from Pluto been addressed?

If you're talking about 3p deps - changing from github/alexdcox to
github/dashevo, that's being reviewed by the dash devs at the moment. Otherwise
I'm not clued up just yet.

> I assume latest develop has been merged in (I think so)?

Yeah I've been continually merging dev. I'll keep checking... feel free to nudge
me and I'll get on it.

> Just checking this works...

Have you checked or are you saying you'd like me to check it?

> Otherwise all looks good. 

Brilliant! Will let you know when I've made this next update,.

--------------------------------------------------------------------------------

Got to add the old chainclient config back.

TODO: Is this right?
```
DefaultCoinbaseValue   = 10000
```

I found a way to turn off logging before. How did I do that?

### 03.02.2022 Thursday

How often is `dashclient/GetConfirmationCount` called?

```
curl -i --user thorchain --data-binary '{"jsonrpc": "1.0", "method": "getblockchaininfo"}' http://localhost:28443/
```
> curl: (52) Empty reply from server

What's up with BCH?  
It was something to do with my temperamental cluster orchestrator. Restart sorted it.  

Keep getting `fail to sign keysign` errors.  
> ERR fail to sign keysign error="The specified item could not be found in the keyring"

What item?!  
Keeps happening after block 5.  

```
  if txs != nil && (txs.TxArray == nil || len(txs.TxArray) < 1) {
    fmt.Println("assuming no transactions, silently continuing")
    return nil, nil
  }
```
The above snippet calms that down when added to `queryKeysign`. Not entirely sure
if it's the correct approach though.

Right back to the question at hand...

```
error="fail to post network fee to thornode: fail to broadcast to THORChain,code:32, log:
github.com/cosmos/cosmos-sdk/x/auth/ante.SigVerificationDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/sigverify.go:242
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.SigGasConsumeDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/sigverify.go:157
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.DeductFeeDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/fee.go:98
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.ValidateSigCountDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/sigverify.go:352
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.SetPubKeyDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/sigverify.go:93
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.RejectFeeGranterDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/fee_grant.go:26
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.ConsumeTxSizeGasDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/basic.go:142
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.ValidateMemoDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/basic.go:66
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.TxTimeoutHeightDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/basic.go:199
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/types/handler.go:40
github.com/cosmos/cosmos-sdk/x/auth/ante.ValidateBasicDecorator.AnteHandle
  /Users/adc/go/pkg/mod/github.com/cosmos/cosmos-sdk@v0.42.1/x/auth/ante/basic.go:34
github.com/cosmos/cosmos-sdk/types.ChainAnteDecorators.func1
  /Users/adc/go/pkg/mod/github.com/co
```
wow.

Here's a quick command to just send a dash deposit to thorchain.  
Need to rinse this command because I'm testing confirmation counts.  
```bash
dothedash() {
  txid=$(dash-cli sendtoaddress yX6kD415WGpwwDkb1AEgJettjj775KSSUZ 1000)
  rawtx=$(dash-cli createrawtransaction \
    "[{\"txid\": \"$txid\", \"vout\": 1}]" \
    '{"yMqULE4YJ7g3sUGu8ZNDofbJaCqaW92JtR": 100.0, "yX6kD415WGpwwDkb1AEgJettjj775KSSUZ": 899.99, "data": "6164643a646173682e646173683a7474686f72317765703830796e78356d346e3236683475766a3979726c766c633071366a6a6373766e736d76"}')
  signed=$(dash-cli signrawtransaction $rawtx | jq -r '.hex')
  dash-cli sendrawtransaction $signed
}
```

```
@dash/GetConfirmationCount
  + 343151ed499202a551a4bf0ad7b7cfa5571164c58430e17ddeb8d413f0cd22a7

@dash/getBlockRequiredConfirmation
  + 343151ed499202a551a4bf0ad7b7cfa5571164c58430e17ddeb8d413f0cd22a7
totalTxValue:        10000000000
totalFeeAndSubsidy:  21447957294
confirm:             0
confirmation required 0

@dash/ConfirmationCountReady
  + 343151ed499202a551a4bf0ad7b7cfa5571164c58430e17ddeb8d413f0cd22a7
ready? true
```

`10000000000 / 21447957294 = 0.46624487`

The fee is so ridiculously large that we don't bother with confirmations, apparently.  
Okay how does this look with a minimum fee?  
Actually the fee is only `0.01` for my tx, so where did it get `214.47957294` from?  
It's the coinbase value of the block.

`dash-cli getblock 2e536618f4e070d6835065b03055f25c56c695e7a83bedefb1804893b1622239`  
`dash-cli getblock 2e536618f4e070d6835065b03055f25c56c695e7a83bedefb1804893b1622239 2`  
`dash-cli getrawblock 2e536618f4e070d6835065b03055f25c56c695e7a83bedefb1804893b1622239 2`  

```
"258ef86e81a7cd3130e97e696bcf1ad5038f2cd1366f8a79c1ba45e4d5358941",
"b9f29870069e4c4e425f9038cc836c46d6de61589f0f8775084c14c7749729cf",
"343151ed499202a551a4bf0ad7b7cfa5571164c58430e17ddeb8d413f0cd22a7"
```

`dash-cli gettransaction 258ef86e81a7cd3130e97e696bcf1ad5038f2cd1366f8a79c1ba45e4d5358941`  
`dash-cli gettransaction b9f29870069e4c4e425f9038cc836c46d6de61589f0f8775084c14c7749729cf`

`97.37372612 + 117.10584682 = 214.47957294`

Okay there it is.  
So my transaction was `100 DASH` the block coinbase total was `214.48 DASH` so 
therefore because my transaction was `100 / 214.48 = 0.47` which as an int is 0,
we don't need any confirmations. So the transaction size needs to be greater than
the block coinbase value before it needs confirmations. Does that ever happen?

Alright that's all a bit crazy to me,. I'm going to manually set
confirmations to be 5, unless we see an instant lock, and see what the
efficiency of that is:

```
@dash/GetConfirmationCount
no transactions = no confirmations

@dash/ConfirmationCountReady
no tx = ready

@dash/GetConfirmationCount
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
confirmation required 5

@dash/ConfirmationCountReady
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
ready? false

@dash/ConfirmationCountReady
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
ready? false

@dash/ConfirmationCountReady
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
ready? false

@dash/ConfirmationCountReady
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
ready? false

@dash/ConfirmationCountReady
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
ready? false

@dash/ConfirmationCountReady
  + 035502848ce4323b060cdff1256ce9cbad532fecc6f5ad2bcc70f3bb18a1a51d
ready? true
```

The above was me setting a hardcoded confirmation requirement of 5.

```
@dash/GetConfirmationCount
block height: 1947
  + 1c9f482198f64da8f0eea79b23f972102a62c40b4c0c0e3ce437b32bc4c30220
confirmation required 5

@dash/ConfirmationCountReady
block height: 1947
  + 1c9f482198f64da8f0eea79b23f972102a62c40b4c0c0e3ce437b32bc4c30220
ready? true
```

That's weird. Went straight to ready.

```
@dash/GetConfirmationCount
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
confirmation required 5

@dash/ConfirmationCountReady
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
current block height: 2002
tx block height:      2002
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
current block height: 2003
tx block height:      2002
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
current block height: 2004
tx block height:      2002
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
current block height: 2005
tx block height:      2002
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
current block height: 2006
tx block height:      2002
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
block height: 2002
  + 1c6d2a988ab9024816b53010770c8b4260895245ac94ea1c29aa288f37b38d0d
current block height: 2007
tx block height:      2002
confirmations req:    5
ready:                true
```

Okay with a bit more logging that's starting to make sense. Right so what I'm
seeing is, the `GetConfirmationCount` method which tells the bifrost how many
confirmations to wait for is only called once. I did suspect this. Now the
question is how best to go about checking that again. Wait let's check the
chainlock parameter first.

```
@dash/GetConfirmationCount
block height: 2083
  + d81a7c2600fdc4d3dcf66653dc4e408699f83057d506deccd248a67b3720612d
block chainlocked: true

@dash/ConfirmationCountReady
block height: 2083
  + d81a7c2600fdc4d3dcf66653dc4e408699f83057d506deccd248a67b3720612d
current block height: 2083
tx block height:      2083
confirmations req:    0
ready:                true
```

Okay that worked as expected. By the time we queried the block, it had been
chainlocked.

2 in a row. 3. 4. 5. Hmm my private network in regtest is chainlocking these too
fast. I'll try killing 3/4 dash nodes and then see what happens.

```
docker stop dash2 dash3 dash4
```

```
@dash/GetConfirmationCount
block height: 670
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
block chainlocked: false
confirmation required 5

@dash/ConfirmationCountReady
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
current block height: 670
tx block height:      670
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
current block height: 671
tx block height:      670
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
current block height: 672
tx block height:      670
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
current block height: 673
tx block height:      670
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
current block height: 674
tx block height:      670
confirmations req:    5
ready:                false

@dash/ConfirmationCountReady
  + bbc9414cded06127141492704247cee6e17f7b28a181bfc17c5749b252f1bc82
current block height: 675
tx block height:      670
confirmations req:    5
ready:                true
```

Okay that looks like it's behaving nicely.

Notes:
- If the chainlock is slow we'll be using confirmation counts
- The confirmation count will usually be 0 because of the crazy math behind `GetConfirmationCount`
  (the same way all the other clients calculate this)

Suppose I should test this with outbound transactions too.
- [ ] test swap with llmq
- [ ] test swap without llmq

Ah. The midgard docker container can't connect to the thornode instance I'm 
running bare metal. Of course. Maybe I should do net=host and just use localhost
to cover both situations?

Setting the `MIDGARD_LISTEN_PORT: 7777` doesn't seem to be making a blind bit of
difference. https://gitlab.com/thorchain/midgard/-/tree/develop/config/examples
is lying to me.

Actually it is listening on 7777 but only ipv6. Great.

Using `http://[::1]:7777/` in chrome, still nothing.

https://github.com/docker/for-mac/issues/1432
> No, it won't work. I just tried. Docker for mac runs in a very special type of
  separate network which prevents ipv6 from working at alljj.

Midgard is on busybox too so I can't do any `socat` magic. Argh. Why doesn't it
just bind to ipv4 ffs.

Okay I'm going to rebuild `midgard` with alpine so I can use `socat` to redirect
ipv4 traffic to ipv6 listen address.

```
docker build -t registry.gitlab.com/thorchain/midgard:develop .
docker run -it --rm --name tt --entrypoint sh registry.gitlab.com/thorchain/midgard:develop
```

### 08.02.2022 Tuesday

So it seems like providing the `entrypoint` in a docker compose file causes the
default `command` to be ignored. I suppose that makes sense, I was just relying
on not having to find and copy it.

> On MacOS, --net=host does not work for allowing your container process to
  connect to your host machine using localhost. Instead, have your container
  connect to the special MacOS only hostname docker.for.mac.host.internal
  instead of localhost. No extra parameters are needed to docker run for this
  to work. You can pass this in as an env var using -e if you want to keep your
  container platform agnostic. That way you can connect to the host named in
  the env var and pass docker.for.mac.host.internal on MacOS and localhost on
  Linux.
> latest hostname for mac is `host.docker.internal`

> socat[625] E connect(5, AF=10 [0000:0000:0000:0000:0000:0000:0000:0001]:7777, 28): Address not available

```
pkill socat
socat TCP4-LISTEN:8080,fork TCP6:[::1]:7777,fork
socat TCP4-LISTEN:8080,fork TCP4:localhost:7777,fork
```

OKAY. Midgard, check. Network explorer, check. Lets run a goddamn test already.

- [ ] with llmq  
TC seems to be having trouble sending the dash tx.

I think this has something to do with the `The specified item could not be
found in the keyring` error we saw before.

Updating branch to match dev. Think it's triggered by the bifrost sending
an rpc request. Perhaps MsgSolvency.

Do we get the message on my working cluster? Well, I'm inundated with errors
now so I can't tell:

```
{"level":"error","rune in module":0,"rune in pools":0,"time":"2022-02-08T21:08:07Z","message":"cannot migrate with a zero amount"}
{"level":"error","error":"fail to prepare outbound tx: insufficient funds for outbound request: 0x340b94e5369cEDe551a117960c75547eA84eAEdE 60000000 remaining","time":"2022-02-08T21:08:07Z","message":"fail to schedule refund MKR transaction"}
{"level":"error","error":"cannot add bond while node is active or ready status: 1 error occurred:\n\t* internal error\n\n","time":"2022-02-08T21:08:19Z","message":"msg bond fail validation"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T21:08:19Z","message":"keeper error"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T21:08:19Z","message":"fail to add fee to reserve"}
{"level":"error","error":"cannot add bond while node is active or ready status: 1 error occurred:\n\t* internal error\n\n","time":"2022-02-08T21:08:19Z","message":"msg bond fail validation"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T21:08:19Z","message":"keeper error"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T21:08:19Z","message":"fail to add fee to reserve"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T21:08:26Z","message":"msg set version failed validation"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T21:08:26Z","message":"msg set version failed validation"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T21:08:31Z","message":"msg set version failed validation"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T21:08:31Z","message":"msg set version failed validation"}
```

On and off again? Same thing happened. It's probably the `--gas X` flag now
being required for every `thornode tx` command. Would love a justification
for that.

With the flag, we move on to `cannot add bond while node is active or ready...`

Rebuilding the docker image (this time with a version tag)  
Deleted everything docker. Updated. Rebuilt just one image with specific
net-version tag. Updated scripts to use this new tag for v0.80.

Is it worth rolling back to 0.79 to double check my cluster scripts? Losing
faith I haven't messed those up...

Getting `0.72.0` node version logged in genesis from other node. Looks like
somewhere I'm fetching the old image again.

```
git pull --tags
gco v0.79.1
./_adc/docker-build-image.sh
THORNODE_IMAGE=registry.gitlab.com/thorchain/thornode:mocknet-0.79.1 ./thornode.sh
```

Still seeing `0.80.0`. Bit of refining to do here.

`docker run --rm registry.gitlab.com/thorchain/thornode:mocknet-0.79.1 thornode version`

Having a mismatch between `registry.gitlab.com/thorchain` and `/alexdcox`.

```
docker run --rm registry.gitlab.com/alexdcox/thornode:mocknet-0.79.1 thornode version
THORNODE_IMAGE=registry.gitlab.com/alexdcox/thornode:mocknet-0.79.1 ./thornode.sh
```

```
{"level":"error","error":"vault with pubkey(tthorpub1addwnpepqfrsx4rcnch7m3qd6n6g6y0mmuujjxpjy3nlts2kpzn5cazc5xmtxf54f3p) doesn't exist: vault not found","time":"2022-02-08T23:38:05Z","message":"fail to retrieve vault"}
{"level":"error","error":"vault with pubkey(tthorpub1addwnpepqtgv8rnpv4nkevjcagmr9ky6v0kasj9h0gzvr4gfk2magqprvl37jnlzv9u) doesn't exist: vault not found","time":"2022-02-08T23:38:05Z","message":"fail to retrieve vault"}
{"level":"error","error":"vault with pubkey(tthorpub1addwnpepqv3eslzyykkqzrf2zz5yp7pfepur2tyrvsvhd2lu72egdejpuezgcjyzfgp) doesn't exist: vault not found","time":"2022-02-08T23:38:05Z","message":"fail to retrieve vault"}
{"level":"error","error":"vault with pubkey(tthorpub1addwnpepqdnujur3husklhltj3l0kmmsepn0u68sge0jxg5k550nvdpphxm9s0v7f3v) doesn't exist: vault not found","time":"2022-02-08T23:38:05Z","message":"fail to retrieve vault"}
{"level":"error","error":"cannot save a pool with an empty asset","time":"2022-02-08T23:38:05Z","message":"fail to save pool"}
{"level":"error","rune in module":0,"rune in pools":0,"time":"2022-02-08T23:38:05Z","message":"cannot migrate with a zero amount"}
{"level":"error","error":"vault with pubkey(tthorpub1addwnpepqg65km6vfflrlymsjhrnmn4w58d2d36h977pcu3aqp6dxee2yf88yg0z3v4) doesn't exist: vault not found","pubKey":"tthorpub1addwnpepqg65km6vfflrlymsjhrnmn4w58d2d36h977pcu3aqp6dxee2yf88yg0z3v4","time":"2022-02-08T23:38:05Z","message":"fail to get vault"}
{"level":"error","chain":"ETH","error":"transaction size can't be zero or negative: 0","time":"2022-02-08T23:38:05Z","message":"network fee is invalid"}
{"level":"error","chain":"ETH","error":"transaction size can't be zero or negative: 0","time":"2022-02-08T23:38:05Z","message":"network fee is invalid"}
{"level":"error","error":"fail to prepare outbound tx: insufficient funds for outbound request: 0x340b94e5369cEDe551a117960c75547eA84eAEdE 60000000 remaining","time":"2022-02-08T23:38:05Z","message":"fail to schedule refund MKR transaction"}
{"level":"error","error":"cannot save a pool with an empty asset","time":"2022-02-08T23:38:05Z","message":"fail to save ETH pool"}
{"level":"error","error":"thorpub1addwnpepqdr4386mnkqyqzpqlydtat0k82f8xvkfwzh4xtjc84cuaqmwx5vjvgnf6v5 is not bech32 encoded pub key,err : invalid Bech32 prefix; expected tthorpub, got thorpub","time":"2022-02-08T23:38:05Z","message":"fail to parse pub key"}
{"level":"error","error":"thorpub1addwnpepqdr4386mnkqyqzpqlydtat0k82f8xvkfwzh4xtjc84cuaqmwx5vjvgnf6v5 is not bech32 encoded pub key,err : invalid Bech32 prefix; expected tthorpub, got thorpub","time":"2022-02-08T23:38:05Z","message":"fail to parse pub key"}
{"level":"error","asset":"ETH.USDC-0XA0B86991C6218B36C1D19D4A2E9EB0CE3606EB48 ","error":"invalid symbol","time":"2022-02-08T23:38:05Z","message":"fail to parse asset"}
{"level":"error","error":"thorpub1addwnpepqdr4386mnkqyqzpqlydtat0k82f8xvkfwzh4xtjc84cuaqmwx5vjvgnf6v5 is not bech32 encoded pub key,err : invalid Bech32 prefix; expected tthorpub, got thorpub","pubkey":"thorpub1addwnpepqdr4386mnkqyqzpqlydtat0k82f8xvkfwzh4xtjc84cuaqmwx5vjvgnf6v5","time":"2022-02-08T23:38:05Z","message":"fail to parse pub key"}
{"level":"error","error":"thorpub1addwnpepqdr4386mnkqyqzpqlydtat0k82f8xvkfwzh4xtjc84cuaqmwx5vjvgnf6v5 is not bech32 encoded pub key,err : invalid Bech32 prefix; expected tthorpub, got thorpub","pubkey":"thorpub1addwnpepqdr4386mnkqyqzpqlydtat0k82f8xvkfwzh4xtjc84cuaqmwx5vjvgnf6v5","time":"2022-02-08T23:38:05Z","message":"fail to parse pub key"}
{"level":"error","error":"thorpub1addwnpepqwk8cx4x6jjlsrq6305zs68xtpfcyk3l2k7gp37yqcz0q4g8ar2sz9ms9ur is not bech32 encoded pub key,err : invalid Bech32 prefix; expected tthorpub, got thorpub","time":"2022-02-08T23:38:05Z","message":"fail to parse asgard pub key"}
{"level":"error","error":"thorpub1addwnpepq0myn4whrj7qfrzc647dju7rgtjc5punucxwvfut56mghuzxakq37e8ev4y is not bech32 encoded pub key,err : invalid Bech32 prefix; expected tthorpub, got thorpub","time":"2022-02-08T23:38:05Z","message":"fail to parse asgard vault public key"}
{"level":"error","error":"cannot add bond while node is active or ready status: 1 error occurred:\n\t* internal error\n\n","time":"2022-02-08T23:38:15Z","message":"msg bond fail validation"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T23:38:15Z","message":"keeper error"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T23:38:15Z","message":"fail to add fee to reserve"}
{"level":"error","error":"cannot add bond while node is active or ready status: 1 error occurred:\n\t* internal error\n\n","time":"2022-02-08T23:38:15Z","message":"msg bond fail validation"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T23:38:15Z","message":"keeper error"}
{"level":"error","error":"KVStore Error: fail to send fee to reserve: 0rune is smaller than 2000000rune: insufficient funds [cosmos/cosmos-sdk@v0.42.1/x/bank/keeper/send.go:193]","time":"2022-02-08T23:38:15Z","message":"fail to add fee to reserve"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T23:38:21Z","message":"msg set version failed validation"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T23:38:21Z","message":"msg set version failed validation"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T23:38:26Z","message":"msg set version failed validation"}
{"level":"error","error":"not enough bond: unauthorized","time":"2022-02-08T23:38:26Z","message":"msg set version failed validation"}
```

The same errors on `0.79.1` now. What's changed? Maybe for a while I was
actually running `0.72.0`? Trying...

```
THORNODE_IMAGE=registry.gitlab.com/alexdcox/thornode:mocknet-0.72.0 ./thornode.sh
```

Yep. Both nodes get listed just fine on `0.72.0`. No errors. So my scripts
need to be updated. 

Lets have a look through the changes and see if anything is obvious.

```
git difftool 0.72.0..develop
```

### 09.02.2022 Wednesday

Had a call with `shotonoff` he doesn't want us to copy/fork `btcutil` but just
use the original. I explained:
- All the other chain clients do this.
- Co-dependencies between projecs cause issues (yeah I was vague I did this over a year ago)
- At some point we need to change function arguments to match paths (also vague, couldn't quite remember what)

So it brought up some questions, naturally.
1) What's the problem with the circular dependency?  
   I'm not even sure we need to break it, I just think it's a lot nicer.
2) Can we just use the original `btcutil`?  
   I don't think so, but I can't remember why.
3) A question that came up for me:  
   What functionality does the thorchain code need to use from `dashd-go` and
   `dashutil`?

So I'm dedicating today towards explaining what I did and verifying that it was
a good idea...

-----

Original goals of my PR:
- **What:** Add chainlock and instantlock struct fields to rpc responses.  
  **Why:**  So that we can check in client code if a block was chainlocked.  
  `git cherry-pick -x 14d16e803f88ecb3a1dd943712df051151485da9`

- **What:** Correct chainparams for dash.  
  **Why:**  So that we can determine dash addresses from keys etc.  
  `git cherry-pick -x 2496c2f8d921d71989cfeec6d227fdc078c162df`  

- **What:** Bugfix: Remove GetInfo rpc command  
  **Why:**  It no longer exists on dashd, and there were calls to it that broke required functionality.  
  `git cherry-pick -x cbaf5b7df028e388275f3b0f2acaebe87ba89f85`

You can do these things without updating/changing import or package paths.

When you import that (JUST the above 3 things) into a new project the following
happens:

```
go get github.com/alexdcox/dashd-go@997040ca7d74
```

```
go: downloading github.com/alexdcox/dashd-go v0.22.0-beta.0.20220209174856-997040ca7d74
go get: github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220209174856-997040ca7d74: parsing go.mod:
  module declares its path as: github.com/dashevo/dashd-go
          but was required as: github.com/alexdcox/dashd-go
```

Can we ignore that? I think so, but it ignores go conventions which is why it
spits out that error.

Okay let's JUST fix that, and see how that cascades into more changes...

(next branch)

```
git checkout -b alex-test2
gsed 's+module github.com/dashevo/dashd-go+module github.com/alexdcox/dashd-go+g' -i go.mod

# remove dep on btcd (because it's already this repo why is that there??)

git commit -am "Update module package path to match github url"
git push --set-upstream origin alex-test2
```

(back to the demo project)

```
go get github.com/alexdcox/dashd-go@alex-test2
go get github.com/alexdcox/dashd-go@702745ae
```

Fresh new error:

> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220209180549-98464aecd067/server.go:1352:23: sp.server.syncManager.QueueNotFound undefined (type *netsync.SyncManager has no field or method QueueNotFound)

```
go get github.com/alexdcox/dashd-go@997040ca
```

netsync.SyncManager  
github.com/btcsuite/btcd/netsync

```
sudo rm -rf ~/go/pkg/mod/cache/download/github.com/alexdcox
sudo rm -rf ~/go/pkg/mod/github.com/alexdcox
```

The problem is, even though we've added new struct fields for
instantlock/chainlock in `dashd-go/btcjson/chainsvrresults.go`, they aren't
actually returned because the package path is...?

- Update package paths: btcsuite/btcd to dashevo/dashd-go and btcsuite/??? 

To add instantlock/chainlock struct fields I have to change ___  
To use those changes I have to include `github.com/alexdcox/dashd-go`.  
&nbsp;&nbsp;This is not the package path as defined in `go.mod` (still set to `btcsuite/btcd`)

Wasn't able to spend as much time on this today as I wanted.

### 10.02.2022 Thursday

```
go test ./...
```
> package github.com/alexdcox/dashd-go/database/ffldb  
>   database/ffldb/db.go:19:2: use of internal package github.com/btcsuite/btcd/database/internal/treap not allowed

I think this was the first argument for changing the pathnames, and the first
thing I stumbled into when working on this. I wanted to have working tests
even if that meant commenting out or removing broken ones - to start off on the
right foot.

```
go mod init
go mod edit -replace github.com/dashevo/dashd-go=github.com/alexdcox/dashd-go@997040ca
go get github.com/alexdcox/dashd-go@997040ca
```

```
go clean -modcache
```
> go clean -modcache: unlinkat /Users/adc/go/pkg/mod/cache: directory not empty

So reasons for correcting the module paths:
- It fixes the `module decares its path as` error which prevents `go get`
- It allows `go test ./...`
- It follows go conventions

```
go get -d -v github.com/alexdcox/dashd-go@997040ca
```

I can't find a way to import a module when the `go.mod` file module path
doesn't match the `go get` url. Go just doesn't like it. I'm completely blocked
by the `module decares its path as` error so I'm going to assume I have to at
least change that.

```
go get -d -v github.com/alexdcox/dashd-go@1d233169
```

`go run main.go`
> \# github.com/alexdcox/dashd-go/rpcclient
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:948:47: undefined: "github.com/btcsuite/btcd/btcjson".CreateWalletResult
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:964:28: undefined: "github.com/btcsuite/btcd/btcjson".CreateWalletCmd
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:1023:71: undefined: "github.com/btcsuite/btcd/btcjson".CreateWalletResult
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:1033:49: undefined: "github.com/btcsuite/btcd/btcjson".GetAddressInfoResult
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:1058:51: undefined: "github.com/btcsuite/btcd/btcjson".GetAddressInfoResult
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:1743:46: undefined: "github.com/btcsuite/btcd/btcjson".GetBalancesResult
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:1770:34: undefined: "github.com/btcsuite/btcd/btcjson".GetBalancesResult
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:2376:45: undefined: "github.com/btcsuite/btcd/btcjson".ImportMultiResults
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:2395:46: undefined: "github.com/btcsuite/btcd/btcjson".ImportMultiRequest
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:2395:83: undefined: "github.com/btcsuite/btcd/btcjson".ImportMultiOptions
> ../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e/rpcclient/wallet.go:2395:83: too many errors

> go: github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220210235220-1d233169ac3e used for two different module paths (github.com/alexdcox/dashd-go and github.com/btcsuite/btcd)

The codebase has a load of references to:
`github.com/dashevo/dashd-go/btcjson`


```
replace github.com/dashevo/dashd-go => github.com/alexdcox/dashd-go v0.22.0-beta.0.20220210235220-1d233169ac3e
```

```
go mod tidy
```
```
go: finding module for package github.com/alexdcox/dashd-go/rpcclient
go: found github.com/alexdcox/dashd-go/rpcclient in github.com/alexdcox/dashd-go v0.0.1
go: github.com/alexdcox/dashd-go@v0.0.1 requires
  github.com/alexdcox/dashutil@v0.0.1 requires
  github.com/alexdcox/dashd-go@v0.22.0-beta: parsing go.mod:
  module declares its path as: github.com/dashevo/dashd-go
          but was required as: github.com/alexdcox/dashd-go
```

There's the circular dependency. `dashd-go@v0.0.1` isn't even a thing at the
moment. I'm going to delete my entire modcache.

```
sudo rm -rf ~/go/pkg/mod/cache/download/github.com/alexdcox
sudo rm -rf ~/go/pkg/mod/github.com/alexdcox
```

```
git show 1d233169ac3e:go.mod
```

```
go run main.go
```
```
../../../../pkg/mod/github.com/btcsuite/btcutil@v1.0.2/address.go:14:2: missing go.sum entry for module providing package github.com/btcsuite/btcd/btcec (imported by github.com/btcsuite/btcutil); to add:
  go get github.com/btcsuite/btcutil@v1.0.2
../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220209174856-997040ca7d74/rpcclient/wallet.go:15:2: missing go.sum entry for module providing package github.com/btcsuite/btcd/btcjson (imported by github.com/dashevo/dashd-go/rpcclient); to add:
  go get github.com/dashevo/dashd-go/rpcclient@v0.22.0-beta
../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220209174856-997040ca7d74/rpcclient/infrastructure.go:28:2: missing go.sum entry for module providing package github.com/btcsuite/btcd/chaincfg (imported by github.com/dashevo/dashd-go/rpcclient); to add:
  go get github.com/dashevo/dashd-go/rpcclient@v0.22.0-beta
../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220209174856-997040ca7d74/rpcclient/chain.go:13:2: missing go.sum entry for module providing package github.com/btcsuite/btcd/chaincfg/chainhash (imported by github.com/dashevo/dashd-go/rpcclient); to add:
  go get github.com/dashevo/dashd-go/rpcclient@v0.22.0-beta
../../../../pkg/mod/github.com/alexdcox/dashd-go@v0.22.0-beta.0.20220209174856-997040ca7d74/rpcclient/chain.go:14:2: missing go.sum entry for module providing package github.com/btcsuite/btcd/wire (imported by github.com/dashevo/dashd-go/rpcclient); to add:
  go get github.com/dashevo/dashd-go/rpcclient@v0.22.0-beta
```

```
go get github.com/btcsuite/btcutil@v1.0.2
go get github.com/dashevo/dashd-go/rpcclient@v0.22.0-beta
```

With these replace directives I got my demo program running:
```
replace github.com/btcsuite/btcd => github.com/dashevo/dashd-go v0.22.0-beta
replace github.com/dashevo/dashd-go => github.com/alexdcox/dashd-go v0.22.0-beta.0.20220209174856-997040ca7d74
replace github.com/alexdcox/dashd-go => /Users/adc/go/src/github.com/alexdcox/dashd-go
```

Now will that actually include the chainlock fields?

> FATA[0000] 405 Method Not Allowed

What method? What's it trying? Not very helpful.

Okay it was defaulting to websocket communication because `HTTPPostMode` wasn't
set to true. Now it's working. And I got the chainlock field from my repo! Even
though goland doesn't recognise/follow the replace directive.

Ahh just had to check goland "use go modules" because it didn't detect that like
it usually does.

Just these two in the project that requires the `dashd-go` repo will allow me
to use my repo in place of the official one, and omit the package name changes.
This allows me to test everything in the PR without additional changes. Nice.

```
replace github.com/btcsuite/btcd => github.com/dashevo/dashd-go v0.22.0-beta
replace github.com/dashevo/dashd-go => github.com/alexdcox/dashd-go v0.22.0-beta.0.20220209174856-997040ca7d74
```

Now on to the million dollar question. Is this enough for TC? What are we doing
in TC and can we just use `btcutil`?

Cleaned up a few other package imports I accidentally changed. New branch
`thorchain-integration4` with current HEAD commit `d684d129`.

NOTE: You can add the `require` line in go with just the commit and then run
`go mod tidy` to have go assign the fully qualified `<tag>.<date>-<commit-hash>`
format that it demands the use of.

Will thornode be able to download `eec5a1af50e4` commit for `dashd-go` now that
it doesn't exist?

Uses of dashutil in thornode:

```
dashutil.AmountSatoshi
```

Just a constant. Probably fine to use `btcutil`, dash subunits are 1e8 major
units, same as btc.

```
c.client.GetBlockVerboseTx(hash)
```

RPC method. Now this goes back to where I was talking about arguments. It's
actually the return structs/variables that are important, because we need to be
returning dash specific information which means
`btcsuite/btcd/btcjson:GetBlockVerboseTxResult`  
VS  
`dashevo/dashd-go/btcjson:GetBlockVerboseTxResult`  
...which means these function signatures have to change.

You might ask: can't we just use go mod replace directives?  

For thorchain, unfortunately not. The `github.com/btcsuite/btcd` package is
already required so we can't redirect btcd package usage to our package without
breaking bitcoin.

Therefore, we HAVE to update the package paths in `dashevo/dashd-go`

Okay we have to stop "pretending" to be `btcsuite/btcd`. Can we still use
`btcutil`. I'll update my thorchain branch to use the new dashevo commit,
switch over to using that, and see what carnage unfolds...

This is the latest commit on dashd-go as of 10.02.2022
```
go get -d github.com/dashevo/dashd-go
```

TODO: Absolutely MUST switch over to GetBlockTxVerbose because I didn't know
      that exists at the time.


Okay so I went ahead and made some replacements to my thorchain code:
```
alexdcox/btcutil   ->   btcsuite/btcutil
alexdcox/dashd-go  ->   dashevo/dashd-go
dashutil.          ->   btcutil.
```

Now we get an error for this method call:
```
btcutil.DecodeAddress(sourceAddr.String(), c.getChainCfg())
```

> Cannot use 'c.getChainCfg()' (type *"github.com/dashevo/dashd-go/chaincfg".Params) as the type *"github.com/btcsuite/btcd/chaincfg".Params


This demonstrates the incompatibility between our updated `dashd-go` branch and
the dash chainparams.Params struct with the `btcutil` package.

So how do we solve that?
- Write adapters to convert `dashevo/dashd-go/chaincfg.Params` into
  `btcsuite/btcd/chaincfg.Params`?
- Fork / recreate the `btcsuite/btcutil` package as `dashutil` with function
  arguments changed to `dashevo/dashd-go`
- Modify `dashd-go` and remove all redeclarations of `btcd` structs, so
  `dashd-go` methods return `btcd` structs, so they can be used with `btcutil`.
  This could be a lot of work, is it even viable?

All the other bifrost chainclient devs opted for the second. It saves additional
bloat in the `thorchain` repo (and any other client packages) and requires the
minimal amount of changes in the `btcd` and `btcutil` clones.

Why don't we just avoid using `DecodeAddress` etc?
The return value is `btcutil.Address` interface which is an argument to other
methods in the btcd/dashd-go package such as rpcclient methods

e.g. `ListUnspentMinMaxAddresses(address, chaincfg)`

Also `Address` is needed here: `txscript.PayToAddrScript(addr)` which is a
bifrost tx parsing package over at this repo:
`github.com/alexdcox/thorchain-dashd-txscript`
(eventually `gitlab.com/thorchain/bifrost/dashd-txscript` when it gets approved
by the TC core team) which currently uses my `dashutil` so we'll need to be
able to convert both to and from a handful of btcutil structs if we don't clone
and modify.

`dashd-go-pr-justification`
Trying to justify changes in dashd-go in the context of thorchain as a requiring project

If we use the default btcutil:
- need conversion between btcd.Address and dashd-go.Address
- need conversion between btcd/chaincfg.Params and dashd-go/chaincfg.Params

You know what, I'm going to just try option (3) above and see how it goes. Might
not be a lot of work...

End of my day. Might not be a lot of work for me but it's already looking like a
lot to review, which is not good.

Note for tomorrow: you have to run `go get github.com/dashevo/dashd-go` to have
the latest changes from the aliased repo included.

### 14.02.2022 Monday

Starting with updating my work log.

Right, so have I done enough to explain things now? Let me try:

- We need to update the module path to prevent `go get` issues in dependant packages.
- We can't use the `replace` directive because we've forked (and reference) `btcsuite/btcd`, which is also a separate dependency in thorchain.
- `btcutil` function arguments will not accept `dashd-go` redeclarations

So how do we solve that?
- Write adapters to convert `dashevo/dashd-go/chaincfg.Params` into
  `btcsuite/btcd/chaincfg.Params`?
- Fork / recreate the `btcsuite/btcutil` package as `dashutil` with function
  arguments changed to `dashevo/dashd-go`
- Modify `dashd-go` and remove all redeclarations of `btcd` structs, so
  `dashd-go` methods return `btcd` structs, so they can be used with `btcutil`.
  This could be a lot of work, is it even viable?
 
I've sent that to `shotonoff`. Switching over to `Decred`

### 24.02.2022 Thursday

Shotonoff has come back with a backport pull request for dashd-go with hopefully
all the additional corrections we need.

`go test ./...`

> FAIL: TestDashEvoCmds ...

Hangs on/after `github.com/dashevo/dashd-go/peer` for some reason?

Latest commit on `backport-master` is `go get -u github.com/dashevo/dashd-go@backport-master`.

In `thornode` repo:
`go get -u github.com/dashevo/dashd-go@backport-master`

```
github.com/dashevo/dashd-go imports
  github.com/dashevo/dashd-go/btcec/v2/ecdsa: github.com/dashevo/dashd-go/btcec/v2@v2.0.0-00010101000000-000000000000: invalid version: unknown revision 000000000000
github.com/dashevo/dashd-go imports
  github.com/dashevo/dashd-go/btcutil: github.com/dashevo/dashd-go/btcutil@v0.0.0-00010101000000-000000000000: invalid version: unknown revision 000000000000
github.com/dashevo/dashd-go imports
  github.com/dashevo/dashd-go/btcutil/bloom: github.com/dashevo/dashd-go/btcutil@v0.0.0-00010101000000-000000000000: invalid version: unknown revision 000000000000
github.com/dashevo/dashd-go imports
  github.com/dashevo/dashd-go/blockchain imports
  github.com/dashevo/dashd-go/btcec/v2: github.com/dashevo/dashd-go/btcec/v2@v2.0.0-00010101000000-000000000000: invalid version: unknown revision 000000000000
github.com/dashevo/dashd-go imports
  github.com/dashevo/dashd-go/blockchain/indexers imports
  github.com/dashevo/dashd-go/btcutil/gcs: github.com/dashevo/dashd-go/btcutil@v0.0.0-00010101000000-000000000000: invalid version: unknown revision 000000000000
github.com/dashevo/dashd-go imports
  github.com/dashevo/dashd-go/blockchain/indexers imports
  github.com/dashevo/dashd-go/btcutil/gcs/builder: github.com/dashevo/dashd-go/btcutil@v0.0.0-00010101000000-000000000000: invalid version: unknown revision 000000000000
```

`go get` not working currently.

1. replace `dashd-go/btcec/v2` with `dashd-go/btcec` because it's a package not a module and therefore we can't use the module major version suffix.

### 25.02.2022 Friday

Looking into shotonof PR still... There's somthing with the module layout that's
not allowing `go get` perhaps I can help out here...

New repo: github.com/alexdcox/nested-module-demo

Yeah I've messed around with it a bit. It compiles, but `go mod tidy` and
`go get` won't work because it's not following the go module conventions.

Think we might have to drop the `btcec/v2` submodule. `go get` and `go mod tidy`
complains at the moment and I'm not sure if there's a way to

### 29.02.2022 Monday

Tried shotonoff's branch `backport-master` again, sent a message for him to have
a look at.

### 01.03.2022 Tuesday

Mr S wanted me to use his PR as my base. Done did. Balls back in his court...

### 02.03.2022 Wednesday

Shotonoff asked for my changes to be covered by the unit tests. He merged the
`backport-master` branch into `master` then closed my PR. 

All tests are passing on `master`. Not on my branch. Here we go...

```
--- FAIL: TestHelp (0.00s)
    rpcserverhelp_test.go:43: Failed to generate help for method 'getrawtransaction': txrawresult-chainlock
    rpcserverhelp_test.go:43: Failed to generate help for method 'getblockheader': getblockheaderverboseresult-chainlock
    rpcserverhelp_test.go:43: Failed to generate help for method 'getblock': getblockverboseresult-chainlock
```

Okay so this is already becoming a pain. The block data for tests are stored in
`dat.bz2` files. The blocks are being rejected because the network bytes have
changed.

Need to do a byte find and replace for:
```
3652501241    f9beb4d9    btc mainnet
              d9b4bef9    <- this was written in my `protocol.go` file, inverted
to
3177909439    bf0c6bbd    dash mainnet
              bd6b0cbf    <- this is what I wrote in `dashd-go/blockchain/protocol.go`
```

NOTE: You can do this conversion in cyberchef with:

Int to Hex  
https://gchq.github.io/CyberChef/#recipe=To_Base(16)Swap_endianness('Hex',4,false)Find_/_Replace(%7B'option':'Regex','string':'%20'%7D,'',true,false,false,false)&input=MzY1MjUwMTI0MQ

Hex to Int
https://gchq.github.io/CyberChef/#recipe=Swap_endianness('Hex',4,true)From_Base(16)&input=ZjliZWI0ZDk

Found in `dashpay/dash` `chainparams.cpp`:
```c
pchMessageStart[0] = 0xbf;
pchMessageStart[1] = 0x0c;
pchMessageStart[2] = 0x6b;
pchMessageStart[3] = 0xbd;
```

So I think I need to update my network bytes anyway, they weren't checked and
they don't seem to be right. Na they were. Getting a little thrown off by the
way go reads ints in binary notation as big-endian and binary as little endian
by default.

It's compressed, so need to uncompress first, then F+R, then compress, then
overwrite.

Have to do write in 2 steps, write the modified uncompressed dat, then compress
manually using bzip2 in terminal, as there isn't a bzip2 compression package
for go.

Awesome, that worked. Moving on...

github.com/dashevo/dashd-go/database/ffldb  
FAIL TestFailureScenarios  
> Block doesn't match network: 3652501241 expects MainNet

```
go test github.com/dashevo/dashd-go/database/ffldb -run TestFailureScenarios
```

Might have to run my replacer against all of these `find . -name '*.bz2'`...

github.com/dashevo/dashd-go/txscript  
FAIL: ExamplePayToAddrScript  

```
go test github.com/dashevo/dashd-go/txscript -run ExamplePayToAddrScript
```

Okay for this one I'm just going to use a recent dash mainnet transaction.
txid: `10b0227ab3a1845057c18e2ab06d864f15982bed0e4cc0e7272575f24853d9fb`

Next one:

FAIL: TestElementWire  
Just needed to change the network bytes again.  

### 03.03.2022 Thursday

Shotonof hasn't got round to merging this yet:  
https://github.com/dashevo/dashd-go/pull/13/files

### 04.03.2022 Friday

Apparently I need to fix tests. There's more? Need to run: `make unit-cover`

Looks like either my crypto tool isn't generating testnet wif correctly or
my old dashd-go isn't right...

Interesting, didn't know you can have both uncompressed and compressed wif. The
funny thing is the compressed wif contains more data than the uncompressed.

Right I'm revising `p2sh` to fix this test:

output:  
```
{
    "result": {
        "txid": "3c9018e8d5615c306d72397f8f5eef44308c98fb576a88e030c25456b4f3a7ac",
        "hash": "3c9018e8d5615c306d72397f8f5eef44308c98fb576a88e030c25456b4f3a7ac",
        "version": 1,
        "size": 222,
        "vsize": 222,
        "weight": 888,
        "locktime": 0,
        "vin": [
            {
                "txid": "d6f72aab8ff86ff6289842a0424319bf2ddba85dc7c52757912297f948286389",
                "vout": 0,
                "scriptSig": {
                    "asm": "3045022100abbc8a73fe2054480bda3f3281da2d0c51e2841391abd4c09f4f908a2034c18d02205bc9e4d68eafb918f3e9662338647a4419c0de1a650ab8983f1d216e2a31d8e3[ALL] 046f55d7adeff6011c7eac294fe540c57830be80e9355c83869c9260a4b8bf4767a66bacbd70b804dc63d5beeb14180292ad7f3b083372b1d02d7a37dd97ff5c9e",
                    "hex": "483045022100abbc8a73fe2054480bda3f3281da2d0c51e2841391abd4c09f4f908a2034c18d02205bc9e4d68eafb918f3e9662338647a4419c0de1a650ab8983f1d216e2a31d8e30141046f55d7adeff6011c7eac294fe540c57830be80e9355c83869c9260a4b8bf4767a66bacbd70b804dc63d5beeb14180292ad7f3b083372b1d02d7a37dd97ff5c9e"
                },
                "sequence": 4294967295
            }
        ],
        "vout": [
            {
                "value": 0.01,
                "n": 0,
                "scriptPubKey": {
                    "asm": "OP_HASH160 f815b036d9bbbce5e9f2a00abd1bf3dc91e95510 OP_EQUAL",
                    "hex": "a914f815b036d9bbbce5e9f2a00abd1bf3dc91e9551087",
                    "reqSigs": 1,
                    "type": "scripthash",
                    "addresses": [
                        "3QJmV3qfvL9SuYo34YihAf3sRCW3qSinyC"
                    ]
                }
            }
        ],
        "hex": "010000000189632848f99722915727c5c75da8db2dbf194342a0429828f66ff88fab2af7d6000000008b483045022100abbc8a73fe2054480bda3f3281da2d0c51e2841391abd4c09f4f908a2034c18d02205bc9e4d68eafb918f3e9662338647a4419c0de1a650ab8983f1d216e2a31d8e30141046f55d7adeff6011c7eac294fe540c57830be80e9355c83869c9260a4b8bf4767a66bacbd70b804dc63d5beeb14180292ad7f3b083372b1d02d7a37dd97ff5c9effffffff0140420f000000000017a914f815b036d9bbbce5e9f2a00abd1bf3dc91e955108700000000",
        "blockhash": "000000000000021410ea57495edb671b7feabe29c8fbdee92f0c4f810ba32773",
        "confirmations": 520637,
        "time": 1351370614,
        "blocktime": 1351370614
    },
    "error": null,
    "id": null
}
```

input:  
```
{
    "result": {
        "txid": "837dea37ddc8b1e3ce646f1a656e79bbd8cc7f558ac56a169626d649ebe2a3ba",
        "hash": "837dea37ddc8b1e3ce646f1a656e79bbd8cc7f558ac56a169626d649ebe2a3ba",
        "version": 1,
        "size": 436,
        "vsize": 436,
        "weight": 1744,
        "locktime": 0,
        "vin": [
            {
                "txid": "3c9018e8d5615c306d72397f8f5eef44308c98fb576a88e030c25456b4f3a7ac",
                "vout": 0,
                "scriptSig": {
                    "asm": "0 304502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d0b6ae9de10ebf2da06b1bbdaaba4e50eb078f39e3d78[ALL] 30440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e27038e945bc9db59c732728a383a6f1ed2fb99da7a4[ALL] 52410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353ae",
                    "hex": "0048304502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d0b6ae9de10ebf2da06b1bbdaaba4e50eb078f39e3d78014730440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e27038e945bc9db59c732728a383a6f1ed2fb99da7a4014cc952410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353ae"
                },
                "sequence": 4294967295
            }
        ],
        "vout": [
            {
                "value": 0.01,
                "n": 0,
                "scriptPubKey": {
                    "asm": "OP_DUP OP_HASH160 ae56b4db13554d321c402db3961187aed1bbed5b OP_EQUALVERIFY OP_CHECKSIG",
                    "hex": "76a914ae56b4db13554d321c402db3961187aed1bbed5b88ac",
                    "reqSigs": 1,
                    "type": "pubkeyhash",
                    "addresses": [
                        "1GtpSrGhRGY5kkrNz4RykoqRQoJuG2L6DS"
                    ]
                }
            }
        ],
        "hex": "0100000001aca7f3b45654c230e0886a57fb988c3044ef5e8f7f39726d305c61d5e818903c00000000fd5d010048304502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d0b6ae9de10ebf2da06b1bbdaaba4e50eb078f39e3d78014730440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e27038e945bc9db59c732728a383a6f1ed2fb99da7a4014cc952410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353aeffffffff0140420f00000000001976a914ae56b4db13554d321c402db3961187aed1bbed5b88ac00000000",
        "blockhash": "000000000000037de995971fdc671426710a5bbedff7e9e283a396c6a16bf674",
        "confirmations": 520635,
        "time": 1351371345,
        "blocktime": 1351371345
    },
    "error": null,
    "id": null
}
```

So I'm trying to decode this:
```
0048304502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d0b6ae9de10ebf2da06b1bbdaaba4e50eb078f39e3d78014730440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e27038e945bc9db59c732728a383a6f1ed2fb99da7a4014cc952410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353ae
```

And trying to work out where this came from in the test:

```
52410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353ae
```

It came from the last part of the full input hex.

```
docker run \
  --rm \
  --name bitcoin \
  -it \
  registry.gitlab.com/thorchain/devops/bitcoin-core \
    -printtoconsole \
    -txindex \
    -rpcallowip=0.0.0.0/0 \
    -rpcbind=0.0.0.0 \
    -rpcauth=thorchain:d7e53bb9757b6d4fabf87775c7824b5c\$7097e9cde30ef4319ed708fc559267679ae6cc0bf7e18fd49b283650c0c26a10
```

```
bitcoin-cli -rpcuser=thorchain -rpcpassword=password decodescript
```

```
{
  "asm": "0 304502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d0b6ae9de10ebf2da06b1bbdaaba4e50eb078f39e3d7801 30440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e27038e945bc9db59c732728a383a6f1ed2fb99da7a401 52410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353ae",
  "type": "nonstandard",
  "p2sh": "3GA3KSaFH9VosSvCFiMw1a5V8Ao3a4yEm8",
  "segwit": {
    "asm": "0 d6dfc0d88d8849dd065ebf9ff3c96f77e87f2018739c817f70d1f9f0dfa25d5f",
    "hex": "0020d6dfc0d88d8849dd065ebf9ff3c96f77e87f2018739c817f70d1f9f0dfa25d5f",
    "address": "bc1q6m0upkyd3pya6pj7h70l8jt0wl587gqcwwwgzlms68ulphazt40s05s2w8",
    "type": "witness_v0_scripthash",
    "p2sh-segwit": "3NoEjsiB3supBvJb8XFHsCV4S2S9Mo4bkR"
  }
}
```

If you follow the `asm` and put that back into `decodescript` again in parts:
```
0
304502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d0b6ae9de10ebf2da06b1bbdaaba4e50eb078f39e3d7801
30440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e27038e945bc9db59c732728a383a6f1ed2fb99da7a401
52410491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f864104865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec687441048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d4621353ae
```

```
{
  "asm": "4502200187af928e9d155c4b1ac9c1c9118153239aba76774f775d7c1f9c3e106ff33c0221008822b0f658edec22274d 6ae9de10ebf2da06b1bbda OP_CODESEPARATOR OP_MAX OP_UNKNOWN [error]",
  "type": "nonstandard",
  "p2sh": "3KrgUQwuVJ3pBLk2qQ7aSdr4a1nfknM6n6",
  "segwit": {
    "asm": "0 c03e52377ee10169f6d3e05cc641db76168393157b0db03bf269404ef2de4be4",
    "hex": "0020c03e52377ee10169f6d3e05cc641db76168393157b0db03bf269404ef2de4be4",
    "address": "bc1qcql9ydm7uyqknaknupwvvswmwctg8yc40vxmqwljd9qyauk7f0jqrwcxmk",
    "type": "witness_v0_scripthash",
    "p2sh-segwit": "3JDpdoAF3iiYoRkKTKazWKd4aeaXiAeGXv"
  }
}
```

```
{
  "asm": "440220795f0f4f5941a77ae032ecb9e33753788d7eb5cb0c78d805575d6b00a1d9bfed02203e1f4ad9332d1416ae01e2 OP_2OVER [error]",
  "type": "nonstandard",
  "p2sh": "36KDmwh6EZFCPBW87SipsWQcR7fodW5foK",
  "segwit": {
    "asm": "0 e79e3e29c285256f764f7b8a50a91c2d007d0fa1a52a33499aedca5d2fa1568a",
    "hex": "0020e79e3e29c285256f764f7b8a50a91c2d007d0fa1a52a33499aedca5d2fa1568a",
    "address": "bc1qu70ru2wzs5jk7aj00w99p2gu95q86rap554rxjv6ah996tap269q277cyn",
    "type": "witness_v0_scripthash",
    "p2sh-segwit": "3Lo7znQVn92e2WRS9Q5CXiPRBAR62XDmHq"
  }
}
```

```
{
  "asm": "2 0491bba2510912a5bd37da1fb5b1673010e43d2c6d812c514e91bfa9f2eb129e1c183329db55bd868e209aac2fbc02cb33d98fe74bf23f0c235d6126b1d8334f86 04865c40293a680cb9c020e7b1e106d8c1916d3cef99aa431a56d253e69256dac09ef122b1a986818a7cb624532f062c1d1f8722084861c5c3291ccffef4ec6874 048d2455d2403e08708fc1f556002f1b6cd83f992d085097f9974ab08a28838f07896fbab08f39495e15fa6fad6edbfb1e754e35fa1c7844c41f322a1863d46213 3 OP_CHECKMULTISIG",
  "type": "multisig",
  "p2sh": "3QJmV3qfvL9SuYo34YihAf3sRCW3qSinyC"
}
```

So we have two `nonstandard/segwit` followed by `multisig`? Perhaps the first
two leave some important values on the stack? I can't say I fully understand,
but what I now know is that we're testing specifically the multisig operation
and ignoring the rest of it.

I can either search the dash ledger for a multisig script, or make one...

I think the search would be faster, even if I do have to write a script to
acomplish that too....

### 07.03.2022 Monday

Aiming to get these tests completed and pushed today if poss.

Okay my script found this one:  
`10b2099648910f6a6bc944a7efa528a9e48dd357a2886a4e40a2b6d42f10662e`

But the script hex is just `a914e87bbf09472100125616e21553495f5c17d6cc4a87`

Ah was looking at vout not vin. Turns out that tx does have a 3 script multisig
in though! Exactly what I'm looking for.

```
dash-cli decodescript 522102e652b7d4f39cc46150d73987e14f1067a695228e3668fd6eb860fd849461eba1210342d79bccbf0216319d51e58314fc1e66ed47c797afe58f9057e6682540df95112103fd0ac2fbd0f8b182aafc99bf77564562e43e999cc3ef34f671ce1fcc112ac39c53ae
```
```
{
  "asm": "2 02e652b7d4f39cc46150d73987e14f1067a695228e3668fd6eb860fd849461eba1 0342d79bccbf0216319d51e58314fc1e66ed47c797afe58f9057e6682540df9511 03fd0ac2fbd0f8b182aafc99bf77564562e43e999cc3ef34f671ce1fcc112ac39c 3 OP_CHECKMULTISIG",
  "reqSigs": 2,
  "type": "multisig",
  "addresses": [
    "Xws719MBRr95AVtY6noVv3tFeCmWHRK2Ex",
    "Xn3R9nZFR8m2sngBz2BsQB9uwA33U6tkm6",
    "Xiy94svs9rdskmaL3ANjM7x8xBhAiFrA4q"
  ],
  "p2sh": "7iGYJ49wQWsyreaaaH1zQt9qF2eLTYhwdQ"
}
```

Need another. Found `4604215e1e9089eb46e407daa07fa30b0296bf8896cbfff13843ba81624cb910`.

Next failing test:  
```
go test github.com/dashevo/dashd-go/btcutil/gcs/builder -run TestUseBlockHash
```

next...

Okay fixed those unit tests and pushed. Sent shotonoff a message to review.  
Over to decred.  

### 29.03.2022 Tuesday

Had to focus on some ctx.com stuff there. Where am I?...

So my dash pr was accepted, now to see if I can refactor my TC PR

Have a `WIP` commit with a TONNE of messy logging. Not sure exactly what I was
looking for. Lots around:
- getBlockRequiredConfirmation
- GetConfirmationCount
- ConfirmationCountReady

I was bringing dash in-line with BTC/DOGE/BCH etc.  
Okay pushed that.  
Now to refactor alexdcox for dashevo...  

> go: finding module for package 
> gitlab.com/thorchain/thornode/bifrost/pkg/chainclients/dash imports
>   github.com/dashevo/dashd-go/btcec: module github.com/dashevo/dashd-go@latest found (v0.23.4), but does not contain package github.com/dashevo/dashd-go/btcec

Need to replace these:
```
github.com/dashevo/dashd-go/btcec
github.com/btcsuite/btcd/btcec
github.com/btcsuite/btcec
github.com/dashevo/dashd-go/btcec/v2
```

```
github.com/alexdcox/dashutil
github.com/btcsuite/btcutil
dashutil "github.com/dashevo/dashd-go/btcutil"
```

Need to update github.com/alexdcox/thorchain-dashd-txscript to use btcutil
(dashd-go). There was previously a go mod `replace` directive pointing to my
repo.

As expected, there are numerous places now where we're interacting with the
`btcec` library and it expects bitcoin chainparams not dashutil chainparams, and
we haven't reimplemented the btcec library as I recommended, so now we need
adapters as per my discussion in the first place. The job is half finished.

I'm just going to write chaincfg adapters in my txscript repo.

TBH I'm not really sure why we even need the top when there's the bottom:
```
github.com/alexdcox/thorchain-dashd-txscript
github.com/dashevo/dashd-go/txscript
```

They seem to be doing pretty much the same stuff. It's just a copypaste.

Should confirm we need the `a9800ac9` commit of dashevo/dashd-go.

```
go get github.com/dashevo/dashd-go@a9800ac9
```

`go get github.com/dashevo/dashd-go@a9800ac9`
> go get: github.com/dashevo/dashd-go@a9800ac9 (v0.0.0-20220315183651-a9800ac93748) requires github.com/dashevo/dashd-go@v0.23.2, not github.com/dashevo/dashd-go@a9800ac9 (v0.0.0-20220315183651-a9800ac93748)

Potential issues with btcec/v2 and txscript in dashd-go:
- txscript.Signable not found
- txscript.NewPrivateKeySignable not found

`github.com/dashevo/dashd-go@master(a9800ac9)`
has a dependency on an older version of itself:
`github.com/dashevo/dashd-go@v0.23.3`
which causes package resolution issues when I come to build

I sent `shotonoff` this:  
https://github.com/alexdcox/dashd-go-usage-attempt

At this point I would recommend breaking the dependency on btcd. We didn't even
need the backport to begin with.

```
go get github.com/alexdcox/dashd-go@thorchain-integration3
```

```
github.com/dashevo/dashd-go => github.com/alexdcox/dashd-go v0.22.0-beta.0.20220329232951-039daa8159d0
```

```
git diff --stat a9800ac9..039daa81

go get github.com/alexdcox/dashd-go/btcec@aa0c9c8a

github.com/dashevo/dashd-go => github.com/alexdcox/dashd-go v0.22.0-beta.0.20220329234754-aa0c9c8a95ec

go get github.com/dashevo/dashd-go

github.com/dashevo/dashd-go/btcec
github.com/dashevo/dashd-go/btcjson
github.com/dashevo/dashd-go/btcutil
github.com/dashevo/dashd-go/chaincfg
github.com/dashevo/dashd-go/chaincfg/chainhash
github.com/dashevo/dashd-go/mempool
github.com/dashevo/dashd-go/rpcclient
github.com/dashevo/dashd-go/txscript
github.com/dashevo/dashd-go/wire
```

So the way I started out with this was reverting, because that's so much easier.
I should probably just work out how to do things using the new methods,
wherever they are.

`find . -mindepth 2 -name go.mod -or -name go.sum`
```
rm ./btcutil/go.mod
rm ./btcutil/psbt/go.mod
rm ./btcec/go.mod
```

- delete submodules
- rename package paths for missing `v2` package `btcec`
```
github.com/dashevo/dashd-go/btcec/v2
github.com/dashevo/dashd-go/btcec
```
- update main module `go.mod`
- run `go mod tidy`


```
go get github.com/alexdcox/dashd-go@thorchain-integration5
```

```
github.com/dashevo/dashd-go => github.com/alexdcox/dashd-go v0.22.0-beta.0.20220330013947-680511b113d9
```

Okay problem 1:

There's no longer `txscript.Signable`.



### 20.04.2022 Wednesday

I'd like to progress, but `dashd-go` isn't right still. Posted in Discord...

Shotonoff's away today.  
Sam/Quantum's on holiday.  

Daymn.  


### 21.04.2022 Thursday

dashd-go `v0.23.5` is now available:  
`go get github.com/dashevo/dashd-go@v0.23.5`

gitlab.com/thorchain/bifrost/dashd-txscript  
github.com/alexdcox/thorchain-dashd-txscript  

Shotonoff is forcing me to use btcec v2 with dash, which means I'd have to
update a load of code I didn't write, which could introduce bugs. Instead I'm
just going to use the original:

`go get github.com/btcsuite/btcd/btcec`  
`go get github.com/btcsuite/btcd@v0.22.0-beta`

??? Working on my txscript repo

- replace `github.com/alexdcox/dashd-go` with `github.com/dashevo/dashd-go`

- replace `github.com/dashevo/dashd-go/btcec` with `github.com/dashevo/dashd-go/btcec/v2`
OR
- replace `github.com/dashevo/dashd-go/btcec` with `github.com/btcsuite/btcd/btcec`
- `go get github.com/btcsuite/btcd@v0.22.0-beta`

- replace `"github.com/alexdcox/dashutil"` with `dashutil "github.com/dashevo/dashd-go/btcutil"`
- replace `chaincfg.TestNetParams` with `chaincfg.TestNet3Params`


> Cannot use 'pubKey' (type *"github.com/dashevo/dashd-go/btcec/v2".PublicKey) as the type *"github.com/btcsuite/btcd/btcec".PublicKey


I'm forced to convert from v2 to v1 btcec PublicKey types in `sign.go` in the
thorchain txscript library. Thorchain uses btcec v1, the new dashd-go only uses
v2, so extra work to convert there.

```go
v1PublicKey, _ := btcec.ParsePubKey(v2PubKey.SerializeCompressed(), btcec.S256())

v1PrivateKey, _ := btcec.PrivKeyFromBytes(btcec.S256(), v2PrivateKey.Serialize())
```

If that works, I'm good.

Okay so why did TC reimplement `txscript` for all chains in the first place?  
Can I not just use the official one?  
They were updated to make use of the bifrost `Signable` type, data can be signed
passing those in instead of btcec.PrivateKey.

Issue is, `v2` removed:  
`btcec.Signable`  
`btcec.Signature`  


`gitlab.com/thorchain/bifrost/dashd-txscript`
`go get github.com/alexdcox/thorchain-dashd-txscript@58e1d1d`

```
gitlab.com/thorchain/bifrost/dashd-txscript => github.com/alexdcox/thorchain-dashd-txscript@v0.0.0-20220422001116-58e1d1d25f3b
```

```
dashec "github.com/dashevo/dashd-go/btcec/v2"
"github.com/btcsuite/btcd/btcec"
```

Okay updated dashd-txscript. Refactored my thornode branch to use dashevo. Fixed
broken tests. Merged dev in again. Check tests again. Push.

New stuff:
- terra
- bifrost config template needs updating
  - pprofEnabled
  - blockScannerBackoff
  - ethSuggestedFeeVersion
  - btcParallelMempoolScan
  - bchParallelMempoolScan
  - ltcParallelMempoolScan
  - ltcDisabled
  - dogeParallelMempoolScan
  - dogeDisabled
  - dashParallelMempoolScan
  - dashDisabled
  - terraHost
  - terraDisabled
  - terraStartBlockHeight

chains using new block scanner backoff:  
BTC DOGE TERRA LTC BCH ETH  
all of them. Not BNB. Add DASH o course.  

- [ ] TODO: Test the parsing of environment variables when it comes to creating
  the bifrost config json.
- [x] TODO: Refactor the `GetAccount` and `GetAccountByAddress` bifrost client methods.

Dash integration has been on hold until the core Dash team releases a version of
`dashd-go` 

The Dash core devs pushed a new version `v0.23.5` of their `dashd-go` repo
yesterday, which contains updates needed to refactor the Dash bifrost client.
Now the dependency on `github.com/alexdcox/dashd-go` has been replaced with the
official package `github.com/dashevo/dashd-go`. This was requested during a
security review and has been the primary blocker for a while.

Now that's out of the way, the Dash merge request is once again ready!

I'll switch back to `node-launcher` and the smoke tests now.

### 22.04.2022 Friday

So Leena asked the typical txout concerns again followed by how much the dash
bifrost client might have diverged from the others. I'll go through each method
and see...

`git diff HEAD:bifrost/pkg/chainclients/bitcoin/client.go bifrost/pkg/chainclients/dash/client.go`

- [ ] Is default coinbase value appropriate:

```
DefaultCoinbaseValue   = 10000
```

- [x] `currentBlockHeight` is now `*atomic.Int64`

Are there other places with atomic values now?

- [x] Pretty sure we can use the GetRawBlock dash rpc method now.

`c.client.GetBlockVerboseTx`

```go
rawBlock, err := c.client.RawRequest("getblock", []json.RawMessage{
  []byte(fmt.Sprintf(`"%s"`, hash.String())),
  []byte(`2`), // This argument selects verbose block output with transaction data included.
})
if err != nil {
  return
}
err = json.Unmarshal(rawBlock, &block)
```

Update dash client interface functions, switch to atomic values.  
Pluto said he's going to jump on the review today.  
Tests are passing.  

Taking to Gavin and Adam from `Nine Realms`?  
The Desert lynx asked about integrating with the TC fork Maya.  

Reopened the node launcher PR:
https://gitlab.com/thorchain/devops/node-launcher/-/merge_requests/361

Arranged a call with 9R guys and their dev.

TODO: Need to rebase node launcher with master.

Responded to a question about Dash on other CTXs and dapps:

Hey, I'm definitely not the best person to ask. My focus is pretty concentrated
on developing CTX.com and currently the TC integration for Dash/Decred so I
haven't been following general trends lately. There's interest in listing on
Maya as well as TC but as far as other DEXs go I'm not sure. I've recently
helped integrate with the DashDirect app, which is continually growing in
popularity. I defer to the Dash community for other apps


### 27.04.2022 Wednesday

9R Call  

I didn't make too many notes. Major things are:
- [ ] Ash to put Dash security review team in contact with 9R
- [ ] Me to rework txscript extra dependency out of dash bifrost chain client
- [ ] Me to arrange call to walk through dash client with 9R / secteams / devsA
- [ ] Answer the question: what is the maximum delay for a chainlock since it was launched?
- [ ] Set the dash docker image in `node-launcher` after they've run the build.sh

### 02.05.2022 Monday

Following node-launcher recommendations first.  
`chart.lock` has a checksum in it so I'll probably need to work that out.  

They've switched over to using docker image hashes so need to find that out.  

- [ ] Add `dash-core` aka `dash daemon` to `node-launcher/ci/images`
- [ ] Update `Chart.lock` node launcher
- [ ] Set dash image hash in node launcher when possible
- [ ] Fill out new chain proposal template

So if I'm following correctly, the goal is to move all images from
`thorchain/devops/*-core` to inside the `node-launcher` repo. All images will
resolve with the image name
`registry.gitlab.com/thorchain/devops/node-launcher` but will be differentiated
by the hash.

```
docker run \
  -it \
  --rm \
  --name dash-daemon \
  --entrypoint bash \
  registry.gitlab.com/thorchain/devops/node-launcher:dash-daemon-$(cat version)
```

```
/scripts/entrypoint-mock.sh
```

```
--env-file $dir/.env \
```

Okay going to try and modify my cluster setup script to work with the new dash
image and to work out what the address should be.

Deffo not the inbound address. Perhaps we can generate using the mnemonics listed
in `mocknet-30.yaml` in `node-launcher`?


```
docker exec -it thornode1 bash
thornode keys add temp --recover
> soldier tank ribbon above result process tide avocado enforce twice myself taste arrow stamp trend hub relax tired monster bone inch steel uphold charge
thornode keys show temp

NET=mocknet go run ./tools/pubkey2address -p tthorpub1addwnpepqvw0532tjm6skvc7wl02nflv97za4l0zd76z4xvya6935mwku65r5z2p6an
```

No luck.  
Trying:
- infant exchange ripple diet rebuild enact apology erode job throw faculty flight sock october same melt defense cook echo wise tobacco fatal egg nothing
tthorpub1addwnpepq0lncdjk6c8lnv7znzcwardfx2v55sm4m0kplmuca4fswt6fhv5gqmlg60g

I'm searching for a needle in a haystack here. So I just asked for help and will
move on to the new chain proposal:

```
Chain Name:                     dash
Chain Type:                     UTXO
Hardware Requirements:          1GB memory, 100GB storage
Year started:                   2014
Market Cap:                     USD 960,364,804
CoinMarketCap Rank:             95
24hr Volume:                    USD 109,459,640
Current DEX Integrations:       Atomic DEX
Other relevant dApps:           DashDirect
Number of previous hard forks:  17
```

I don't think Dash is listed on any dex with significant usage.

Getting some fresh new errors trying to start thornode locally:

> Error: error validating genesis file gitlab.com/thorchain/thornode/_adc/.thornode/config/genesis.json: {"@type":"/cosmos.crypto.secp256k1.PubKey","key":"AzE2zPSwVl6Dbqq4AFD3amw3m7hQCNgBLIQEIjUeefWH"} is not bech32 encoded pub key,err : decoding bech32 failed: string not all lowercase or all uppercase

> 8:14PM ERR fail to parse consensus public key error="decoding bech32 failed: string not all lowercase or all uppercase" key=+wFnXcxckuTILF0s+xxSp+r4f8eVfTdwql/HNW5iXjQ=
panic: decoding bech32 failed: string not all lowercase or all uppercase

So the addresses are not being populated on inbound_addresses because for some
reason the vault address has not been set. Probably because I'm just running the
one node here, okay so back to my cluster...

### 03.05.2022 Tuesday

First hour, back to cluster...  

It looks like `add_node_account` now sets a bond amount too along with the ip.  
Which means I no longer need to send all the node setup commands.  

Sent the revised chain proposal in.

Currently stuck on how to derive this master dash address.  
Asked for help...  

These are all the mnemonics I can see in the mocknet:

```
[
  "soldier tank ribbon above result process tide avocado enforce twice myself taste arrow stamp trend hub relax tired monster bone inch steel uphold charge",
  "infant exchange ripple diet rebuild enact apology erode job throw faculty flight sock october same melt defense cook echo wise tobacco fatal egg nothing",
  "edit tenant confirm word debate ginger urge bus cushion normal surface depend film much interest subway august frozen hobby fatal soon shock life message",
  "noodle deer august stay cradle shrug inform alpha recycle audit tribe pelican payment produce appear region economy annual nut frown sauce much kick warrior",
  "project pride grant dawn soccer couple snap swing laundry until icon weather because obvious clog often huge whisper unit side suit employ borrow reunion",
  "what sell bitter enjoy frozen pizza myth pepper garment chapter drill rural globe please clap sing title enroll ladder siren flock donate liberty remove",
  "original dirt tiny note pledge hint rather code ugly kite rain stamp exile until plate jazz reason nation mom penalty portion glue spring limit",
  "two almost ball rule lawsuit soon chaos ignore concert proud interest find tissue cram skate gospel damage mountain club review shield anger giant diary",
  "service junk alone utility pear profit used draw girl rack car cattle hurdle donkey empty shift setup creek grit volume crime spin silk token",
  "attack payment curious dwarf attack robust purchase trade when report good curtain detail want eagle riot use volume radar lamp spike caution drift mobile",
  "jacket bachelor fine rookie maid shiver title illegal essay afraid enjoy sauce diesel onion turkey crew record fade analyst romance warrior annual blame furnace",
  "project point select blur hospital liar galaxy crucial bottom flush fetch faith grief valid retreat drastic fence pepper ivory advance equip hire shallow marble",
  "emerge transfer spatial electric hint quarter modify matrix bench whip canoe super unveil entry put horse barely canyon poverty quarter police train fuel body",
  "sign beef glue custom slot jelly identify sheriff magnet click index dove inspire long often spice roof run asset position home nest sausage owner",
  "sea outside control burden fog reduce nature festival verb type tumble blind entire glimpse chapter claw bid diet lady focus pen ritual effort limit",
  "blade such habit october danger scare since sister now hurry garden fatal fat animal memory glove volcano start illness express great diary pyramid suffer",
  "fold argue fever away fame motion goose pond dry chair remain barrel ranch unfold forget fade defy crime history pledge disagree loud ten misery",
  "floor naive chase erase company arena manage custom rose vintage cute fork peasant latin fork senior equal domain faith grid quarter stage improve student",
  "sting winter punch floor clinic used alert hurry damp elevator remember retreat absent example rent divorce green wave receive element medal nation myth police",
  "wolf system range dance vendor across address pink vital about remove steel warrior property clean female fish stairs tent silly setup safe chair picnic",
  "cupboard wrong drive pepper scrub heavy repeat expire volume legend border poet shell fancy devote crowd crucial section actual connect sure stay honey feature",
  "term cherry busy blast flock wisdom female manage luxury boat measure place impose light camp arctic lobster dizzy notable capable runway regret message weapon",
  "drill raccoon mansion suggest base lunar inner industry shoe auto pair melt entry gauge lobster vivid labor pledge another interest parade labor canal domain",
  "fortune omit message sweet purity page green seed meat dose owner gas citizen cat service neutral dilemma vast enact mixed bonus atom inform floor",
  "adapt mushroom club noodle win clump door sunset cycle size punch airport favorite broom combine addict aware mixture lucky wage hollow tenant smart final",
  "surge drive surge vault bottom salad april glad zero evidence short load repeat quick quit chicken nerve fiber cancel merit either air wage buzz",
  "math girl panic party mention rebel custom tattoo good sunny icon mad couch shaft velvet apology regret end anger iron tiger pottery often hour",
  "happy bomb flame denial shoe modify bone correct banner mansion gallery answer tobacco sign payment cat avocado vanish immense soap best possible sell patch",
  "try whale organ balcony bacon noble iron carpet satisfy sunny anger stable innocent render strategy radio best library drum dove blanket kingdom tomato moment",
  "cruise narrow chest spare wink front swarm food parade bench bid tuna lecture maple report rain bulb badge version small teach fringe shove burden",
  "punch water dinner hybrid mesh desert mail nominee actual bleak corn dolphin piano dream also collect mule depart refuse chimney input message clump patch",
  "guilt document tag chief dignity pistol wheel essence damage estate fury endorse happy inherit ankle solution praise toast tuition long toilet long broken illegal"
]  
```

`make lint` was suggested for me to test the pipeline, but unfortunately mac
doesn't support `find` with the `-printf` which is contained in the script.

```
docker run \
  -it \
  --rm \
  ubuntu bash

apt update
apt install -y make curl shellcheck golang
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
curl -sS https://webinstall.dev/shfmt | bash

docker commit d68b0016c64a node-launcher-linter

docker run \
  -it \
  --rm \
  -v $(pwd):/mnt \
  -w /mnt \
  node-launcher-linter \
    bash -c "PATH=\"\$PATH:/root/.local/bin\" make lint"
```

```
helm dependency build
```

Build pipeline for node launcher fixed.  

It looks like there's a mismatch between dev intentions and the current state of
things, as we have all the docker images now contained within `ci/images` with
the intention of building everything under the `node-launcher` namespace and
referencing specific nodes by hash (they are also tagged `chain-version` but
we're using just the hashes for security)

--------------------------------------------------

Hey, so I'm noticing a bit of a disparity between the direction of the repo and
the current state of things. We're moving all the node images into `ci/images`
but we're still referencing the old images. Am I right in thinking we will
eventually make this kind of replacement to all the chains:
```
image: registry.gitlab.com/thorchain/devops/bitcoin-core
WITH
image: registry.gitlab.com/thorchain/devops/node-launcher:bitcoin-daemon-22.0
```

Is that going to be added soon?

--------------------------------------------------

Added another comment with my linting docker image steps, floated the idea of
including it.


### 09.05.2022 Monday

Just quickly updated the `node-launcher` PR. 10mins max, not charging for that.  
Apparently they already have an image for linting.  

### 10.05.2022 Tuesday

I want to see some brutal progress today. First half of the day, commence...

Will start with admin, catching up days. It's a good recap.  
Last batch paid out was 7th March.  
Need to claim 32hrs up until the start of today.  

Use this script to lint the `node-launcher` (courtesy of Asmund THORSec)
```
docker run \
  --rm \
  -it \
  -v $PWD:/repo \
  registry.gitlab.com/thorchain/devops/node-launcher@sha256:744718ddfad1948dfdb1342670aadf38f25b2472f9c5c56e42c260a4fc051011 \
    ./scripts/lint.sh
```

All green. Guess I'll get back to:
- [x] getting a local cluster running
- [ ] then completing the final piece of the puzzle, the smoke tests
- [x] Oh I'll check the thornode dash MR against develop too.
- [x] I agreed to try refactor thorchain to not use `gitlab.com/thorchain/bifrost/dash-txscript` along with Signer/Signable and just create a wrapper in the dash client.

I'm a little worried about my orchestrator bash shenanagins now. There are lots
of failed connection attempts and it's breaking things.

Well, that time I got lucky and everything worked.  
I have 2 thornodes, each bonded with 1 RUNE.  
Dash inbound address is listed correctly.  
Let's try a swap...  
Great success, both BCH->DASH and DASH->BCH seem good.  

Let's take a look at these smoke tests...  
Added new draft MR for Heimdall AKA smoke tests.  
Might make more sense to update `thornode` first actually.  

NOTE: I've done the following on special branch `982-add-dash-chain-local-cluster-fixes`:
Allow transactions with `TransactionSize` and `TransactionFeeRate` `== 0` because
otherwise the inbound address doesn't get generated on my local cluster. Also, 
set `AsgardSize` and `MinimumNodesForYggdrasil` `= 2` respectively, so that I
can test with just 2 thornode docker instances.

There's 6 or so references to `bifrostdashtxscript` which is the package I'd
like to do without. Luckily, they're ALL in `dash/signer.go`.

--------------------------------------------------

Refactor to remove the external dependency 'thornode/bifrost/dashd-txscript'

If you search the repo for '-txscript' you'll see many of the bifrost chain
clients currently using external packages at:
'gitlab.com/thornode/bifrost/<chain>-txscript'

These were originally added along with the 'Signable' interface to facilitate
either TSS or single private key signing.

This refactor updates the dash client to use a new func
'RawTxInSignatureUsingSignable' which allows signing using the
'bifrost/txscript.Signable' interface with the official 'dashd-go/txscript' 
package, removing the need for 'thornode/bifrost/dashd-txscript'.

--------------------------------------------------

`git checkout develop && git fetch && git pull`
`git diff 83d0cecc2..515e21ce3 -- ./bifrost`

I was using `Compare With...` in Goland to diff the dash and bitcoin clients.  
That could be useful when doing the dev/sec walkthrough.  
Alright dash MR is inline with develop changes.  
Back to `heimdall` smoke tests.  

What do I need to do/add/update?
- [ ] ./Dockerfile
- [ ] ./requirements.txt
- [ ] ./chains/aliases.py
- [ ] ./chains/dash.py
- [ ] ./data/smoke_test_balances.json
- [ ] ./data/smoke_test_events.json
- [ ] ./data/smoke_test_transactions.json
- [ ] ./scripts/smoke.py
- [ ] ./tests/test_smoke.py
- [ ] ./thorchain/thorchain.py
- [ ] ./utils/common.py

Switched back to `thornode` there for a minute as I realised the `./build`
directory has changed over to reference the `node-launcher`. Guessing that
happened while they were tackling the removal of the makefile madness, something
I'm very happy about. Added dash in there.

FYI/FMI AKA NOTE:  
The dash node launcher image will eventually be at:  
`registry.gitlab.com/thorchain/devops/node-launcher:dash-daemon-0.17.0.3`
(as soon as the node launcher maintainers merge dash and rerun `build.sh`)

Argh. There's a python dependency `https://pypi.org/project/python-dogecoin/`
referenced in `requirements.txt`. No such dash dependency. 

The github forks can be traced back as follows:  
https://github.com/amiller/bitcoin-python  
https://github.com/jcsaaddupuy/dogecoin-python  
https://github.com/bmwant/python-dogecoin  

So in theory, I could do the same for dash. I really don't want to do that.

Well, I'm no python developer, but as far as I can tell, that entire dependency
for doge is used once, to convert a public key to a p2pkh address string.

```python
from dogecointx.wallet import P2PKHDogecoinRegtestAddress
...
class MockDogecoin(HttpClient):
  ...
  def get_address_from_pubkey(cls, pubkey):
    return str(P2PKHDogecoinRegtestAddress.from_pubkey(pubkey))
```

Can't find any helpful commands to rebuild the image for local use. Pieced it
together using the cicd

```bash
cd build/docker
DOCKER_BUILDKIT=0 docker build \
  --build-arg TAG=mocknet \
  -t gitlab.com/thorchain/thornode:mocknet \
  -f Dockerfile \
  ../..
```

Ahh `Heimdall` docs are a bit behind now. This is no longer appropriate advice:

```bash
make -C build/docker reset-mocknet-standalone
```

We need to use the docker compose file:

```bash
export COMPOSE_PROFILES="mocknet,midgard"
export COMPOSE_PROJECT_NAME=thorchain

docker compose up -d
docker compose logs -f thornode bifrost
docker compose exec thornode sh
docker compose run /docker/scripts/hard-fork.sh
docker compose down -v
```

That is brilliant. Pretty much exactly what I did with my docker compose /
thornode-cluster repo, except it runs every chain. All we need is to be able to
disable chains via environment variables and that will be perfect.

Well, there's still a load of errors when you start it up which is extremely
jarring. I think we should disable vault migrations for non-mainnet or something.

```
E[2022-05-11 02:36:35,201] HTTPConnectionPool(host='localhost', port=8080): Max retries exceeded with url: /v2/pool/BNB.BNB (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fedf405ce80>: Failed to establish a new connection: [Errno 111] Connection refused'))
E[2022-05-11 02:36:35,201] Smoke tests failed
Traceback (most recent call last):
  File "/usr/local/lib/python3.10/site-packages/urllib3/connection.py", line 156, in _new_conn
    conn = connection.create_connection(
  File "/usr/local/lib/python3.10/site-packages/urllib3/util/connection.py", line 84, in create_connection
    raise err
  File "/usr/local/lib/python3.10/site-packages/urllib3/util/connection.py", line 74, in create_connection
    sock.connect(sa)
ConnectionRefusedError: [Errno 111] Connection refused
```

```
I[2022-05-11 02:39:25,607]  0     MASTER => CONTRIB    [SEED] 10.00000000 BNB.BNB
I[2022-05-11 02:39:25,621]  1     MASTER => USER-1     [SEED] 26.00000000 BNB.BNB, 1,500.00000000 BNB.LOK-3C0
I[2022-05-11 02:39:25,633]  2     MASTER => PROVIDER-1 [SEED] 10.00000000 BNB.BNB, 800.00000000 BNB.LOK-3C0
I[2022-05-11 02:39:25,666]  3     MASTER => PROVIDER-2 [SEED] 2.00000000 BNB.BNB, 100.00000000 BNB.LOK-3C0
I[2022-05-11 02:39:25,694]  4     MASTER => USER-1     [SEED] 2.00000000 BTC.BTC
I[2022-05-11 02:39:26,446]  5     MASTER => PROVIDER-1 [SEED] 5.00000000 BTC.BTC
I[2022-05-11 02:39:26,724]  6     MASTER => USER-1     [SEED] 200.00000000 DOGE.DOGE
I[2022-05-11 02:39:26,860]  7     MASTER => PROVIDER-1 [SEED] 2,000.00000000 DOGE.DOGE
I[2022-05-11 02:39:26,972]  8     MASTER => USER-1     [SEED] 500,000.00000000 TERRA.LUNA
I[2022-05-11 02:39:30,884]  9     MASTER => PROVIDER-1 [SEED] 500,000.00000000 TERRA.LUNA
I[2022-05-11 02:39:35,854] 10     MASTER => USER-1     [SEED] 500,000.00000000 TERRA.UST
I[2022-05-11 02:39:40,882] 11     MASTER => PROVIDER-1 [SEED] 500,000.00000000 TERRA.UST
I[2022-05-11 02:39:45,923] 12     MASTER => PROVIDER-2 [SEED] 5.00000000 BTC.BTC
I[2022-05-11 02:39:46,969] 13     MASTER => USER-1     [SEED] 2.00000000 BCH.BCH
I[2022-05-11 02:39:47,154] 14     MASTER => PROVIDER-1 [SEED] 2.00000000 BCH.BCH
I[2022-05-11 02:39:47,297] 15     MASTER => PROVIDER-2 [SEED] 2.00000000 BCH.BCH
I[2022-05-11 02:39:47,423] 16     MASTER => USER-1     [SEED] 2.00000000 LTC.LTC
I[2022-05-11 02:39:47,647] 17     MASTER => PROVIDER-1 [SEED] 2.00000000 LTC.LTC
I[2022-05-11 02:39:47,924] 18     MASTER => PROVIDER-2 [SEED] 2.00000000 LTC.LTC
I[2022-05-11 02:39:48,251] 19     MASTER => USER-1     [SEED] 400,000,000,000.00000000 ETH.ETH
E[2022-05-11 02:39:48,374] {'code': -32000, 'message': 'insufficient funds for gas * price + value'}
```

Unfortunately, both my first two runs of `make smoke` failed, and I haven't
changed anything yet. Perhaps I just need to wait a bit longer?

Gets to test `26` again and fails at: `/v2/pool/BNB.BNB`

`http://localhost:6040/p2pid`
`http://localhost:8080/v2/pool/BNB.BNB`

Switched from using my cluster `github.com/alexdcox/thornode-cluster` to using
the docker compose in the actual `thornode` repo, added a script simmilar to
`thornode.sh` to my private scripts `./_adc/docker-compose-mocknet.sh` which
just loops up/down when I hit the return key.

Need to be sure to set both `mocknet` and `midgard` in profiles or else the
smoke tests will fail.

Waiting till thorchain block `20` at least.

Oh fuck ???? Failed at `46` now:

```
I[2022-05-11 03:19:07,431] 46 PROVIDER-1 => VAULT      [SWAP:BNB.BNB:PROVIDER-1] 0.10000000 BTC/BTC
E[2022-05-11 03:19:53,240] Midgard   [BNB.BNB        ] RUNE  [T]964.88003016 != [M]918.42871797 [DIFF] 4.93295% (4,645,131,219)
E[2022-05-11 03:19:53,240] Smoke tests failed
Traceback (most recent call last):
  File "/app/scripts/smoke.py", line 136, in main
    smoker.run()
  File "/app/scripts/smoke.py", line 646, in run
    self.run_health()
  File "/usr/local/lib/python3.10/site-packages/tenacity/__init__.py", line 311, in wrapped_f
    return self.call(f, *args, **kw)
  File "/usr/local/lib/python3.10/site-packages/tenacity/__init__.py", line 391, in call
    do = self.iter(retry_state=retry_state)
  File "/usr/local/lib/python3.10/site-packages/tenacity/__init__.py", line 350, in iter
    raise retry_exc.reraise()
  File "/usr/local/lib/python3.10/site-packages/tenacity/__init__.py", line 168, in reraise
    raise self.last_attempt.result()
  File "/usr/local/lib/python3.10/concurrent/futures/_base.py", line 439, in result
    return self.__get_result()
  File "/usr/local/lib/python3.10/concurrent/futures/_base.py", line 391, in __get_result
    raise self._exception
  File "/usr/local/lib/python3.10/site-packages/tenacity/__init__.py", line 394, in call
    result = fn(*args, **kwargs)
  File "/app/scripts/smoke.py", line 372, in run_health
    self.health.run()
  File "/app/scripts/health.py", line 95, in run
    self.check_pools()
  File "/app/scripts/health.py", line 153, in check_pools
    self.error(
  File "/app/scripts/health.py", line 105, in error
    raise Exception(err)
Exception: Midgard   [BNB.BNB        ] RUNE  [T]964.88003016 != [M]918.42871797 [DIFF] 4.93295% (4,645,131,219)
make: *** [smoke] Error 1
```

I have a sneaky suspicion this is actually just because my lappy is old and slow
and the smoke tests don't retry if it gets a 200 response but with incorrect
values. All guesswork o course.

Hmmm. I'll try again. Closed some non-essential apps and some project windows...

Failed at `41`.  
Again. Closing everything, even this note... brb...  
Got all the way to `90` that time. Hmm. Maybe I should run this on my other pc.

Running linux in a new virtualbox instance and setting it up...

### 11.05.2022 Wednesday

Finished setting up ubuntu server with all the prerequisites.  
Now on to actually testing.  

- `mkdir /go/src`
- clone `thornode`, `heimdall`, `node-launcher`
- add my forks as git origins, switch to dash branches
- run (modified - no dockerhub) `./ci/images/build.sh`

Notes while doing the above:
- might be nice to update `ci/images/build.sh` to not use dockerhub and just build the images locally, perhaps hub push can be a separate script

Getting some werid docker crazyness
> unable to prepare context: unable to evaluate symlinks in Dockerfile path: lstat /var/lib/snapd/void/Dockerfile: no such file or directory

Had to uninstall docker snap and install via apt instead.

```bash
cd /go/src/gitlab.com/thorchain/thornode
cd /go/src/gitlab.com/thorchain/devops/node-launcher
cd /go/src/gitlab.com/thorchain/heimdall
```

```bash
export COMPOSE_PROFILES="mocknet,midgard"
export COMPOSE_PROJECT_NAME=thorchain
```

```bash
while true; do
  docker-compose up --remove-orphans -d
  echo -n "Press enter to STOP thorchain..."
  read ignored

  docker-compose down --volumes
  echo -n "Press enter to RESTART thorchain..."
  read ignored
done
```

```bash
docker-compose logs -f thornode bifrost

make smoke
```

Is it possible we'll set a new high score?

Bear in mind, these are now running on a 16GB/4-core vm with an nvme drive. If
this doesn't pan out, the tests definitely need some work.

`96`! ????????????

The whole thing takes quite a while though. 20mins so far and reached `110`.

`119` and DONE!!! Yesss. 23 minutes.

Now to do all that with Dash added to `heimdall`.
- [x] ./Dockerfile (going to try and avoid the need for python-dash)
- [x] ./requirements.txt (skip, same reason)
- [x] ./chains/aliases.py
- [ ] ./chains/dash.py
- [ ] ./data/smoke_test_balances.json
- [ ] ./data/smoke_test_events.json
- [ ] ./data/smoke_test_transactions.json
- [ ] ./scripts/smoke.py
- [ ] ./tests/test_smoke.py
- [ ] ./thorchain/thorchain.py
- [ ] ./utils/common.py

Is it possible to convert from `Bech32PrefixAccAddr` node account address
to a p2pkh address?


```bash
NET=mocknet go run ./tools/pubkey2address -p tthorpub1addwnpepqvw0532tjm6skvc7wl02nflv97za4l0zd76z4xvya6935mwku65r5z2p6an
```

tthor is the address prefix
tthorpub is the public key prefix

I always forget the process to replace a dependency with an alias, so here it is:
1. Try and get the replacement package specifying an exact commit. This will fail,
  because the url will point to a forked package with the original package name. That's ok.
2. Use the output of that to add the `go.mod` `replace` directive.
3. `go get` the original package (which will silently fetch the new/replacement package instead)

```
go get -v gitlab.com/alexdcox/thornode@1aa57d788
gitlab.com/thorchain/thornode => gitlab.com/alexdcox/thornode v0.68.1-0.20220511214941-1aa57d7887b0
go get gitlab.com/thorchain/thornode
```

Morale of the story, don't use branch names!

```
master
priv: ef235aacf90d9f4aadd8c92e4b2562e1d9eb97f0df9ba3b508258739cb013db2
pub:  02b4632d08485ff1df2db55b9dafd23347d1c47a457072a1e87be26896549a8737
eth:  0x3fd2d4ce97b082d4bce3f9fee2a3d60668d2f473
bnb:  bnb1j08ys4ct2hzzc2hcz6h2hgrvlmsjynawtf2n0y
btc:  bc1qj08ys4ct2hzzc2hcz6h2hgrvlmsjynawlht528
ltc:  ltc1qj08ys4ct2hzzc2hcz6h2hgrvlmsjynawmt3sjh
bch:  qzfuujzhpd2ugtp2lqt2a2aqdnlwzgj04cswjhml4x
dash: XpANHDZNTgEyM2FN8QjERafkRaK4X8Uaeq
doge: DJcczDr7oNvfj5qP17Qa7p9ZUNTfnYYDJC

contrib
priv: 289c2857d4598e37fb9647507e47a309d6133539bf21a8b9cb6df88fd5232032
pub:  037db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf7
eth:  0x970e8128ab834e8eac17ab8e3812f010678cf791
bnb:  bnb1zupk5lmc84r2dh738a9g3zscavannjy3nkkcrl
btc:  bc1qzupk5lmc84r2dh738a9g3zscavannjy38ghlxu
ltc:  ltc1qzupk5lmc84r2dh738a9g3zscavannjy3r5dm7v
bch:  qqtsx6nl0q75dfkl6yl54zy2rr4nkwwgjyzgwf5228
dash: XcnXU1m6d1pkoCd17SgknUdgV1dbPvBrcU
doge: D7EnB23qxiWTBGD1z9N6Ui7VXonCgY9eeE

user1
priv: e810f1d7d6691b4a7a73476f3543bd87d601f9a53e7faf670eac2c5b517d83bf
pub:  03f98464e8d3fc8e275e34c6f8dc9b99aa244e37b0d695d0dfb8884712ed6d4d35
eth:  0xf6da288748ec4c77642f6c5543717539b3ae001b
bnb:  bnb1qqnde7kqe5sf96j6zf8jpzwr44dh4gkddg5yfw
btc:  bc1qqqnde7kqe5sf96j6zf8jpzwr44dh4gkdek4rvd
ltc:  ltc1qqqnde7kqe5sf96j6zf8jpzwr44dh4gkda2085a
bch:  qqqzdh86crxjpyh2tgfy7gyfcwk4k74ze522f8panm
dash: XahePWt94WHuFrfABrfAaqDKZWvqEjuqVV
doge: D59u6XAtQCybdvFB4ZLWH4h8cK5SY8show

provider1
priv: a96e62ed3955e65be32703f12d87b6b5cf26039ecfa948dc5107a495418e5330
pub:  02950e1cdfcb133d6024109fd489f734eeb4502418e538c28481f22bce276f248c
eth:  0xfabb9cc6ec839b1214bb11c53377a56a6ed81762
bnb:  bnb10s4mg25tu6termrk8egltfyme4q7sg3hm84ayj
btc:  bc1q0s4mg25tu6termrk8egltfyme4q7sg3h0e56p3
ltc:  ltc1q0s4mg25tu6termrk8egltfyme4q7sg3ht9w7ep
bch:  qp7zhdp230nf0y0vwcl9radyn0x5r6pzxuqvhx5vs3
dash: Xn1PydbxxPrTHq4heBc2jr81gQ9qcdUp1X
doge: DGTegdtiJ6Y9fteiWtHNS5bpjCJSrY4Kiz

provider2
priv: 9294f4d108465fd293f7fe299e6923ef71a77f2cb1eb6d4394839c64ec25d5c0
pub:  0238383ee4d60176d27cf46f0863bfc6aea624fe9bfc7f4273cc5136d9eb483e4a
eth:  0x1f30a82340f08177aba70e6f48054917c74d7d38
bnb:  bnb1jw8h4l3dtz5xxc7uyh5ys70qkezspgfuh4nh0z
btc:  bc1qjw8h4l3dtz5xxc7uyh5ys70qkezspgfurtjs2p
ltc:  ltc1qjw8h4l3dtz5xxc7uyh5ys70qkezspgfu8hg5j3
bch:  qzfc77h794v2scmrmsj7sjreuzmy2q9p8sxs8lu34e
dash: Xp953eZGiFzHfr5wHuA9DBTzxS37JMNykT
doge: DJbKker23xfz3ufxAbqUuQwp1EBibGJJHu
```

Can you run the smoke tests against a subset?

```bash
docker run \
  -it \
  --network=host \
  --rm \
  -e RUNE=THOR.RUNE \
  -e LOGLEVEL=INFO \
  -e PYTHONPATH=/app \
  -e BLOCK_SCANNER_BACKOFF=0.8s \
  -v $(pwd):/app \
  -w /app \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --fast-fail=True
```

```
logging.info(f"--> {pubkey.hex()}")
logging.info(f"<-- {str(P2PKHDogecoinRegtestAddress.from_pubkey(pubkey))}")
```

This is the output for doge (before it fails):
> I[2022-05-11 23:48:53,589] --> 026fa0929eba67e7fbe28eb500e530addf8c37b40aaa2ac5cc286e51919c2d76fc
  I[2022-05-11 23:48:53,590] <-- n33GAjMrho9Bd6pz11e1Ea1vhUvrDcQik8

Need to do this conversion for dash without a library.

public key bytes uncompressed -> sha256 -> ripemd160 = pkhash  
(0x4c + pkhash) = netpkhash  
netpkhash -> sha256 -> sha256 -> last4 = checksum  
(netpkhash + checksum) -> base58 = p2pkh address  

Am I going to have to make this for dash?  
`https://gitlab.com/thorchain/bifrost/python-dogecointx`  

I'll try...
`https://gitlab.com/alexdcox/python-dash`  

Need to populate these values:

- P2SHDashAddress
- P2SHDashLegacyAddress
- P2SHDashTestnetAddress
- P2SHDashTestnetLegacyAddress
- P2SHDashRegtestAddress
- P2SHDashRegtestLegacyAddress
- P2PKHDashAddress
- P2PKHDashTestnetAddress
- P2PKHDashRegtestAddress
- CDashKey
- CDashTestnetKey
- CDashRegtestKey
- CDashExtPubKey
- CDashExtKey
- CDashTestnetExtPubKey
- CDashTestnetExtKey
- CDashRegtestExtPubKey
- CDashRegtestExtKey

Ooooooooooooooooooooooot of time.

### 12.05.2022 Thursday

- [x] Follow `thornode` merge reques comments/suggestions from `Eridanus`...
- [ ] Fix `thornode` pipeline
  - [ ] gosec-sast

    ```
    go install github.com/securego/gosec/v2/cmd/gosec@latest
    gosec ./...
    ```

    It shows 2 issues with my stuff and 5 issues with other things.  
    `Eridanus` said he'd take a look tomorrow.  
    I'll just sort the dash issues if I can...  

  - [x] lint

    `make lint`

    > xargs: gofumpt: No such file or directory
    
    `go install mvdan.cc/gofumpt@latest`

    > make: trunk: No such file or directory
    
    `brew install trunk`

    > error: Found argument 'check' which wasn't expected, or isn't valid in this context
    
    Wrong trunk.

    `curl https://get.trunk.io -fsSL | bash`

    Okay it doesn't like the way I did the bifrost config with handlebar style templates.
    Fair enough. I'll switch to jq and json path updates.

    The linter is absurdly strict in some cases. It doesn't like arrays with one
    value spanning multiple lines:

    ```json
    "addresses": [
      "XoSxpd5VYNQvKbXbEaDKt6P1aZANzAkXrJ"
    ]
    ```

    Has to be:

    ```json
    "addresses": ["XoSxpd5VYNQvKbXbEaDKt6P1aZANzAkXrJ"]
    ```

    ...or it fails the lint check and the build pipeline fails. This is a bit
       ridiculous, especially seeing as my format is how the dash-cli response
       is actually returned.

    How to improve the linter IMO:
    - Allow array blocks to span any x lines
    - Don't enfore json files to end with a single empty line
  
    Well, you can `cd` and run `trunk fmt` so at least there's that.

  - [ ] secret_detection

  ```
  brew install gitlab-runner
  brew services start gitlab-runner
  gitlab-runner install
  gitlab-runner start

  gitlab-runner exec docker lint
  gitlab-runner exec docker unit-tests
  gitlab-runner exec docker smoke-test
  ```

  No lappy space left ><
  

### 13.05.2022 Friday

- [ ] Fix `thornode` pipeline
  - [x] secret_detection

  I'm thinking I should probably run this on the Ubuntu vm rather than my laptop
  seeing as it couldn't handle running `make lint` directly and the gitlab
  runner involves nested vms.

  ```bash
  curl -LJO "https://gitlab-runner-downloads.s3.amazonaws.com/latest/deb/gitlab-runner_amd64.deb"
  dpkg -i gitlab-runner_amd64.deb
  sudo gitlab-runner start

  gitlab-runner exec docker lint
  ```

  It runs this:
  ```bash
  trunk check --no-progress --monitor=false --upstream origin/develop
  ```

  The `--upstream` flag is a bit worrying, i'm not using `origin` but `alex` and
  I'm on branch `982-add-dash-chain` not `develop`.

  Also that doesn't log any progress to the stdout which is a pretty horrible
  user experience, just looks like it's hanging for ages.

  ```bash
  trunk check --upstream origin/develop
  ```

  ```bash
  gitlab-runner exec docker secret_detection
  ```

  > FATAL: missing 'script' for job

  `/etc/gitlab-runner/config.toml`

  ```bash
  gitlab-runner run test
  ```

  Okay took me a while, but the `github-runner` doesn't support running
  everything, as would be the case when a commit is pushed to a new branch.
  Also, it doesn't support "secret variables" which I'm assuming is this
  secret_detection step.

  - [x] unit-tests

  ```bash
  gitlab-runner exec docker unit-tests
  ```

  Out of space. Hmm. Had to follow this guide because ubuntu installed and only
  used 50% of the disk space:  
  https://askubuntu.com/questions/1106795/ubuntu-server-18-04-lvm-out-of-space-with-improper-default-partitioning


  ```bash
  make test-coverage-sum
  ```

  Beaut. All green.

  - [x] semgrep

  ```
  gitlab-runner exec docker semgrep
  ```

  We're done here.

```
gitlab-runner exec docker smoke-test
```

- [x] ./Dockerfile (going to try and avoid the need for python-dash)
- [x] ./requirements.txt (skip, same reason)
- [x] ./chains/aliases.py
- [ ] ./chains/dash.py

- [ ] ./data/smoke_test_balances.json
- [ ] ./data/smoke_test_events.json
- [ ] ./data/smoke_test_transactions.json

- [x] ./scripts/smoke.py
- [x] ./tests/test_smoke.py
- [x] ./thorchain/thorchain.py (NEED TO CONFIRM SOME FIGURES, SEARCH TODO)
- [x] ./utils/common.py

It looks like this: https://medium.com/free-code-camp/how-to-create-a-bitcoin-wallet-address-from-a-private-key-eca3ddd9c05f
is exactly what I'm looking for with regard to `get_address_from_pubkey`.

https://github.com/Destiner/blocksmith/blob/master/blocksmith/bitcoin.py#L48

```python
def __public_to_address(public_key):
    public_key_bytes = codecs.decode(public_key, 'hex')
    # Run SHA256 for the public key
    sha256_bpk = hashlib.sha256(public_key_bytes)
    sha256_bpk_digest = sha256_bpk.digest()
    # Run ripemd160 for the SHA256
    ripemd160_bpk = hashlib.new('ripemd160')
    ripemd160_bpk.update(sha256_bpk_digest)
    ripemd160_bpk_digest = ripemd160_bpk.digest()
    ripemd160_bpk_hex = codecs.encode(ripemd160_bpk_digest, 'hex')
    # Add network byte
    network_byte = b'00'
    network_bitcoin_public_key = network_byte + ripemd160_bpk_hex
    network_bitcoin_public_key_bytes = codecs.decode(network_bitcoin_public_key, 'hex')
    # Double SHA256 to get checksum
    sha256_nbpk = hashlib.sha256(network_bitcoin_public_key_bytes)
    sha256_nbpk_digest = sha256_nbpk.digest()
    sha256_2_nbpk = hashlib.sha256(sha256_nbpk_digest)
    sha256_2_nbpk_digest = sha256_2_nbpk.digest()
    sha256_2_hex = codecs.encode(sha256_2_nbpk_digest, 'hex')
    checksum = sha256_2_hex[:8]
    # Concatenate public key and checksum to get the address
    address_hex = (network_bitcoin_public_key + checksum).decode('utf-8')
    wallet = base58(address_hex)
    return wallet

def base58(address_hex):
    alphabet = '123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz'
    b58_string = ''
    # Get the number of leading zeros and convert hex to decimal
    leading_zeros = len(address_hex) - len(address_hex.lstrip('0'))
    # Convert hex to decimal
    address_int = int(address_hex, 16)
    # Append digits to the start of string
    while address_int > 0:
        digit = address_int % 58
        digit_char = alphabet[digit]
        b58_string = digit_char + b58_string
        address_int //= 58
    # Add '1' for each 2 leading zeros
    ones = leading_zeros // 2
    for one in range(ones):
        b58_string = '1' + b58_string
    return b58_string
```

### 17.05.2022 Tuesday

On with trying to get the python pubkey to address code working...

```
Network Agnostic
private hex (32 bytes):              c03d33d24a4f01109233fe76c247dfe8d80e15416e15d83960636dd2b016f237
public uncompressed hex (65 bytes):  0429277cdf6c0ee28124c8c68b03675582b6fc4ee4e09944c816ace1b8469626d257bf607aab190cb7f01a3d76b96f8d405b6f593bdb487c3c2a3fb89f3d5bd455
public compressed hex (33 bytes):    0329277cdf6c0ee28124c8c68b03675582b6fc4ee4e09944c816ace1b8469626d2
public s256:                         cf965936a64376b30f709f3a28852369cd7ee90c22c35b28451f431b199a7a76
public ripemd160 hash:               7941ed2d195d32afcd0632fe1482b3d576d39711

Testnet / Regtest
private wif (uncompressed): 933aenYLSA25ppgaAg4YtU7QgZcUx396ZNStAdEBMPkq1A47r3m
private wif (compressed):   cU2PXn1Jn2onJ5TfPhQfkAfHXcwcMvSjXsfEqUuAh1SSsLfaUJ5s
p2pkh:              yXNbb4n4XefV5FtrhsoXEwRF9nqvKrVpH4
txscript p2pkh asm: OP_DUP OP_HASH160 7941ed2d195d32afcd0632fe1482b3d576d39711 OP_EQUALVERIFY OP_CHECKSIG:
txscript p2pkh hex: 76a9147941ed2d195d32afcd0632fe1482b3d576d3971188ac
p2sh:               1P6oz3gjgxfcMuGUacvMdeSy7PAgfVFXsi

checksum  
expected: c982672f  
actual:   7311cbf9  
```

### 18.05.2022 Wednesday

Okay wasn't using the python byte format correctly. Needed to be `b'\x8c'`
rather than `b'76'` (attempting to set in base 10 didn't work). Also wasn't
using the pubkey hash for the address data, but the raw bytes. Oops.

Now that's out the way I have a working (presumably) `dash.py` file. Just need
to add dash tx data now. 

- [x] ./data/smoke_test_transactions.json
  Transactions:
  - [x] Seed
  - [x] Vault Add
  - [x] Swap
  - [x] Vault Withdrawal

- [x] ./data/smoke_test_events.json

- [ ] ./data/smoke_test_balances.json

Enable DASH txs in smoke tests

> /docker/scripts/bifrost.sh: no such file or directory

Finding it difficult to debug this because the volume seems to be mounted
correctly and I can't freeze the  container with `tail -f /dev/null` because
the image
`registry.gitlab.com/thorchain/thornode:runner-base-v1@sha256:8fc433efa3e853b59cafe920654705e37c94228ae99cba6892933a61594c11f3`
doesn't even have `bash`, let alone `tail`.

I'll try `sleep 999999999`

> bifrost_1       | /bin/sleep: line 1: ELF: not found
> bifrost_1       | /bin/sleep: line 2: P: not found
> bifrost_1       | /bin/sleep: line 3: P: not found
> bifrost_1       | /bin/sleep: line 6: syntax error: unterminated quoted string

Managed to get into the container with:

```bash
entrypoint: /bin/sh
command: ["-c", "apk update && apk add bash coreutils && /usr/bin/tail -F /dev/null"]
```

> parse error: Invalid numeric literal at line 10, column 36

Getting this in the bifrost log. No idea why.

### 20.05.2022 Friday

Right, can I get the smoke tests done?

Noticed notes on node-launcher, updated MR.

That was it, having an issue with the `bifrost.sh`. Quick google of the error
and it seems like that's coming from `jq`. Let's dump the output...

I was using an outdated docker image for bifrost, which still had handlebar
template format for `/scripts/bifrost-config-template.json` and therefore didn't
parse with jq. Rebuilt container.

Message from Asmund THORSec:

> Thank you for the contribution, and the iterations on it. This is ready to
  merge (pending the rest of the approvals)

WOOP WOOP ???? That's the sound of the beast.

Okay so now bifrost is exiting with code 0. Very odd. Last log message is:
> Checking if THORNode Thor 'thorchain' account exists

Ahh I deleted the `exec "@?"` thingy at the end of the bifrost entrypoint script
as well as the `command` in `docker-compose`, to match thornode. Needed to
append the bifrost command to the script.

Running the smoke tests again... Python error:

> ValueError: Unknown chain 'dash/regtest'

Damn. I think there's some python magic going on here. Looks like a "magic" init
file here: `dogecointx/__init__.py` that I'm guessing is loaded when that
dependency is imported. It sets the `dogecoin/{mainnet,testnet,regtest}` params.

Hmm.. I Really didn't want another dependency but I feel like I don't have much
choice. They  didn't need to do this with Terra because there's a python sdk.

Double checked if `dashpay` official github has any python repos. It does, but
they're old and don't seem particularly relevant.

On with https://gitlab.com/alexdcox/python-dashtx then it seems. Yet another
repo to (create, modify, get approved, maintain), this time in a different
programming language. Talk about barriers to entry.

```
Python Variable               Doge (int|hex|base58)   Dash
P2SH____Address                22|      16|9,A ???     16|      10|7
P2SH____LegacyAddress          22|      16|9,A ???     16|      10|7
P2SH____TestnetAddress        196|      c4|2           19|      13|8
P2SH____TestnetLegacyAddress  196|      c4|2           19|      13|8
P2SH____RegtestAddress        196|      c4|2           19|      13|8
P2SH____RegtestLegacyAddress  196|      c4|2           19|      13|8  
P2PKH____Address               30|      1e|D           76|      4c|X
P2PKH____TestnetAddress       113|      71|n          140|      8c|y
P2PKH____RegtestAddress       111|      6f|m,n        140|      8c|y
C____Key                      158|      9e|6,Q ???    204|      cc|7,X
C____TestnetKey               241|      f1|9          239|      ef|9,c
C____RegtestKey               239|      ef|9,c        239|      ef|9,c
C____ExtPubKey                   |02FACAFD|dgub          |0488b21e|xpub
C____ExtKey                      |02FAC398|dgpv          |0488ade4|xprv
C____TestnetExtPubKey            |043587CF|tpub          |043587CF|tpub        
C____TestnetExtKey               |04358394|tprv          |04358394|tprv        
C____RegtestExtPubKey            |043587CF|tpub          |043587CF|tpub        
C____RegtestExtKey               |04358394|tprv          |04358394|tprv        
```

Got a bit stuck for a minute trying to convert from the hex to the letter to
double check this, but remember, the address should be 25 bytes, and the first
byte of the base58 encoding is the length. It worked when I used this in cyber
chef:

`8c000000000000000000000000000000000000000000000000`
from hex
to base58
take bytes(0,1)

Having trouble reconciling the P2SHDogecoinAddress. 22 decimal is 16 in hex
which when appended to a 25 byte address comes out as `9` or `A`.

Doge in goland has this and I get `6` or `Q`:
```
PrivateKeyID:            0x9E, // 158 starts with 5 (uncompressed) or K (compressed)
```

TODO: The go code comment in doge says starts with `3`. I need to confirm this is wrong.
TODO: The go code comment for dash also seems wrong:
```
ScriptHashAddrID:        byte(19), // starts with 2
```
I make that `8`??!

`933aenYLSA25ppgaAg4YtU7QgZcUx396ZNStAdEBMPkq1A47r3m`
`efc03d33d24a4f01109233fe76c247dfe8d80e15416e15d83960636dd2b016f237b5bc3a44`
private wif - uncompressed | 37 bytes, 74 hex | ef | byte(239) | base58:9

`cU2PXn1Jn2onJ5TfPhQfkAfHXcwcMvSjXsfEqUuAh1SSsLfaUJ5s`
`efc03d33d24a4f01109233fe76c247dfe8d80e15416e15d83960636dd2b016f23701d67d5e46`
private wif - compressed   | 38 bytes, 76 hex | ef | byte(239) |  base58:c

Here's another discrepency. For dash `PrivateKeyID` we have `byte(204)` but
using the scripts I've already used to import keys, I'm seeing `0xef` or
`byte(239)`.

For doge mainnet we have `0x9e` in the code and `byte(158)` and base58:`5`
compressed and base58:`K` uncompressed. Let's check:
`9e000000000000000000000000000000000000000000000000000000000000000000000000`
`6`

`9eff0000000000000000000000000000000000000000000000000000000000000000000000`
`6`

`9e00000000000000000000000000000000000000000000000000000000000000000000000000`
`Q`

`9eff000000000000000000000000000000000000000000000000000000000000000000000000`
`Q`

`cc00000000000000000000000000000000000000000000000000000000000000000000000000`
`X`

`cc000000000000000000000000000000000000000000000000000000000000000000000000`
`7`

`ef00000000000000000000000000000000000000000000000000000000000000000000000000`
`c`

`ef000000000000000000000000000000000000000000000000000000000000000000000000`
`9`

Yeah I think all the comments are wrong. Quite misleading. Going by the code...

`043587CF000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000`
`tpub`


https://gitlab.com/alexdcox/python-dashtx
https://gitlab.com/thorchain/bifrost/python-dashtx

Might have found a bit of an issue with `heimdall`. If you want to add a new
chain you have to include new python dependencies. These are baked into the
container, and the container is always pulled from the registry on `make
smoke`. So any attempt to update the dependencies is ignored, so the tests will
fail.

Perhaps `imagePullPolicy: IfNotPresent` and building locally is a good solution?

Also, why does `make build` pull the image it's trying to build before building
over it? That seems a bit crazy. Surely it would fetch anything it needs in the
build. What happens when the chicken comes before the egg? Why is a raven like
a writing desk?

>   Resolved https://gitlab.com/alexdcox/python-dashtx.git to commit a14d9420369644a83060df8c82dedc225e7b3dfd

Ahh looks like there's a hard-coded reference to a commit somewhere?

TBC next time...

### 21.05.2022 Saturday

No really, it is a Saturday. It's a lovely day outside. Sunny. Warm. I'm going
to work. You might ask me where my sanity has gone. I did skip work on Thursday,
so I'm back-filling that missed day on my schedule. That's why.

So with that. Here goes.


Need commit `a25cd91`

`pip3 install git+https://gitlab.com/alexdcox/python-dashtx.git#egg=python-dashtx`

> raise ImportError('secp256k1 library not found')

Oh?

`pip3 install git+https://gitlab.com/thorchain/bifrost/python-dogecointx.git#egg=python-dogecointx`

Yeah the TC version of dogecoin python raises the same error.

Feel like it can't be right that I have to do this just to use an import.  
Shouldn't the import have it's own list of dependencies??  

```
pip3 install secp256k1
```

Doesn't seem to help.

This is what is says it's doing:

```
git clone --filter=blob:none --quiet https://gitlab.com/alexdcox/python-dashtx.git /tmp/pip-install-um8vk0mi
```

Ahh I actually had two repos `python-dash` and `python-dashtx` and forgot to
delete the former. That was confusing. Looks like the build is going to work
now.

> ValueError: Unknown chain 'dash/regtest'

Dejavu. Argh.

```
docker run \
  -it \
  --rm \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
  python

```

```python
from bitcointx import select_chain_params

from dogecointx.wallet import P2PKHDogecoinRegtestAddress
select_chain_params('dogecoin/mainnet')

from dashtx.wallet import P2PKHDashRegtestAddress
select_chain_params('dash/regtest')
```

Okay that actually worked. What about `regtest`? Yep. No problem.

- [ ] TODO: Need to find out the size of the withdrawal tx so I can set an
  estimate in heimdall.


```
docker run \
  -it \
  --rm \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --generate-balances=True
```

Realised I put dash mainnet addresses in the alias section, also missed a few
references in there for dash.

> Cannot transfer. No DASH UTXO available for yZnyJAdouDu3gmAuhG3dTc66hroS4AXxnL

So I need the node to be generating to that address it seems. How do the other
nodes configure this?


### 22.05.2022 Sunday

Just getting the DI account squared away at the moment...  
Last comment on DI was 24.03.2022  
That was paying out my work up to the 07.03.2022  
74.5hrs to claim from 29.03.2022 to 22.05.2022 (today).  


### 23.05.2022 Monday

New thornode stack on vm.  
Waiting for block 20.  
Rerunning the smoke tests.  
Oh same error about the utxo. Did I rebuild the dash docker image?  
Clearly not, rebuilt, restarting stack, waiting for 20...  
Smoking.  
Same deal. Now that's worrying. What happens when I just run the thing? Scratch
that I didn't pull `node-launcher` changes. Cycling back.  
Smoking.  

> E[2022-05-23 20:03:27,228] {"result":null,"error":{"code":-32,"message":"signrawtransaction is deprecated and will be fully removed in v0.18. To use signrawtransaction in v0.17, restart dashd with -deprecatedrpc=signrawtransaction.\nProjects should transition to using signrawtransactionwithkey and signrawtransactionwithwallet before upgrading to v0.18"},"id":null}

Ahh. I've seen that before on other chains.  

`signrawtransactionwithkey`  
`signrawtransactionwithwallet`  

Okay updated, pushed locally, pulled on vm, restarting stack, waiting for 20...  
Smoking.  

> E[2022-05-23 20:18:01,144] Smoke tests failed
Traceback (most recent call last):
  File "/app/scripts/smoke.py", line 143, in main
    smoker.run()
  File "/app/scripts/smoke.py", line 639, in run
    self.broadcast_chain(txn)
  File "/app/scripts/smoke.py", line 403, in broadcast_chain
    return self.mock_dash.transfer(txn)
  File "/app/chains/dash.py", line 222, in transfer
    tx_in = [{"txid": unspent["txid"], "vout": unspent["vout"]}]
KeyError: 'txid'
make: *** [Makefile:42: smoke] Error 1

Is that saying there's no `txid` field as part of the unspent?

```python
default_gas = 100000
...
min_amount = float(amount + (self.default_gas / Coin.ONE))  # add more for fee
```

`100000 / 100000000 = 0.001`  
I'm generating `500.0` at a time so surely that's ok.  

Maybe this is where the issue lies:  
`unspents = self.call("listunspent", 1, 9999, [str(address)])`

What address is it asking for? Maybe that address doesn't resunt in an utxo
selection because there are none to choose from?

Added some extra logging:

```python
logging.warning("Selecting UTXO for: " + str(address))
```
  
Oh it's because I'm trying to send 2K dash and all the utxos are 500 max. Riight.

Need to rework some of the tx values in the heimdall data file to match the 500
limit. At one point there's a 2K tx which will of course fail.

Okay updated transaction data, push/pull, new stack, waiting for 20...  
Running regenerate balances, perhaps we could just have a script for this too?...  
If `heimdall` was in go, we could use the same core logic for pools, and then
just have a mock thorchain network run instantly and print the balances from that, right?  

Running generate balances only... ????  
I'm getting the same error:  
> Exception: Address for alias not found, chain not supported (DASH)

Which tells me the scripts are built into the `heimdall` docker image. I changed
that to actually print the alias that wasn't found to help with debugging.  
Rebuilt  
Re done did all the things.  
Running the `smoke.py --generate-balances=Yesdeargodpleasedothat` ????????????  

Loads of errors. I might need to ask for help with this.  
I asked heimdall. That seemed appropriate.  
Also reached out to Eridanus at 9R as he seems to know what he's doing.  

My best guess is that I'm asking it to do something it can't do, so the expected
event never gets fired.

> thornode_1      | 1:23AM INF receive MsgDeposit coins=[{"amount":"50000000000","asset":"THOR.RUNE"}] from=tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257 memo=SWAP:BNB.BNB:tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257
> thornode_1      | 1:23AM ERR fail to process native inbound tx error="swap destination address is not the same chain as the target asset: unknown request" tx hash=3715CDF3EF26C444F89C00C9980EBCB4BC114BD8115E0FE70F2D83F3EECF296C


```
address tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257    
alias   provider_1
type    SWAP
dest    BNB.BNB
amount  50000000000
asset   THOR.RUNE
```

So it's trying to send to itself? So I'm trying to match this error with the
transactions data...

> thornode_1      | 1:24AM INF receive MsgDeposit coins=[{"amount":"100000000000","asset":"THOR.RUNE"}] from=tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257 memo=SWAP:BNB.BNB:tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257
> thornode_1      | 1:24AM ERR fail to process native inbound tx error="swap destination address is not the same chain as the target asset: unknown request" tx hash=F82B68B4AA3094056144DAB5991F45D49EBEA4F36825D6F240A769BE5146F63F

Okay here's a question. If I revert all my dash stuff, will it work? Because
BNB.BNB is the thing that's broken and I haven't touched that.

```
git checkout develop -- data/smoke_test_transactions.json
EXPORT=data/smoke_test_balances.json EXPORT_EVENTS=data/smoke_test_events.json make test
make smoke
```

Yeah, they fail. That's actually good. Now I can diff my generated events with
the develop branch compiled events and see what is breaking it...  

```
git diff --cached develop
```

Nothing major. Bit difficult to see being on my branch. Going to do it on a clean
branch.

Using main branch doesn't cause any issues. I'm lost.

```
git checkout 982-add-dash-chain
git checkout develop -- data/smoke_test_transactions.json
EXPORT=data/smoke_test_balances.json EXPORT_EVENTS=data/smoke_test_events.json make test
git add -A
git commit -am 'WIP'
git diff develop -- data
```

No changes.

Pulled develop on my vm again, rerunning the smoke tests on develop branch.

I'm thinking perhaps my thornode dash branch has drifted behind too much and now
is out of alignment with the latest heimdall changes. If this smoking works then
I'd expect my branch to just work.

It failed. Ok. Trying again with the official image.

```
docker images
docker rmi -f 54a82d84fcc2 9e75f439b5a5 73412f277ebd
docker pull registry.gitlab.com/thorchain/thornode:mocknet
```

Obviously, dash will no longer work, but on my heimdall dash branch and with a
checked out version of develop transactions, I'd expect things to work just fine.

Ah thorchain startup is broken now. On `thornode` in my vm:

```
git checkout develop
git pull
cd build/docker
```

Restarted the cluster.  
So. Many. Bash. Errors. Wtf.  
I'm on the latest develop branch. I'm using the unmodified docker compose.  
I'm using the image referenced in that compose file.  
Let's just rebuild the thornode image and try again.  
Perhaps the one on registry.gitlab.com `thornode` official is just way behind.  
That's better.  

Failed to connect??  

> W[2022-05-24 04:31:14,536] Retrying (Retry(total=4, connect=4, read=6, redirect=None, status=None)) after connection broken by 'NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7ff5afc21960>: Failed to establish a new connection: [Errno 111] Connection refused')': /

Rebuilding heimdall as well...   
Argh. Lets reboot the vm...  
Check docker networks are all deleted.  

I'll wait for block 20.  
????  
Why. Why is it doing this??  
Why is the error so unhelpful?  

It says it can't connect using `urllib3.connection.HTTPConnection` to `/`, ok,
whats the domain/ip? What protocol are you trying to use?

Okay the stacktrace has `dash` in it. Gotcha. It's trying to connect to the
non-existent dash node. How do I comment that out for now?

Commented a bunch of dash related things out in `scripts/smoke.py`. I have a
good feeling about this. Cummon baby.

> 'Smoker' object has no attribute 'mock_dash'

Correct, I removed it. Don't worry about it.  
Clearly, I wasn't heavy handed enough with my commenting out.  
Now.  
It's a good time to work.  

Thank god. All green.

- [ ] TODO: Need to ensure the pipelines for `thornode`, `node-launcher` and
  `heimall` are all green/passing.


### 24.05.2022 Tuesday

Might only get a few hours done today. 

To start with I need to access the vm running on my home pc, as I'm working
remotely. I'll just use google desktop to access my pc, then install a zerotier
network within the vm, and ssh via the vpn.

Done, Took 5 minutes. God I love zerotier.

Attempts:
- `thornode:default` and `heimdall:add-dash` (dash commented out in  `smoke.py`) OK
- `thornode:add-dash` and `heimdall:add-dash` (dash commented out in  `smoke.py`) ?

It really does take a while to rebuild the `thornode` docker image.


### 06.07.2022 Wednesday

Coming back to this after the long break, with a fresh new laptop :) Time to
wrinse it. Now where on earth am I???

Firstly pulling `thornode` changes to `develop`.  
> Updating d223f726c..46a919f1d  
166 commits. What happened?  


```bash
gd d223f726c..46a919f1d -- bifrost/pkg/chainclients/bitcoincash
```

- delete block_meta
- delete block_meta_accessor
- delete block_meta_accessor_test
- delete block_meta_test

So I'm now using an M1 mac but all my homebrew installs have been copied over
from my old intel mac. I'm getting issues.

```
/usr/sbin/softwareupdate --install-rosetta --agree-to-license

```

Installed homebrew arm and latest go.  
I now have `/opt/homebrew` AND `/usr/local/Cellar/`  

> Warning: /opt/homebrew/bin is not in your PATH.
  Instructions on how to configure your shell for Homebrew
  can be found in the 'Next steps' section below.

Okay back on track. Have:

`go mod tidy`

> gitlab.com/thorchain/thornode/bifrost/pkg/chainclients/bitcoin imports
>   github.com/btcsuite/btcd/chaincfg/chainhash loaded from github.com/btcsuite/btcd@v0.22.0-beta,
>   but go 1.16 would fail to locate it:
>   ambiguous import: found package github.com/btcsuite/btcd/chaincfg/chainhash in multiple modules:
>   github.com/btcsuite/btcd v0.22.0-beta (/Users/adc/go/pkg/mod/github.com/btcsuite/btcd@v0.22.0-beta/chaincfg/chainhash)
>   github.com/btcsuite/btcd/chaincfg/chainhash v1.0.1 (/Users/adc/go/pkg/mod/github.com/btcsuite/btcd/chaincfg/chainhash@v1.0.1)
> 
> To proceed despite packages unresolved in go 1.16:
>   go mod tidy -e
> If reproducibility with go 1.16 is not needed:
>   go mod tidy -compat=1.17
> For other options, see:
>   https://golang.org/doc/modules/pruning

`go mod tidy -e`

> gitlab.com/thorchain/thornode/bifrost/pkg/chainclients/bitcoin imports
>   github.com/btcsuite/btcd/chaincfg/chainhash loaded from github.com/btcsuite/btcd@v0.22.0-beta,
>   but go 1.16 would fail to locate it:
>   ambiguous import: found package github.com/btcsuite/btcd/chaincfg/chainhash in multiple modules:
>   github.com/btcsuite/btcd v0.22.0-beta (/Users/adc/go/pkg/mod/github.com/btcsuite/btcd@v0.22.0-beta/chaincfg/chainhash)
>   github.com/btcsuite/btcd/chaincfg/chainhash v1.0.1 (/Users/adc/go/pkg/mod/github.com/btcsuite/btcd/chaincfg/chainhash@v1.0.1)

Argh.  

Just checked out the develop version and worked with that.  
Now I'm getting `Coin` is undefined in `common/coin.go`.  
Interesting.  
Invalidating the cache to see if that helps.  
Seems like the repo is in a state of disrepair at the moment...  
It was because the proto files were not comitted. D'oh.  

Okay how do I generate these proto files?  
Does `protocgen.sh` exist in the project repo?  

`make protob`  
> find: -printf: unknown primary or operator
> make: *** [protob] Error 1

Another script that doesn't work properly on mac :(  
Why can't this just be part of go generate?  
Replaced `find` with `gfind` (gnu find for mac) in `./scripts/protocgen.sh` and
all is well. But I had to check that script out again so note to me: try and 
remember that protobuf requires manual shenanigans.  


### 07.07.2022 Thursday

`go test -tags mocknet ./...`  
> go: no such tool "compile"

Huh?  
Oh I was using an old terminal tab with invalid `GOROOT` env var.  

> address_test.go:422:
>     c.Check(addr.GetNetwork(semver.MustParse("999.0.0"), DASHChain), Equals, MockNet)
> ... obtained common.ChainNetwork = 0x0
> ... expected common.ChainNetwork = 0x2

Dash testnet and mocknet are the same, switched test to `TestNet`.

All tests passing :)

Asked Aquila from Nine Realms to get Dash into the next milestone.

Back to the smoke tests...

Getting this when rebuilding the thornode docker image:
> [Warning] The requested image's platform (linux/amd64) does not match the
  detected host platform (linux/arm64/v8) and no specific platform was
  requested

This was the solution:  
`export DOCKER_DEFAULT_PLATFORM=linux/amd64`  

Haven't looked into these yet:
```
brew install gitlab-runner
brew services start gitlab-runner
gitlab-runner install
gitlab-runner start

gitlab-runner exec docker lint
gitlab-runner exec docker unit-tests
gitlab-runner exec docker smoke-test
```

Getting this when running the heimdall tests:  
> ModuleNotFoundError: No module named 'terra_proto.terra'

Probably just outdated right?  
`gco develop && ggpull`  
> rename chains/{terra.py => gaia.py

Good to know.  
Just going to try for a clean run using `develop`.

```
docker run \
  -it \
  --rm \
  --network thorchain_default \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  --entrypoint bash \
  registry.gitlab.com/thorchain/heimdall

docker run \
  -it \
  --rm \
  --network thorchain_default \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py \
      --thorchain http://thorchain-thornode-1:1317 \
      --binance http://thorchain-binance-1:26660 \
      --gaia http://thorchain-gaia-1:21317 \
      --bitcoin http://thorchain:password@thorchain-bitcoin-1:18443 \
      --bitcoin-cash http://thorchain:password@thorchain-bitcoin-cash-1:28443 \
      --litecoin http://thorchain:password@thorchain-litecoin-1:38443 \
      --dogecoin http://thorchain:password@thorchain-dogecoin-1:18332 \
      --ethereum http://thorchain-ethereum-1:8545 \
      --midgard http://thorchain-midgard-1:8080
```

http://thorchain-thornode-1:6030  
http://thorchain-thornode-1:6040  
http://thorchain-thornode-1:6060  

Heimdall is designed for all the ports to be accessible via localhost.  
Heimdall assumes bifrost and thornode are on the same node/container (no bifrost
specific config).  

What to do about that...  
docker network host is the answer, that's already setup apparently.  

There's a worrying lack of output from the smoke tests.  

Added that `loglevel` envvar but it's just showing http requests not the actual
smoke test output.

```
docker rmi registry.gitlab.com/thorchain/heimdall

docker pull registry.gitlab.com/thorchain/heimdall

docker build --platform linux/amd64 -t registry.gitlab.com/thorchain/heimdall .

docker run \
  -it \
  --rm \
  --name heimdall \
  --network host \
  --pull never \
  --platform linux/amd64 \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --fast-fail=True

docker run \
  -it \
  --rm \
  --name heimdall \
  --network host \
  --entrypoint bash \
  --pull never \
  --platform linux/amd64 \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall
```

Best thing to do is just watch the bifrost logs and refresh
`http://localhost:6040/p2pid` until bifrost is ready, then run the smoke tests.

The `run`s above worked, the first normally and the second from within a shell
inside the container.

```
I[2022-07-07 21:38:27,324] 71     USER-1 => VAULT      [SWAP:GAIA.ATOM:USER-1] 1.00000000 BNB.BNB
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event refund | {'code': '108'} {'reason': 'fail swap, invalid balance'} {'id': '5BB162F6905AD92D6347F0C62D56C1513CC7C486F9A052B36EB6A8A8CC9C6527'} {'chain': 'BNB'} {'from': 'tbnb157dxmw9jz5emuf0apj4d6p3ee42ck0uwksxfff'} {'to': 'tbnb1qf2l2hd4cp2dd2z45jtv2d9zxczansdk78hg56'} {'coin': '100000000 BNB.BNB'} {'memo': 'SWAP:GAIA.ATOM:cosmos1z63f3mzwv3g75az80xwmhrawdqcjpaek5l7xc0'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event refund | {'code': '108'} {'reason': "GAIA.ATOM pool doesn't exist"} {'id': '5BB162F6905AD92D6347F0C62D56C1513CC7C486F9A052B36EB6A8A8CC9C6527'} {'chain': 'BNB'} {'from': 'tbnb157dxmw9jz5emuf0apj4d6p3ee42ck0uwksxfff'} {'to': 'tbnb1qf2l2hd4cp2dd2z45jtv2d9zxczansdk78hg56'} {'coin': '100000000 BNB.BNB'} {'memo': 'SWAP:GAIA.ATOM:cosmos1z63f3mzwv3g75az80xwmhrawdqcjpaek5l7xc0'}
E[2022-07-07 21:38:46,613] Events mismatch

E[2022-07-07 21:38:46,614] Smoke tests failed
Traceback (most recent call last):
 File "/mnt/heimdall/scripts/smoke.py", line 136, in main
   smoker.run()
 File "/mnt/heimdall/scripts/smoke.py", line 630, in run
   self.check_events(events, sim_events)
 File "/mnt/heimdall/scripts/smoke.py", line 368, in check_events
   self.error("Events mismatch\n")
 File "/mnt/heimdall/scripts/smoke.py", line 235, in error
   raise Exception(err)
Exception: Events mismatch
```

So with my thorchain image and my heimdall image it got stuck at/after 71.

Trying with the offical ones on develop...  
Removed all the thornode/heimdall images.  

It fails spectacularly. Thornode container wont start up, thornode not found, no
such file or directory errors, madness.

DELETE EVERYTHING  
`docker system prune -a`  

```
docker run \
  -it \
  --rm \
  --name thornode \
  --platform linux/amd64 \
  -e NET=mocknet \
  -e CHAIN_ID=thorchain \
  registry.gitlab.com/thorchain/thornode:mocknet \
    thornode
```

> docker: Error response from daemon: failed to create shim task: OCI runtime
  create failed: runc create failed: unable to start container process:
  exec: "thornode": executable file not found in $PATH: unknown.

```
docker run \
  -it \
  --rm \
  --name thornode \
  --platform linux/amd64 \
  -e NET=mocknet \
  -e CHAIN_ID=thorchain \
  registry.gitlab.com/thorchain/thornode:mocknet \
    find / -name thornode
```

nothing. There's no `thornode` binary in that container. wtf.  

```
docker run \
  -it \
  --rm \
  --name thornode \
  --platform linux/amd64 \
  -e NET=mocknet \
  -e CHAIN_ID=thorchain \
  registry.gitlab.com/thorchain/thornode:latest \
    find / -name thornode
```

nothing. Is this some kind of practical joke?  

```
docker run \
  -it \
  --rm \
  --name thornode \
  --platform linux/amd64 \
  -e NET=mocknet \
  -e CHAIN_ID=thorchain \
  registry.gitlab.com/thorchain/thornode:latest \
    thornode
```

```
docker run \
  -it \
  --rm \
  --name thornode \
  --platform linux/amd64 \
  -e NET=mocknet \
  -e CHAIN_ID=thorchain \
  registry.gitlab.com/thorchain/thornode:00bbe31ad \
    thornode
```

Okay that one has a `thornode` binary. But not `latest` or `mocknet`??

`docker tag registry.gitlab.com/thorchain/thornode:00bbe31ad registry.gitlab.com/thorchain/thornode:mocknet`

In `node-launcher`, after some tweaking to allow me to run it locally:
`./ci/images/build.sh`

> cp: can't stat '/scripts/bifrost-config-template.json': No such file or directory

Now that would only happen if it were using my code. I deleted everything.  
At what point is it rebuilding thornode using my code?  

Ah yes, scripts are mounted. This is the problem with coming back to this after
a month, there's so much to remember. Switching to `develop` branch on `thornode`.

`bifrost` keeps crashing. Can't connect to `thorchain-bitcoin-1`.  

Bitcoin container is showing this error:
> bitcoind: error while loading shared libraries: libgcc_s.so.1: cannot open shared object file: No such file or directory

```
docker rmi registry.gitlab.com/thorchain/devops/node-launcher:bitcoin-daemon-22.0
docker pull registry.gitlab.com/thorchain/devops/node-launcher:bitcoin-daemon-22.0
```

Retry. Are my builds squiffy? If we get another connection error for another
node I'm going to assume yes.

Well assumed. Rebuilding with platform envvar set. That's going to be so easy to
forget.

Bonbonbonbons, we're there. So how do I not fuck up heimdall?

```
docker run \
  -it \
  --rm \
  --name heimdall \
  --network host \
  --platform linux/amd64 \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --fast-fail=True
```

It's pulling. That's good. 71 to beat ????  

Finally got all the way to 110. Okay. Great. Fantastic. Amazing.  
Now with my image configured with dash but without dash enabled...  
I'm keeping heimdall the same.  

`thornode`  
```
git checkout 982-add-dash-chain

cd build/docker

export DOCKER_DEFAULT_PLATFORM=linux/amd64

docker build \
  --progress plain \
  --build-arg TAG=mocknet \
  -t registry.gitlab.com/thorchain/thornode:mocknet \
  -f Dockerfile \
  ../..

export COMPOSE_PROFILES="mocknet,midgard"
export COMPOSE_PROJECT_NAME=thorchain

while true; do
  docker compose up --remove-orphans -d
  echo -n "Press enter to STOP thorchain..."
  read ignored
  docker compose down --volumes
  echo -n "Press enter to RESTART thorchain..."
  read ignored
done
```

Bifrost has connected to thornode and is generating the primes.  
Done, and I have a p2pid.  

Just a quick check to make sure it's definitely using my new thornode/bifrost
image:

```
docker exec thorchain-bifrost-1 ls -la /scripts/bifrost-config-template.json
```

Yep, that's where it should be. So far so good.  
Now... ???? heimdall...  

`heimdall`
```
export DOCKER_DEFAULT_PLATFORM=linux/amd64

docker run \
  -it \
  --rm \
  --name heimdall \
  --network host \
  --pull never \
  --platform linux/amd64 \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --fast-fail=True
```

Waiting for the standard 20s of docker/python startup...  
We're off!  
Can it reach 110???  

Same place. This is the crucial log from thorchain:

> fail to swap error="fail swap, invalid balance"
  msg="0B71F4F06888490CCA10E543CACDB4D86E6B4F3CE2EF09232693A159C988752B:
  tbnb157dxmw9jz5emuf0apj4d6p3ee42ck0uwksxfff ==>
  tbnb1gm5prz65qkrkhrvm567ctpwhfc32xu04p00szp
  (Memo: SWAP:GAIA.ATOM:cosmos1z63f3mzwv3g75az80xwmhrawdqcjpaek5l7xc0)
  100000000 BNB.BNB (gas: [37500 BNB.BNB])"

Can I find this address anywhere?  
`tbnb157dxmw9jz5emuf0apj4d6p3ee42ck0uwksxfff`  

It's in `aliases_bnb` in `aliases.py` within `heimdall` for `USER-1`.  
I have a feeling this has something to do with my genesis script being different
from the offical branch, perhaps not including an address or an updated amount.

It looks like we're expecting a refund but what's actually happening is we're
getting a "gaia.atom pool doesn't exist" error.


Okay tomorrow I'd like to see if the bifrost config for gaia looks ok.


### 08.07.2022 Friday

New stack.  

I have a plan. Going to compare the logs from this run with my thornode image
against the logs from the official one and see if all these thornode error logs
I'm seeing are valid or not.

Got to run to the airport to collect my baggage, they finally have it after 10
days of not having any clothes etc.

### 14.07.2022 Thursday

Didn't manage much on Friday as it was the beer festival. Envoy and DashDirect
stuff got in the way too.

Today is TC only.

- Updated develop and merged
- Rebuilt images

```bash
cd build/docker

export DOCKER_DEFAULT_PLATFORM=linux/amd64

docker build \
  --progress plain \
  --build-arg TAG=mocknet \
  -t registry.gitlab.com/thorchain/thornode:mocknet \
  -f Dockerfile \
  ../..

export COMPOSE_PROFILES="mocknet,midgard"
export COMPOSE_PROJECT_NAME=thorchain

while true; do
  docker compose up --remove-orphans -d
  echo -n "Press enter to STOP thorchain..."
  read ignored
  docker compose down --volumes
  echo -n "Press enter to RESTART thorchain..."
  read ignored
done
```

```bash
export DOCKER_DEFAULT_PLATFORM=linux/amd64

docker build --platform linux/amd64 -t registry.gitlab.com/thorchain/heimdall .

docker run \
  -it \
  --rm \
  --name heimdall \
  --network host \
  --pull never \
  --platform linux/amd64 \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --fast-fail=True
```

heimdall:  
> failed to send all outbound transactions 1
> smoke tests failed

thornode:  
> Failed to read request err="websocket: close 1006 (abnormal closure): unexpected EOF

I think it could be a freak accident.  
Need to run again...  

Okay captured a fresh fail on `71` with thorchain (add-dash) heimdall (develop).  
Now running with dev/dev so I have some logs to compare.  

> SWAP:GAIA.ATOM:cosmos1z63f3mzwv3g75az80xwmhrawdqcjpaek5l7xc0

Searching the above memo will take you to the right place in both thornode logs.

These errors don't exist on the develop branch:

> ERR app/x/thorchain/manager_gas_current.go:86 > network fee is invalid error="transaction size can't be zero or negative: 0" chain=GAIA

> ERR app/x/thorchain/handler_swap.go:38 > fail to handle MsgSwap error="fail swap, invalid balance"

> ERR app/x/thorchain/manager_swap_queue_current.go:162 > fail to swap error="fail swap, invalid balance" msg="36093190A1E0AA6FE2D81260C7F8599F04B1FFC87D00CDEA043D9FFD3D81D078: tbnb157dxmw9jz5emuf0apj

- `manager_gas_current`: identical
- `handler_swap`: identical
- `manager_swap_queue_current`: identical
- `./bifrost/pkg/chainclients/gaia/*`: identical
- Just compared my branch vs develop and there's nothing obvious that would make gaia different.
- Is the generated bifrost config the same in my version vs the official?

  
Instead of constantly having to rebuild I'm going to tag using the branch names
and latest commit as well.

```bash
docker build \
  --progress plain \
  --build-arg TAG=mocknet \
  -t registry.gitlab.com/thorchain/thornode:$(git branch --show-current)-$(git rev-parse --short HEAD) \
  -f Dockerfile \
  ../..

docker image ls

docker tag registry.gitlab.com/thorchain/thornode:982-add-dash-chain-9d461ce85 registry.gitlab.com/thorchain/thornode:mocknet

docker exec -it thorchain-bifrost-1 cat /etc/bifrost/config.json
```

Just realised the branch does need to match as well because we're mounting the
scripts. Argh, so much to remember.

Okay how does it go with the default scripts but MY image?  

Got to `87`. Interesting. Okay that was it. My bifrost scripts mess things up. I'll just
revert then as I clearly changed things I don't understand well enough.

With 10mins left on the clock, I found the issue. I think I'm going to quit
while I'm ahead here.

Damn right at the end there I got:

> failed to send all outbound transactions 2
> Smoke tests failed

I think this is more of a random error caused by too short timeouts rather than
anything serious. Will run again to check...


### 15.07.2022 Friday

- [x] Revert bifrost scripts...
- [x] Pull from develop

Right now I feel like I should start again completely with heimdall.  
Hmm.  
What's the fastest way to do this?  

I'm thinking:
- rebuild my thornode image
- merge heimdall dev -> dash
- remove any dash txs in the list
- see if that works (it really should at this point)
- rerun the generate / emulator thingy (this is the bit I'm unsure about)
  to CREATE the tests which will be run against the actual thornode.
  tbh I think that bit is going to be the hardest.
- run the damn thing...

Good plan lets do it.

I need python for heimdall. New macs don't come with python installed. I still
have the homebrew version which was upgraded for the m1. Current sentiment seems
that Anaconda is the way to go.

```
brew install --cask anaconda
```

Managed to find `anaconda3` in the root of the homebrew directory. Looks like
that's where it went.

If I want to use `conda`:
```
export PATH="/opt/homebrew/anaconda3/bin:$PATH"
```

Selected the conda binary in the jetbrains plugin and that seemed to do the
trick. It whirred and did some scary looking stuff and then presented me with
a list of packages. Not the ones I need though in `requirements.txt`.

I complained it listened, it started fetching them.  
Bet it wont find `python-dashtx`.  

```
Collecting package metadata (current_repodata.json): ...working... done
Solving environment: ...working... failed with initial frozen solve. Retrying with flexible solve.
Collecting package metadata (repodata.json): ...working... done
Solving environment: ...working... failed with initial frozen solve. Retrying with flexible solve.


PackagesNotFoundError: The following packages are not available from current channels:

 - bitcoincash==0.1.5

Current channels:

 - https://repo.anaconda.com/pkgs/main/osx-arm64
 - https://repo.anaconda.com/pkgs/main/noarch
 - https://repo.anaconda.com/pkgs/r/osx-arm64
 - https://repo.anaconda.com/pkgs/r/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

   https://anaconda.org

and use the search bar at the top of the page.
```

Not quite what I was expecting but still bad.  
Hmm.  

Just unchecked that one and it failed at the next one on the list. Looks like
it just reports the first error and all of them cannot be found.

`python-litecointx` seems to be a pypi package.

You can use pypy "puppy" as the python interpreter in a conda environment,
apparently.

```
conda config --set channel_priority strict
conda create -n pypy pypy
conda activate pypy
```

> PackagesNotFoundError

```
cd /opt/homebrew/anaconda3/envs/heimdall
```

```
/opt/homebrew/anaconda3/envs/heimdall/bin/pip install pipreqs
/opt/homebrew/anaconda3/envs/heimdall/bin/pipreqs
```

Nope. Well, I have enough syntax highlighting and code sense easily to get by.  
Resolved git conflicts.  

Now I have a thorchain image and mocknet cluster docker compose file setup to 
run dash, and a heimdall with the capabilities of understanding dash but without
actually having dash in the tests.

It might be worth a run here, but I'm going to skip ahead to save 30mins and
fallback to here if things jenga.

```
export DOCKER_DEFAULT_PLATFORM=linux/amd64

docker run \
  -it \
  --rm \
  --name heimdall \
  --network host \
  --pull never \
  --platform linux/amd64 \
  -v $(pwd):/mnt/heimdall \
  -w /mnt/heimdall \
  registry.gitlab.com/thorchain/heimdall \
    python scripts/smoke.py --fast-fail=True
```

It's my understanding that we have to manually update `smoke_test_transactions`.  
The events and balances can be updated during the `make test`.  
Then we run all that against `make smoke` with a real mocknet cluster.

```
make test
EXPORT=data/smoke_test_balances.json EXPORT_EVENTS=data/smoke_test_events.json make test
make smoke
```

```
I[2022-07-15 19:00:42,395] 10     MASTER => USER-1     [SEED] 200.00000000 DASH.DASH
I[2022-07-15 19:00:42,580] 11     MASTER => PROVIDER-1 [SEED] 2,000.00000000 DASH.DASH
E[2022-07-15 19:00:42,668] 'txid'
E[2022-07-15 19:00:42,669] Smoke tests failed
Traceback (most recent call last):
 File "/app/scripts/smoke.py", line 143, in main
   smoker.run()
 File "/app/scripts/smoke.py", line 639, in run
   self.broadcast_chain(txn)
 File "/app/scripts/smoke.py", line 403, in broadcast_chain
   return self.mock_dash.transfer(txn)
 File "/app/chains/dash.py", line 222, in transfer
   tx_in = [{"txid": unspent["txid"], "vout": unspent["vout"]}]
KeyError: 'txid'
make: *** [smoke] Error 1
```


`docker exec thorchain-dash-1 dash-cli listunspent`

All are going to `yZnyJAdouDu3gmAuhG3dTc66hroS4AXxnL` except one which is going
to `yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5` for 200. That looks like the:
master -> user1 above  
So master -> provoder1 did actuall fail?  

Ahh I think I found it. Dash utxos are 500 dash max. So we can't send 2K with a
single utxo.  
400, sure.  

Brought all dash transaction sizes down an order of magnitude.  
Retrying...  

```
I[2022-07-15 19:35:16,728] 77     USER-1 => VAULT      [SWAP:DASH.DASH:USER-1] 1.00000000 BNB.BNB
E[2022-07-15 19:35:38,266] out coins not matching 2508985011 DASH.DASH != 2510623011 DASH.DASH
```

```
2508985011 expected by sim
2510623011 actual, in logs, part of txout array

25.08985011
25.10623011
  .01638000
```

So we're actually sending a bit more dash to the customer than "expected". This
could mean we're not charging enough in thornode or calculating too much in the
simulator. I'm tempted to go with the latter.

Coming from `sim_catch_up`.  
There's a `thorchain_client` and `thorchain_state`, think state is the sim.  
Leads into `sim_trigger_tx` which I think is called first.  
This leads into `broadcast_simulator` which has a line `return self.dash.transfer(txn)`.  
It also has a comment "Broadcast tx to simulator state chain" which doesn't
fit because the `self.dash` is an instance of `Dash()` not `MockDash()` and as
far as I can tell goes on to call `transfer(self, txn)` which actually sends
that on to the node. How is that a simulator? That's real as real can be.  
I'm lost.  

Probably just set a fee wrong somewhere. But where??

From the readme:
> The smoke tests compare a mocknet against a simulator implemented in python.

Alright it's a pinch of questionable naming with a splash of my infamiliarity
with python at play. So `MockDash` actually makes calls to the dash node so in
my mind that is a real client, not a mock, `Dash` on the other hand is a mock
in so far as it doesn't make any real connections, it implements `GenericChain`
which has a `transfer(self, txn)` method which just moves funds from account
A to account B in memory. Right. Now that's cleared up...

We have:
`rune_fee = 2000000`

I'm actually not sure what's going on with the python sim. Going to start by
stripping it down to just dash and bnb.

```
I[2022-07-16 02:04:28,084]  0     MASTER => CONTRIB    [SEED] 10.00000000 BNB.BNB
I[2022-07-16 02:04:28,112]  1     MASTER => USER-1     [SEED] 20.00000000 DASH.DASH
I[2022-07-16 02:04:28,234]  2     MASTER => PROVIDER-1 [SEED] 200.00000000 DASH.DASH
I[2022-07-16 02:04:28,327]  3 PROVIDER-1 => VAULT      [SWAP:BNB.BNB:PROVIDER-1-SYNTH] 500.00000000 THOR.RUNE
I[2022-07-16 02:04:32,474] [-] 499.98000000 THOR.RUNE | Fee 0.02000000 THOR.RUNE | Gas 0.02000000 THOR.RUNE
I[2022-07-16 02:04:32,475]  4 PROVIDER-1 => VAULT      [ADD:BNB.BNB:PROVIDER-1] 1,000.00000000 THOR.RUNE
I[2022-07-16 02:04:37,424]  5 PROVIDER-1 => VAULT      [ADD:BNB.BNB:PROVIDER-1] 2.50000000 BNB.BNB
E[2022-07-16 02:04:42,291] 'NoneType' object is not iterable
E[2022-07-16 02:04:42,292] Smoke tests failed
Traceback (most recent call last):
 File "/app/scripts/smoke.py", line 143, in main
   smoker.run()
 File "/app/scripts/smoke.py", line 654, in run
   self.check_binance()
 File "/app/scripts/smoke.py", line 293, in check_binance
   for bal in macct["balances"]:
TypeError: 'NoneType' object is not iterable
make: *** [smoke] Error 1
```

Oh python. Why doth thou ail me?

Took out all txs except BNB + DASH. Getting:
> 'NoneType' object is not iterable

On:
> PROVIDER-1 => VAULT      [ADD:BNB.BNB:PROVIDER-1] 2.50000000 BNB.BNB

> I[2022-07-16 04:08:50,140] 31     USER-1 => VAULT      [SWAP:DASH.DASH:USER-1] 1.00000000 BNB.BNB
> E[2022-07-16 04:09:03,747] out coins not matching 556920153 DASH.DASH != 558558153 DASH.DASH

556920153
558558153

5.58558153 - 5.56920153
0.01638
same difference out :) clues

### 21.07.2022 Thursday

So back to working out why there is a tc, smoke mismatch.

In the smoke test, the run fees are all calculated for all chains like this:
```
dash_amount = pool.get_rune_in_asset(int(cls.rune_fee / 2))
```

And the rune fee is always `rune_fee = 2000000`.  
Which can be simplified to `pool.get_rune_in_asset(1000000)`.  
1mill get rune in asset.  
What does `get_rune_in_asset` mean/do?  
Think this is a bit misleading, you're not getting rune at all, you're getting
the asset value for the given rune value, so it could be written like:  
"get asset equivalent for rune value"  
So it's asking, what's the dash equivalent for 1 million rune in the pool?  
Which means the gas price is fixed against rune?

The values have changed a bit:

```
I[2022-07-22 00:27:39,052] 29 USER-1 => VAULT [SWAP:DASH.DASH:USER-1] 1.00000000 BNB.BNB
E[2022-07-22 00:28:02,640] out coins not matching 556776998 DASH.DASH != 558414998 DASH.DASH
```

Probably because of my transactions.json having different txs.

Just saved the output of the above in `run5` md5 of transactions json is: 
> MD5 (./data/smoke_test_transactions.json) = 7a4ad5d5abdfb669ecb69b416c72c27d

- Any txs with `-SYNTH` all go to the synth addresses?

Here's my attempt to work through heimdall txs here:

- 1: `MASTER => USER-1     [SEED] 26.00000000 BNB.BNB, 1,500.00000000 BNB.LOK-3C0`  
  Seed USER1 26 BNB and 1500 LOK  

- 2: `MASTER => PROVIDER-1 [SEED] 10.00000000 BNB.BNB, 800.00000000 BNB.LOK-3C0`  
  Seed PROVIDER1 10 BNB and 800 LOK  

- 3: `MASTER => PROVIDER-2 [SEED] 2.00000000 BNB.BNB, 100.00000000 BNB.LOK-3C0`  
  Seed PROVIDER2 2 BNB and 100 LOK  

- 4: `MASTER => USER-1     [SEED] 20.00000000 DASH.DASH`  
  Seed USER1 20 DASH  

- 5: `MASTER => PROVIDER-1 [SEED] 200.00000000 DASH.DASH`  
  Seed PROVIDER1 200 DASH  

- 6: `PROVIDER-1 => VAULT      [SWAP:BNB.BNB:PROVIDER-1-SYNTH] 500.00000000 THOR.RUNE`  
  PROVIDER1 trying to SWAP 500 RUNE for BNB  
  At this point provider1 doesn't seem to actually have any rune  
  No change, that makes sense  
  Must be an invalid tx which is immediately prevented without incurring fees?  
  We're seeing `[-]` which I'm guessing means the transaction didn't happen.  

- 7: `PROVIDER-1 => VAULT      [ADD:BNB.BNB:PROVIDER-1] 1,000.00000000 THOR.RUNE`  
  PROVIDER1 trying to add 1K RUNE to the BNB pool.  
  `POOL.BNB.BNB` was created but with 0 values, probably because provider1 still  
  doesn't have any rune?  
  Output
```json
{
    "CONTRIB":
    {
        "BNB.BNB": 1000000000
    },
    "OUT": 0,
    "POOL.BNB.BNB":
    {
        "BNB.BNB": 0,
        "THOR.RUNE": 0
    },
    "PROVIDER-1":
    {
        "BNB.BNB": 1000000000,
        "BNB.LOK-3C0": 80000000000
    },
    "PROVIDER-2":
    {
        "BNB.BNB": 200000000,
        "BNB.LOK-3C0": 10000000000
    },
    "TX": 7,
    "USER-1":
    {
        "BNB.BNB": 2600000000,
        "BNB.LOK-3C0": 150000000000
    },
    "VAULT":
    {}
}
```

- 8: `PROVIDER-1 => VAULT      [ADD:BNB.BNB:PROVIDER-1] 2.50000000 BNB.BNB`  
  PROVIDER1 trying to add 2.5 BNB to BNB pool  
  Looks like it works  
  Gas is apparently 0.00037500 BNB.BNB  
  AKA `0.00015` of the value  
  Now the vault does actually have BNB  
  Provider 1 has 749962500 BNB which is:  
  1000000000 - 250000000 - 37500 = 749962500  
  The output is:  
```json
{
    "CONTRIB":
    {
        "BNB.BNB": 1000000000
    },
    "OUT": 0,
    "POOL.BNB.BNB":
    {
        "BNB.BNB": 250000000,
        "THOR.RUNE": 100000000000
    },
    "PROVIDER-1":
    {
        "BNB.BNB": 749962500,
        "BNB.LOK-3C0": 80000000000
    },
    "PROVIDER-2":
    {
        "BNB.BNB": 200000000,
        "BNB.LOK-3C0": 10000000000
    },
    "TX": 8,
    "USER-1":
    {
        "BNB.BNB": 2600000000,
        "BNB.LOK-3C0": 150000000000
    },
    "VAULT":
    {
        "BNB.BNB": 250000000
    }
}
```
  So the vault AND the pool both have BNB allocated, it's accounted for in two
  places. It still makes sense, apart from I have no idea where the 1K rune came
  from. Setup scripts?

  Okay going to combine the aliases in heimdall and the thornode setup script
  to see if any of these match up and what address gets what:

```js
  let aliases = {
    "MASTER": "tthor1nrsk6f4kalwwrqqyrfmxzl96hyjhe96t4gmvp2",
    "CONTRIB": "tthor1m8prd4pvqe5p3cu7tu82pn50a5f9xzxzetc35t",
    "USER-1": "tthor1z63f3mzwv3g75az80xwmhrawdqcjpaekk0kd54",
    "PROVIDER-1": "tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257",
    "PROVIDER-2": "tthor1xwusttz86hqfuk5z7amcgqsg7vp6g8zhsp5lu2",
    "VAULT": "tthor1g98cy3n9mmjrpn0sxmn63lztelera37nrytwp2",
    "SYNTH": "tthor1v8ppstuf6e3x0r4glqc68d5jqcs2tf38ulmsrp",
    "RESERVE": "tthor1dheycdevq39qlkxs2a6wuuzyn4aqxhve3hhmlw",
    "BOND": "tthor17gw75axcnr8747pkanye45pnrwk7p9c3uhzgff",
  }

  let balances = [
    {
      "address": "tthor1wt88pankukq3qhj9ndqpdes2ukuuu4yq22a5lx",
      "coins": [{"denom": "rune", "amount": "1000000000"}]
    },
    {
      "address": "tthor1z63f3mzwv3g75az80xwmhrawdqcjpaekk0kd54",
      "coins": [{"denom": "rune", "amount": "5000000000000"}]
    },
    {
      "address": "tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257",
      "coins": [{"denom": "rune", "amount": "25000000000100"}]
    },
    {
      "address": "tthor18f55frcvknxvcpx2vvpfedvw4l8eutuhku0uj6",
      "coins": [{"denom": "rune", "amount": "25000000000100"}]
    },
    {
      "address": "tthor1xwusttz86hqfuk5z7amcgqsg7vp6g8zhsp5lu2",
      "coins": [{"denom": "rune", "amount": "5090000000000"}]
    },
    {
      "address": "tthor1uuds8pd92qnnq0udw0rpg0szpgcslc9p8lluej",
      "coins": [{"denom": "rune", "amount": "200000000000000"}]
    },
    {
      "address": "tthor1zf3gsk7edzwl9syyefvfhle37cjtql35h6k85m",
      "coins": [{"denom": "rune", "amount": "200000000000000"}]
    },
    {
      "address": "tthor13wrmhnh2qe98rjse30pl7u6jxszjjwl4f6yycr",
      "coins": [{"denom": "rune", "amount": "200000000000000"}]
    },
    {
      "address": "tthor1qk8c8sfrmfm0tkncs0zxeutc8v5mx3pjj07k4u",
      "coins": [{"denom": "rune", "amount": "200000000000000"}]
    }
  ]

  balances.forEach(b => {
    const alias = Object.entries(aliases).find(([k, v]) => v === b.address)
    if (alias) {
      console.log(alias[0], b.address, b.coins[0].amount / 1e8, 'RUNE')
    }
  })
```

```
USER-1 tthor1z63f3mzwv3g75az80xwmhrawdqcjpaekk0kd54 50000 RUNE
PROVIDER-1 tthor1wz78qmrkplrdhy37tw0tnvn0tkm5pqd6zdp257 250000.000001 RUNE
PROVIDER-2 tthor1xwusttz86hqfuk5z7amcgqsg7vp6g8zhsp5lu2 50900 RUNE
```

  Okay that solves that mystery, moving on...

- 9: `PROVIDER-1 => VAULT      [ADD:DASH.DASH:PROVIDER-1] 10.00000000 THOR.RUNE`  
  PROVIDER1 trying to ADD 10 RUNE to DASH pool  
  Should work, we see the `POOL.DASH.DASH` with nothing in it. We'd expect the  
  vault to hold the necessary rune but I think rune is just being omitted.  
  
- 10: `PROVIDER-1 => VAULT      [ADD:DASH.DASH:PROVIDER-1] 150.00000000 DASH.DASH`  
  PROVIDER1 trying to ADD 150 DASH to dash pool  
  I'm looking at the outputs above and seeing that the Provider1 and User1  
  should be showing 200 DASH and 20 DASH respectively, they're not.  
  
  Going to rebuild heimdall on this branch to make sure I have my changes
  included. Also double check the makefile...

  ```bash
  docker run \
    -it \
    --rm \
    --name heimdall \
    --network host \
    --pull never \
    --platform linux/amd64 \
    -v $(pwd):/app \
    -e RUNE=THOR.RUNE \
    -e LOGLEVEL=INFO \
    -e PYTHONPATH=/app \
    -w /app \
    registry.gitlab.com/thorchain/heimdall \
      python scripts/smoke.py --fast-fail=True
  ```

  If this still doesn't seem to SEED, I'll try with DOGE too and see if that
  seeds or if it's nothing to worry about.

  Okay, DOGE doesn't get added to the vault either.

  Next step: Add a shit tonne of logging to heimdall until I understand what's
  going on better...

  ```python
  logging.info(f"@DASH CALCULATE GAS dash_amount: {dash_amount}")
  ```

  Interestingly, there's this: `default_gas = 100000` which is one 0/d.p out
  from the stuff I found before.

  So at this point we have:
  `'POOL.DASH.DASH': {'DASH.DASH': 15000000000, 'THOR.RUNE': 1000000000},`

  

The second number is the actual number sent on the dash network. i.e.
```json
{
  "involvesWatchonly": true,
  "address": "yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5",
  "category": "receive",
  "amount": 5.58414998,
  "label": "",
  "vout": 0,
  "confirmations": 306,
  "instantlock": false,
  "instantlock_internal": false,
  "chainlock": false,
  "blockhash": "731b9cc7a7263056631ca08d7e2f0ef5701d5100fdad79f6926e77724a35a248",
  "blockindex": 3,
  "blocktime": 1658462283,
  "txid": "dceea33a8a4fb48e442bfe67d9a7503edfc1648e653785b9c564a385d8873dda",
  "walletconflicts": [
  ],
  "time": 1658462283,
  "timereceived": 1658462283
},
```

So the first number is mis-calculated.  
Where is 556776998 coming from?  

Am I looking at `self.thorchain_state.handle`?  
Or `self.broadcast_simulator(out)`?  

Outbound in hex:  
`01000000010eb21a3234c3a8250dc0309f6bf3119ffa302d27fb7fb8ddb29541778fd7b254000000006a4730440220379a3c5df696893ef4095b242247220829ceea85e4a903c9fdea67f1477d2a69022075eceb368656b622fd7e7314ade908d4d29ade2fdf74d7398b2f54a1eeb598730121020569e5e356ecf4fba59eb70d511729ec0b724d7166da3eae824660158887d3d3ffffffff0396bc4821000000001976a9140026dcfac0cd2092ea5a124f2089c3ad5b7aa2cd88ac4c2ac75c030000001976a91444d0c5c98fb4cc549d86dd0da3003547f3dc98fa88ac0000000000000000466a444f55543a3236464231363036304645374337323338383742323044304337464333333936463235324345313541334445453639424541443832463034454444393432394500000000`


--------------------------------------------------


Here's a command to keep trying the p2pid url until it works and then make a
sound:

```bash
timeout 300 bash -c 'while [[ "$(curl --insecure -s -o /dev/null -w ''%{http_code}'' http://localhost:6040/p2pid)" != "200" ]]; do sleep 5; done' && afplay /System/Library/Sounds/Funk.aiff
```

### 22.07.2022 Friday

heimdall gave me some hints last night a bit after I'd finished, so time to try
them out now.

1. I'm using doge code in heimdall at `scan_blocks` which doesn't use
  `getblockstats` like the others do. Will try re-working from litecoin.
2. I may have a bad value for `self.dash_estimate_size = 261`. He said I need
  to set that to the size of a standard bifrost out tx with 1 input and 3 outputs.
  I believe that came to 304 when I tried. Need to confirm.

```
dash-cli listtransactions "*" 99999999
dash-cli getrawtransaction 722602f4b5c8aeb6d8361419e025f95d5c62800be70bfc086cf0421b64609e2d
0100000001effe324c0f9c173b9f8738a8a9d6264b0038a5989ba350863f3db18723999fb3000000006b483045022100d7572d7ace078acd1e503b48e2cad85c6e9599e91aac27d5959db459ce42fb050220402685105b197ac95db4e426ba891ac42f64f61553a9a8ccdbf201ff4acf70ef012103c1d7eb24859f30af1f9c0140603eff181028243320ce8a8de7af23d0ee1a19a5ffffffff03bab64821000000001976a9140026dcfac0cd2092ea5a124f2089c3ad5b7aa2cd88ac3a2dc75c030000001976a9148aea9e186c33393d516e3e8fa7bfd15cc9b00b2988ac0000000000000000466a444f55543a3444343631303244463244384635383836454232443641363444444339323441433839353934383635414332343844464136423235383038303632384536413000000000
305 bytes
```

```
LOGLEVEL=INFO EXPORT=data/smoke_test_balances.json EXPORT_EVENTS=data/smoke_test_events.json make test
```

`58413498`

```
{
  "involvesWatchonly": true,
  "address": "yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5",
  "category": "receive",
  "amount": 5.58413498,
  "label": "",
  "vout": 0,
  "confirmations": 77,
  "instantlock": false,
  "instantlock_internal": false,
  "chainlock": false,
  "blockhash": "3b726ba83b5f76f277a36f0c7ad58990e899a57c257e63528bb15e8355ba5d17",
  "blockindex": 1,
  "blocktime": 1658516822,
  "txid": "9af927e6c039de662213ff9fcc314b978be6536843c35324d795ca8db640c2a1",
  "walletconflicts": [
  ],
  "time": 1658516821,
  "timereceived": 1658516821
},

010000000119f50976fd8aa16f9acf567574efef655892d65e80df00615858ef9240d717a6000000006a47304402207168b36ebe812fe0b65a73a2121f076e185628f0d373248547c83f20238c5bff0220069b549f429d0cd6e06cb5f80f3db65828871bf62b07c7e97ac2e8c195594015012102e5fa6eca615183bb2727e20cae17f2012a2bed384b4eb5dbbf76a6f56f784f59ffffffff03bab64821000000001976a9140026dcfac0cd2092ea5a124f2089c3ad5b7aa2cd88ac3a2dc75c030000001976a914b31546607a1524cba40cf08dd97861c9cac0344988ac0000000000000000466a444f55543a3844463445314234423839383045453539323441424646453838363836373045344137354433303534364337374445354537384237383931303133454234344400000000

{
  "txid": "9af927e6c039de662213ff9fcc314b978be6536843c35324d795ca8db640c2a1",
  "version": 1,
  "type": 0,
  "size": 304,
  "locktime": 0,
  "vin": [
    {
      "txid": "a617d74092ef58586100df805ed6925865efef747556cf9a6fa18afd7609f519",
      "vout": 0,
      "scriptSig": {
        "asm": "304402207168b36ebe812fe0b65a73a2121f076e185628f0d373248547c83f20238c5bff0220069b549f429d0cd6e06cb5f80f3db65828871bf62b07c7e97ac2e8c195594015[ALL] 02e5fa6eca615183bb2727e20cae17f2012a2bed384b4eb5dbbf76a6f56f784f59",
        "hex": "47304402207168b36ebe812fe0b65a73a2121f076e185628f0d373248547c83f20238c5bff0220069b549f429d0cd6e06cb5f80f3db65828871bf62b07c7e97ac2e8c195594015012102e5fa6eca615183bb2727e20cae17f2012a2bed384b4eb5dbbf76a6f56f784f59"
      },
      "value": 150.00000000,
      "valueSat": 15000000000,
      "address": "yceMHkJJ1V3uwLRfA5mTDgbib8GYQwWWLu",
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 5.58413498,
      "valueSat": 558413498,
      "n": 0,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 0026dcfac0cd2092ea5a124f2089c3ad5b7aa2cd OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a9140026dcfac0cd2092ea5a124f2089c3ad5b7aa2cd88ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5"
        ]
      }
    },
    {
      "value": 144.41459002,
      "valueSat": 14441459002,
      "n": 1,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 b31546607a1524cba40cf08dd97861c9cac03449 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a914b31546607a1524cba40cf08dd97861c9cac0344988ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "yceMHkJJ1V3uwLRfA5mTDgbib8GYQwWWLu"
        ]
      }
    },
    {
      "value": 0.00000000,
      "valueSat": 0,
      "n": 2,
      "scriptPubKey": {
        "asm": "OP_RETURN 4f55543a38444634453142344238393830454535393234414246464538383638363730453441373544333035343643373744453545373842373839313031334542343444",
        "hex": "6a444f55543a38444634453142344238393830454535393234414246464538383638363730453441373544333035343643373744453545373842373839313031334542343444",
        "type": "nulldata"
      }
    }
  ],
  "hex": "010000000119f50976fd8aa16f9acf567574efef655892d65e80df00615858ef9240d717a6000000006a47304402207168b36ebe812fe0b65a73a2121f076e185628f0d373248547c83f20238c5bff0220069b549f429d0cd6e06cb5f80f3db65828871bf62b07c7e97ac2e8c195594015012102e5fa6eca615183bb2727e20cae17f2012a2bed384b4eb5dbbf76a6f56f784f59ffffffff03bab64821000000001976a9140026dcfac0cd2092ea5a124f2089c3ad5b7aa2cd88ac3a2dc75c030000001976a914b31546607a1524cba40cf08dd97861c9cac0344988ac0000000000000000466a444f55543a3844463445314234423839383045453539323441424646453838363836373045344137354433303534364337374445354537384237383931303133454234344400000000",
  "blockhash": "3b726ba83b5f76f277a36f0c7ad58990e899a57c257e63528bb15e8355ba5d17",
  "height": 367,
  "confirmations": 112,
  "time": 1658516822,
  "blocktime": 1658516822,
  "instantlock": false,
  "instantlock_internal": false,
  "chainlock": false
}
```

Just remembered this too: `self.dash_estimate_size = 304 # TODO: CONFIRM`

out coins not matching 557935556 DASH.DASH != 558413498 DASH.DASH

There are multiple estimated sizes for dash.  I need to bruteforce which one is
actually making a difference.

Made 3 bookmarks. Here we gooooo.

The fact that an estimate needs to be exact for the test to pass is absurd, but
so is the complexity of life, who am I to take exception.  

bookmark 1, init, 304  
bookmark 2, handle withdraw1, 304  
bookmark 3, handle withdraw2, 188  

out coins not matching 558359798 DASH.DASH != 558413498 DASH.DASH

-----

bookmark 1, init, 330  
bookmark 2, handle withdraw1, 304  
bookmark 3, handle withdraw2, 188  

out coins not matching 557934833 DASH.DASH != 558414998 DASH.DASH

----

bookmark 1, init, 330  
bookmark 2, handle withdraw1, 304  
bookmark 3, handle withdraw2, 188  

out coins not matching 557935556 DASH.DASH != 558413498 DASH.DASH

----

bookmark 1, init, 330  
bookmark 2, handle withdraw1, 304  
bookmark 3, handle withdraw2, 188  

out coins not matching 557935556 DASH.DASH != 558413498 DASH.DASH

```
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event outbound | {'in_tx_id': '5F91B779874ED2B19D86CC9E3BD0BD472915ED99A55CFE5BD24581180A5CEEB4'} {'id': 'F874948976F0B02184BFBD32300D6488C246711460AD1C230E7AAC5C85E7337C'} {'chain': 'DASH'} {'from': 'yVSUM22EpJCV85rUrcbSiwvfLnppNaU25R'} {'to': 'yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5'} {'coin': '558413498 DASH.DASH'} {'memo': 'OUT:5F91B779874ED2B19D86CC9E3BD0BD472915ED99A55CFE5BD24581180A5CEEB4'}
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event gas | {'asset': 'DASH.DASH'} {'asset_amt': '127500'} {'rune_amt': '219700'} {'transaction_count': '1'}
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event fee | {'tx_id': '5F91B779874ED2B19D86CC9E3BD0BD472915ED99A55CFE5BD24581180A5CEEB4'} {'coins': '255000 DASH.DASH'} {'pool_deduct': '455723'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event gas | {'asset': 'DASH.DASH'} {'asset_amt': '366471'} {'rune_amt': '631436'} {'transaction_count': '1'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event fee | {'tx_id': '5F91B779874ED2B19D86CC9E3BD0BD472915ED99A55CFE5BD24581180A5CEEB4'} {'coins': '732942 DASH.DASH'} {'pool_deduct': '1309832'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event gas | {'asset': 'BNB.BNB'} {'asset_amt': '37500'} {'rune_amt': '14390497'} {'transaction_count': '1'}
```

----

bookmark 1, init, 330  
bookmark 2, handle withdraw1, 304  
bookmark 3, handle withdraw2, 188  

out coins not matching 557933063 DASH.DASH != 558414998 DASH.DASH

```
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event fee | {'tx_id': 'B0610EAEBA1A037129C1724E30E3FEB1F9EEE778C6BB1F7ED96E899A4B0E25A0'} {'coins': '253500 DASH.DASH'} {'pool_deduct': '453042'}
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event outbound | {'in_tx_id': 'B0610EAEBA1A037129C1724E30E3FEB1F9EEE778C6BB1F7ED96E899A4B0E25A0'} {'id': 'CB64C94EDA5B96421815DE13EC942E012CA37EE0AE84AF7D87E00888BA342D73'} {'chain': 'DASH'} {'from': 'yiX98sVhJHgXWKKMqZWSom12bwQbGCZ2NL'} {'to': 'yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5'} {'coin': '558414998 DASH.DASH'} {'memo': 'OUT:B0610EAEBA1A037129C1724E30E3FEB1F9EEE778C6BB1F7ED96E899A4B0E25A0'}
>>>>>>>>>>>>>>> MISSING SIM EVENT
Event gas | {'asset': 'DASH.DASH'} {'asset_amt': '126750'} {'rune_amt': '218407'} {'transaction_count': '1'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event gas | {'asset': 'DASH.DASH'} {'asset_amt': '367717'} {'rune_amt': '633583'} {'transaction_count': '1'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event gas | {'asset': 'BNB.BNB'} {'asset_amt': '37500'} {'rune_amt': '14390497'} {'transaction_count': '1'}
<<<<<<<<<<<<<<< EXTRA SIM EVENT
Event fee | {'tx_id': 'B0610EAEBA1A037129C1724E30E3FEB1F9EEE778C6BB1F7ED96E899A4B0E25A0'} {'coins': '735435 DASH.DASH'} {'pool_deduct': '1314287'}

```

scan_blocks avg_tx_size: 240  
scan_blocks avg_tx_size: 295  
scan_blocks avg_tx_size: 304  

It keeps changing without me doing anything. And when I say it, I mean both 
coin amounts in the error. The average transaction size changes too, along with
the difference between the expected and actual result.

I've been trying to work it out by reading the python code but have ended up
following so many leads into so many classes, I'm not the best at python but
even still there's a lot to unpack here. I feel like the best way forward is for
me to break down every single goddamn line of code relevant to my broken test
and understand it completely. I'll start by getting a feel of it, then try to
make some noticable precision changes, then hopefully that will be the point
when I can start trying to fix this.

Diving deep into `handle_swap` in `thorchain.py`.

On another note: there's nothing in `python-dash` regarding fees.

```
I[2022-07-23 01:53:58,984] @### sim_trigger_tx tbnb157dxmw9jz5emuf0apj4d6p3ee42ck0uwksxfff => tbnb1e0s8ufpf96frkcyrg7whsv736ugqqgaf0dzvrd [SWAP:DASH.DASH:yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5] 1.00000000 BNB.BNB | Gas 0.00037500 BNB.BNB | ID 8CCFC672EA524CC25825E4C1A522176C748963B855782FCC9F3C78DDAD74BFE1
I[2022-07-23 01:53:58,985] @### handle_swap
I[2022-07-23 01:53:58,985] @### tx tbnb157dxmw9jz5emuf0apj4d6p3ee42ck0uwksxfff => tbnb1e0s8ufpf96frkcyrg7whsv736ugqqgaf0dzvrd [SWAP:DASH.DASH:yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5] 1.00000000 BNB.BNB | Gas 0.00037500 BNB.BNB | ID 8CCFC672EA524CC25825E4C1A522176C748963B855782FCC9F3C78DDAD74BFE1
I[2022-07-23 01:53:58,986] @### tx <class 'utils.common.Transaction'>
I[2022-07-23 01:53:58,986] @### tx.memo SWAP:DASH.DASH:yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5
I[2022-07-23 01:53:58,986] @### target_trade 0
I[2022-07-23 01:53:58,987] @### asset DASH.DASH
I[2022-07-23 01:53:58,987] @### source BNB.BNB
I[2022-07-23 01:53:58,987] @### target DASH.DASH
I[2022-07-23 01:53:58,988] @### target.get_chain() DASH
I[2022-07-23 01:53:58,988] @### rune_fee 48911
I[2022-07-23 01:53:58,989] SWAP 1
I[2022-07-23 01:53:58,989] @### pool Pool BNB.BNB Rune: 157422439721 | Asset: 410150000 | Units: 118247627278 | Synth Units: 24438601696 | Synth: 140496985
I[2022-07-23 01:53:58,990] @### emit 248.09246413 THOR.RUNE
I[2022-07-23 01:53:58,990] @### liquidity_fee 6048822726
I[2022-07-23 01:53:58,991] @### liquidity_fee_in_rune 6048822726
I[2022-07-23 01:53:58,991] @### swap_slip 1960
I[2022-07-23 01:53:58,991] @### pool Pool BNB.BNB Rune: 132613193308 | Asset: 510150000 | Units: 118247627278 | Synth Units: 18883130465 | Synth: 140496985
I[2022-07-23 01:53:58,992] SWAP 2
I[2022-07-23 01:53:58,993] @### pool Pool DASH.DASH Rune: 1000000000 | Asset: 15000000000 | Units: 1000000000 | Synth Units: 0 | Synth: 0
I[2022-07-23 01:53:58,994] @### emit 5.58668498 DASH.DASH
I[2022-07-23 01:53:58,994] @### liquidity_fee 13860144443
I[2022-07-23 01:53:58,995] @### liquidity_fee_in_rune 924009630
I[2022-07-23 01:53:58,995] @### swap_slip 9613
I[2022-07-23 01:53:58,995] @### pool Pool DASH.DASH Rune: 25809246413 | Asset: 14441331502 | Units: 1000000000 | Synth Units: 0 | Synth: 0
I[2022-07-23 01:53:58,996] @### out_tx yeuSxB2Gf3UTD62dGGQfmoETxHJRW8rLpR => yLLFQTxaW3wybbahkhyZcrdfqoRCnfzAV5 [OUT:8CCFC672EA524CC25825E4C1A522176C748963B855782FCC9F3C78DDAD74BFE1] 5.58668498 DASH.DASH
I[2022-07-23 01:53:58,997] @### tx.max_gas [<Coin 0.00366832 DASH.DASH>]
I[2022-07-23 01:53:58,997] @### asset_fee 733665
I[2022-07-23 01:53:58,997] @### self.dash_estimate_size 330
I[2022-07-23 01:53:58,998] @### self.dash_tx_rate 829
E[2022-07-23 01:54:18,780] out coins not matching 557934833 DASH.DASH != 558414998 DASH.DASH
```

Trying PyStorm to see if I can step-debug this. Would be a helluva lot faster
than all this logging.




