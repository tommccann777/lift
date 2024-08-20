# Using icrc1_ledger canister

This set of canisters creates LIFT (Lift Cash) token.
Then it demonstrates how to mint by transferring from the minter id to a user.

## Step 1: Set up the environment variables used in step 2:

Edit set_env.sh as appropriate, then run this command. (Using the test ids in the file test ids):
`source set_env.sh`

## Step 2: Command to deploy this contract:

```
dfx deploy icrc1_ledger_canister --specified-id mxzaz-hqaaa-aaaar-qaada-cai --argument "(variant {Init =
record {
token_symbol = \"${TOKEN_SYMBOL}\";
     token_name = \"${TOKEN_NAME}\";
minting_account = record { owner = principal \"${MINTER}\" };
     transfer_fee = ${TRANSFER_FEE};
     metadata = vec {};
     feature_flags = opt record{icrc2 = ${FEATURE_FLAGS}};
     initial_balances = vec { record { record { owner = principal \"${DEFAULT}\"; }; ${PRE_MINTED_TOKENS}; }; };
     archive_options = record {
         num_blocks_to_archive = ${NUM_OF_BLOCK_TO_ARCHIVE};
         trigger_threshold = ${TRIGGER_THRESHOLD};
         controller_id = principal \"${ARCHIVE_CONTROLLER}\";
cycles_for_archive_creation = opt ${CYCLE_FOR_ARCHIVE_CREATION};
};
}
})"
```

## Step 3: Command to transfer 50,000 tokens from the minter account to user alice

```
dfx canister call icrc1_ledger_canister icrc1_transfer '(
record {
from = opt principal "oi3ng-j6cnw-owsv3-4gtwq-nqfhh-ghwzh-assfr-khsv2-d37rq-2ejnj-xqe";
to = record {
owner = principal "blwz3-4wsku-3otjv-yriaj-2hhdr-3gh3e-x4z7v-psn6e-ent7z-eytoo-mqe";
subaccount = null;
};
amount = 50000;
fee = opt 0;
memo = opt blob "Test of minting";
created_at_time = null;
}
)'
```

Should respond with: `(variant { Ok = 1 : nat })`
