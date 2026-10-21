---
license: cc-by-4.0
pretty_name: LLM API Pricing Timeline
language:
- en
tags:
- llm
- pricing
- api
- tabular
size_categories:
- n<1K
configs:
- config_name: default
  data_files:
  - split: train
    path: model-pricing.csv
---

# LLM API Pricing Timeline

Input, output, cached input, batch, cache write and long-context prices per million tokens for the main LLM APIs, read daily
from each provider's official pricing page, with every change dated. Published by
3AM Marketer at https://3ammarketer.com/data/model-pricing, where the same data is shown as a table and chart.

Updated 2026-10-21: 839 rows, 455 current prices.

## Files

- `model-pricing.csv`: the whole timeline. One row per provider and model each time a published price changes.
- `model-pricing-current.csv`: today's price per model only (the rows marked current=yes).

Both files start with one comment line beginning with `#` (source and licence), then a header row.
Skip it with `comment="#"` in pandas.

## Columns

| Column | Meaning |
| --- | --- |
| provider | The company selling the API |
| model | The model name as the provider's pricing page gives it |
| input_usd_per_m | USD per million input tokens; empty when the page does not publish it |
| output_usd_per_m | USD per million output tokens; empty when the page does not publish it |
| cached_input_usd_per_m | USD per million cached input tokens; empty when the page does not publish it |
| effective_date | The date the page says the price took effect, when it says one |
| source_url | The official pricing page the row was read from |
| captured_at | When the row was recorded (UTC) |
| current | yes for today's price for that model; no for history |
| batch_input_usd_per_m | USD per million input tokens through the Batch API; empty unless the page prints it for the model |
| batch_output_usd_per_m | USD per million output tokens through the Batch API; empty unless the page prints it for the model |
| cache_write_usd_per_m | USD per million tokens written to the cache (the default 5 minute cache where there are two); empty when not published |
| long_context_threshold_tokens | Prompt length above which the long-context rates apply to the whole request; empty when the page does not state it |
| long_context_input_usd_per_m | USD per million input tokens above the long-context threshold; empty when there is no such tier |
| long_context_output_usd_per_m | USD per million output tokens above the long-context threshold; empty when there is no such tier |
| retired_at | Set on the row recording that the provider removed the model from its pricing page (UTC); the model then has no current row |

## How prices are checked

Prices are read daily from each provider's official pricing page. Every row links to that page
in `source_url`, so any price can be checked against its source. Text models priced per million
tokens only; image, audio and other units are left out.

## Update frequency

Daily.

## Licence

CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/). Credit: 3AM Marketer, https://3ammarketer.com/data/model-pricing

## Citation

3AM Marketer. LLM API Pricing Timeline. https://3ammarketer.com/data/model-pricing. Accessed 2026-10-21. Licensed CC BY 4.0.

## Contact

ops@3ammarketer.com
