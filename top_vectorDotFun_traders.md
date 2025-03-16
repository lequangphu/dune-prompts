You have access to the following tables in the DuneSQL database to query and analyze data to achieve a goal I'm about to describe.
Each table may have partition columns listed at the bottom. If they exist, you must use them in your queries to filter the data.

table: dex_solana.trades
schema:
| name | type |
| --- | --- |
| blockchain | string |
| project | string |
| version | integer |
| block_month | date |
| block_time | timestamp |
| block_slot | long |
| trade_source | string |
| token_bought_symbol | string |
| token_sold_symbol | string |
| token_pair | string |
| token_bought_amount | double |
| token_sold_amount | double |
| token_bought_amount_raw | uint256 |
| token_sold_amount_raw | uint256 |
| amount_usd | double |
| fee_tier | double |
| fee_usd | double |
| token_bought_mint_address | string |
| token_sold_mint_address | string |
| token_bought_vault | string |
| token_sold_vault | string |
| project_program_id | string |
| project_main_id | string |
| trader_id | string |
| tx_id | string |
| outer_instruction_index | integer |
| inner_instruction_index | integer |
| tx_index | integer |
partition by block_month

table: tokens_solana.transfers
schema:
| name | type |
| --- | --- |
| block_month | date |
| block_date | date |
| block_hour | timestamp(3) with time zone |
| block_time | timestamp(3) with time zone |
| block_slot | bigint |
| action | varchar |
| amount | uint256 |
| amount_display | double |
| amount_usd | double |
| price_usd | double |
| token_mint_address | varchar |
| symbol | varchar |
| from_owner | varchar |
| to_owner | varchar |
| from_token_account | varchar |
| to_token_account | varchar |
| token_version | varchar |
| tx_signer | varchar |
| tx_id | varchar |
| outer_instruction_index | integer |
| inner_instruction_index | integer |
| outer_executing_account | varchar |
partition by block_date

Make a plan to achieve a goal, explain the applied math/logic/method, step by step.
Each step must have a query of its own to review.
Apply query optimizations as early as possible, for example: filter data before joining, join before aggregating, etc.
At the end of each step, stop and wait for my review before moving on to the next step.

<goal>
    Find top traders of https://www.vector.fun/, a trading app on Solana blockchain.
    Measure the traders performance the same as the investing industry measures elite traders/investors.
    What are on/off-chain data needed to calculate the measures?
</goal>

Hint: to get trades of vector dot fun, join with transfer table, filter for transfers which have `outer_executing_account = 'VFeesufQJnGunv2kBXDYnThT1CoAYB45U31qGDe5QjU'`.
