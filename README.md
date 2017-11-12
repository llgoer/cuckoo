[![Build Status](https://travis-ci.org/AidosKuneen/cuckoo.svg?branch=master)](https://travis-ci.org/AidosKuneen/cuckoo)
[![GoDoc](https://godoc.org/github.com/AidosKuneen/cuckoo?status.svg)](https://godoc.org/github.com/AidosKuneen/cuckoo)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/AidosKuneen/cuckoo/master/LICENSE)


Cuckoo Cycle
=====

## Overview

This library is [Cockoo Cycle](https://github.com/tromp/cuckoo) in Go 
mentiond in [this paper](https://github.com/tromp/cuckoo/blob/master/doc/cuckoo.pdf).

In short, 

```
Cuckoo Cycle is the first graph-theoretic proof-of-work, and the most memory bound, yet with instant verification.
```

to prevent ASICs to get half of hash power easier in network, without heavy work for proover.

This library uses below parameters.

* cycle = 20 to minimize the size impact to transactions.
* bits of nodes (log2(#nodes)) = 26, memory usage should be around 256MB.
* easiness = 100% to prevent optimizations e.g. by edge trimming.
* largest nonce must be over #nodes * 0.7 to prevent earlier solution.


## Requirements

* git
* go 1.9+

are required to compile.


## Install
    $ go get -u github.com/AidosKuneen/cuckoo


## Usage

```go
	import "github.com/AidosKuneen/cuckoo"
	var hash []byte //should be 32 bytes
	nonces, found := cuckoo.PoW(hash)
	if !found{
		//retry with another hash
	}

	if !cuckoo.Verify(hash,nonces){
		//failed to verify
	}
```
