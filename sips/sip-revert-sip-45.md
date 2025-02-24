|   SIP-Number | <Leave this blank; it will be assigned by a SIP Editor> |
|         ---: | :--- |
|        Title | revert SIP-45 |
|  Description | revert SIP-45 deterministic block order |
|       Author | moonshiesty<@moonshiesty> |
|       Editor | <Leave this blank; it will be assigned by a SIP Editor> |
|         Type | Standard |
|     Category | Core |
|      Created | 2025-02-23 |
| Comments-URI | <Leave this blank; it will be assigned by a SIP Editor> |
|       Status | <Leave this blank; it will be assigned by a SIP Editor> |
|     Requires | <Optional; SIP number(s), comma separated> |

## Abstract

Revert deterministic block ordering as implemented in SIP-45

## Motivation

SIP-45 does not achieve it's goals of prioritizing block-submission and instead provides a deterministic mechanism for searchers to position their transactions within a block by manipulating gas price

for example SIP-45 allows a searcher to construct a sandwich by paying +1 of the target gas price on the frontrun and -1 unit SUI of the target gas price on the backrun. this is the optimal strategy for any searcher.

for backruns SIP-45 also does not maximize value for validators since it will always be optimial for searchers to pay exactly -1 unit of SUI to be ordered right after the target

for arbitrage SIP-45 does maximize validator value, at the risk of providing yet another mechanism for arbitragers themselves to be deterministically frontrun


## Specification

Revert SIP-45 and begin exploring of one of two approaches:

1) make consensus ordering random. sui randomness already provides a seed to randomly reorder transactions. this approach likely requires an additional hop to sequence consensus. this attempts minimizes extractable value by making it non-deterministic for searchers to place a transaction within a block. my concern with this approach is that searchers can attempt to statistically frontrun targets by spamming transactions that revert if they don't land in the right spot

2) allow validators to specify how they want to be consensus ordering and expose an API for searchers to propose ordering. this approach will maximize extractable value for validators and provide the equivalent of a "block-building" API on SUI


## Rationale

reverting SIP-45 an important issue because deterministic block ordering exposes users to MEV without a way to protect themselves through fee markets

front-running on SUI is possible whenever either:
1) protocol leaks information about transactions
2) a validator leaks information about transaction certification

because shio is leaking user transactions this is present concern to SUI users

source:

https://x.com/moon_shiesty/status/1893783038653571292

## Backwards Compatibility


no issues with backwards compatibility

## Security Considerations

None
