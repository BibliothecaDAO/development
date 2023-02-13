---
sidebar_position: 2
---

# Loot Hello World

Test your setup by minting a Loot item from your account.

---

## Step 1. Get your environment set up

Set up your environment [manually](/docs/getting-started/environment) or [using docker](/docs/cli/docker). If you're using docker, run this to get shell access once your image is built:

```
$ docker run -it --entrypoint /bin/bash realms_cli
```

Also make sure your account is funded with a small amount of Goerli ETH.

---

## Step 2. List the commands you can run

See the list of available commands by running:

```
$ nile
```
---

## Step 3. Mint a Loot item

Run the following command to mint a Loot item:

```
$ nile mint_loot
```

You should see output that looks like:

```
⏳ Querying the network to check transaction status and identify contracts...
🕒 Transaction status: RECEIVED. Trying again in a moment...
🕒 Transaction status: RECEIVED. Trying again in a moment...
🕒 Transaction status: PENDING. Trying again in a moment...
🕒 Transaction status: PENDING. Trying again in a moment...
🕒 Transaction status: PENDING. Trying again in a moment...
✅ Transaction status: ACCEPTED_ON_L2. No error in transaction.
```

Once that's done, check the explorer to see your Loot item by going to `https://goerli.voyager.online/contract/<account_address>#transactions`.

For example, if your account address is 0x02c01a3b299b0badbea54846a469bb146c305aca47bbeb80e7e58232a4b57a8e, then go to https://goerli.voyager.online/contract/0x02c01a3b299b0badbea54846a469bb146c305aca47bbeb80e7e58232a4b57a8e#transactions

On the transactions page, click on the latest transactions hash, then click on events: https://goerli.voyager.online/tx/0x5f7febb2d4b3b34a62a220fb11b933c7e3a746698be908f4e5d3e9c3f16cce8#events

The data field for Event 1 should look like:

```
[0]: 0
[1]: 1244041374027438511511608435205679134226560852740256554748835554917069716110
[2]: 10
[3]: 0
```
Your Loot item TokenID is the value of the index `[2]`, in this case 10.

---

## Step 4. Inspect your Loot item

Run the following command to inspect the Loot item with the TokenID you minted in the previous step (e.g. TokenID 10):

```
$ nile get_loot 10
```

This should give you the following output:

```
------- CALL ----------------------------------------------------
calling getItemByTokenId from proxy_Loot with ['10', 0]
------- CALL ----------------------------------------------------
_________ LOOT ITEM - 63___________

| Id : 63                                  | Slot : 5
| Type : 202                               | Material : 3205
| Rank : 2                                 | Prefix_1 :
| Prefix_2 :                               | Suffix :
| Greatness : 0                            | CreatedBlock : 1663898665
| XP : 0                                   | Adventurer : 0
| Bag : 0
```

You've minted your first Loot item, congrats!
