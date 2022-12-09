# CPMM

The ``CPMM`` module (**C**onstant **P**roduct **M**arket **M**aker) provides functionalities related with liquidity pools on the Chaos DEX.

## Contents

1. **[Concepts](#concepts)**
2. **[States](#states)**
3. **[Messages](#messages)**
4. **[Transactions](#transactions)**
5. **[Query](#query)**

## Concepts
The `x/cpmm` module implements an AMM using CPMM model with pool having more than 2 tokens.

## States

### Pair

```go
type Pair struct {
    Id          uint64
    CoinDenoms  []string
    Prices      []sdk.Dec   
}
```

### Pool

```go
    Id              uint64
    PairId          uint64
    ReserveAddress  string
    PoolCoinDenom   string
    MinPrice        []sdk.Dec
    MaxPrice        []sdk.Dec
```

## Message

### MsgCreatePair

```go
type MsgCreatePair struct {
    CoinDenoms  []string
}
```

### MsgCreatePool

```go
type MsgCreatePool struct {
    Creator         string
    PairId          uint64
    DepositCoins    sdk.Coins
    MinPrice        []sdk.Dec
    MaxPrice        []sdk.Dec
}
```

### MsgDeposit

```go
type MsgDeposit struct {
    Depositor       string
    PoolId          uint64
    DepositCoins    sdk.Coins
}
```

### MsgWithdraw

```go
type MsgWithdraw struct {
    Withdrawer  string
    PoolId      uint64
    PoolCoin    sdk.Coin
}
```


### MsgSwap

`MsgSwap` considers multi-hop swap via multiple pairs.

```go
type MsgSwap struct {
    Orderer     string
    PairIds     []uint64
    CoinIn      sdk.Coin
    MinCoinOut  sdk.Coin
}
```