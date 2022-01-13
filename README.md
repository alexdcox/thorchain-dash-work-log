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
[12.01.2022 Wednesday 7hrs](#12012022-wednesday)  

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
```bash
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


