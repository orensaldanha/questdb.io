---
title: Regex operators
sidebar_label: Regex
description: Regex operators reference documentation.
---

This page describes the available operators to assist with performing pattern
matching via regular expressions.

## ~ (match)

`string ~ regex` - matches `string` value to regex

`symbol ~ regex` - matches `symbol` value to regex

[java.util.regex](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/regex/Pattern.html)

## !~ (does not match)

`string !~ regex` - checks if `string` value does not match regex

`symbol !~ regex` - checks if `symbol` value does not match regex

## LIKE 

The `LIKE` operator returns true if it matches the specified pattern

`string LIKE pattern` - checks if `string` value matches `pattern`

The pattern can contain wildcards which are interpreted as follows:
- `?` - matches any single character
- `%` - matches any sequence of zero or more characters

Wildcards can be used as follows:

|      query           | result  |
| -------------------- | ------- |
| 'quest' LIKE 'quest' |  true   |
| 'quest' LIKE 'quest_'|  true   |
| 'quest' LIKE 'que%'  |  true   |
| 'quest' LIKE '\_ues_' |  true   |
| 'quest' LIKE 'q_'    |  false  |

### Example

```questdb-sql 
SELECT * FROM trades
WHERE symbol LIKE '%-USD'
LATEST ON timestamp PARTITION BY symbol;
```

| symbol | side | price | amount | timestamp |
| --- | --- | --- | --- | --- |
| ETH-USD | sell | 1348.13 | 3.22455108 | 2022-10-04T15:25:58.834362Z |
| BTC-USD | sell | 20082.08 | 0.16591219 | 2022-10-04T15:25:59.742552Z |