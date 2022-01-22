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
[13.01.2022 Thursday 7hrs](#13012022-thursday)  
[14.01.2022 Friday 7hrs](#14012022-friday)  
[19.01.2022 Wednesday 7hrs](#19012022-wednesday)  
[20.01.2022 Thursday 7hrs](#20012022-thursday)  
[21.01.2022 Friday 7hrs](#21012022-friday)  

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
- [ ] Submit to @HildisvíniÓttar for a vulnerability review
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
