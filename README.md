# REM.jl

Relational Event Models for Julia.

## Overview

REM.jl provides tools for analyzing relational event data - timestamped records of interactions between actors in a social system. It implements the Relational Event Model framework for statistical analysis of event sequences.

This package is a Julia port of the R `relevent` package's core REM functionality.

## Installation

```julia
using Pkg
Pkg.add(url="https://github.com/Statistical-network-analysis-with-Julia/REM.jl")
```

## Features

- **Event representation**: `Event{T}` type for sender-receiver-time tuples
- **Event sequences**: `EventSequence{T}` for collections of events with actor metadata
- **Statistics**: Dyadic, degree-based, triadic, and node attribute statistics
- **Case-control sampling**: Efficient estimation via stratified sampling
- **Model fitting**: `fit_rem()` using conditional logistic regression

## Quick Start

```julia
using REM

# Create events
events = [
    Event(1, 2, 0.0),
    Event(2, 3, 1.0),
    Event(1, 3, 2.0),
    Event(3, 1, 3.0)
]

# Create event sequence
seq = EventSequence(events, 3)  # 3 actors

# Define statistics
stats = [
    InertiaStatistic(halflife=10.0),
    ReciprocityStatistic(halflife=10.0),
    OutdegreeStatistic(halflife=10.0)
]

# Fit model
result = fit_rem(seq, stats)
println(result)
```

## Statistics

### Dyadic Statistics
- `InertiaStatistic`: Tendency to repeat past interactions
- `ReciprocityStatistic`: Tendency to reciprocate received events

### Degree Statistics
- `OutdegreeStatistic`: Sender activity effect
- `IndegreeStatistic`: Receiver popularity effect

### Triadic Statistics
- `TransitivityStatistic`: Friend-of-friend effects
- `CyclicClosureStatistic`: Cyclic closure tendency

### Node Attribute Statistics
- `SenderEffectStatistic`: Effect of sender attributes
- `ReceiverEffectStatistic`: Effect of receiver attributes
- `HomophilyStatistic`: Similarity effects

## References

- Butts, C. T. (2008). A relational event framework for social action. Sociological Methodology, 38(1), 155-200.
- Stadtfeld, C., & Block, P. (2017). Interactions, actors, and time: Dynamic network actor models for relational events. Sociological Science, 4, 318-352.

## License

MIT License
