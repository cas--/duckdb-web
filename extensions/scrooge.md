---
layout: community_extension
title: scrooge
excerpt: |
  DuckDB Community Extensions
  Provides functionality for financial data-analysis. Including data scanners for the Ethereum Blockchain and Yahoo Finance.

extension:
  name: scrooge
  description: Provides functionality for financial data-analysis. Including data scanners for the Ethereum Blockchain and Yahoo Finance.
  version: 0.0.1
  language: C++
  excluded_platforms: "windows_amd64_rtools"
  build: cmake
  license: MIT
  maintainers:
    - pdet

repo:
  github: pdet/Scrooge-McDuck
  ref: fc7ef9c9c6aad1406cddd6e98d919a154e5aa1d6

docs:
  hello_world: |
    -- Set the RPC Provider
    set eth_node_url= 'https://mempool.merkle.io/rpc/eth/pk_mbs_0b647b195065b3294a5254838a33d062';
    -- Query Transfer events of USDT from blocks 20034078 - 20034100 while parallelizing on one block per thread
    FROM read_eth(
    'USDT',
    'Transfer',
    20034078,
    20034100, 
    blocks_per_thread=1
    );
  extended_description: |
    Scrooge McDuck is a third-party financial extension for DuckDB. 
    This extension's main goal is to support a set of aggregation functions and data scanners for financial data. 
    It currently supports access to the logs of Ethereum nodes and stock information from Yahoo Finance.
    More information on the supported scanners and functions can be found on Scrooge's [wiki page](https://github.com/pdet/Scrooge-McDuck/wiki).
    You can also find a ROI example of Ether on the [following blogpost](https://pdet-blog.github.io/2024/06/30/ethereum.html)

extension_star_count: 118 

---

### Installing and Loading
```sql
INSTALL {{ page.extension.name }} FROM community;
LOAD {{ page.extension.name }};
```

{% if page.docs.hello_world %}
### Example
```sql
{{ page.docs.hello_world }}```
{% endif %}

{% if page.docs.extended_description %}
### About {{ page.extension.name }}
{{ page.docs.extended_description }}
{% endif %}

### Added Functions

<div class="extension_functions_table"></div>

|   function_name    | function_type | description | comment | example |
|--------------------|---------------|-------------|---------|---------|
| first_s            | aggregate     |             |         |         |
| last_s             | aggregate     |             |         |         |
| portfolio_frontier | table         |             |         |         |
| read_eth           | table         |             |         |         |
| sma                | aggregate     |             |         |         |
| timebucket         | scalar        |             |         |         |
| volatility         | aggregate     |             |         |         |
| yahoo_finance      | table         |             |         |         |

### Added Settings

<div class="extension_settings_table"></div>

|     name     |            description             | input_type | scope  |
|--------------|------------------------------------|------------|--------|
| eth_node_url | URL of Ethereum node to be queried | VARCHAR    | GLOBAL |



---
