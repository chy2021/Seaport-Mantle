# Seaport

Seaport is a marketplace protocol for safely and efficiently buying and selling NFTs.

## Table of Contents

- [Seaport](#seaport)
  - [Table of Contents](#table-of-contents)
  - [Background](#background)
  - [Diagram](#diagram)

## Background

Seaport is a marketplace protocol for safely and efficiently buying and selling NFTs. Each listing contains an arbitrary number of items that the offerer is willing to give (the "offer") along with an arbitrary number of items that must be received along with their respective receivers (the "consideration").

See the [documentation](docs/SeaportDocumentation.md), the [interface](contracts/interfaces/SeaportInterface.sol), and the full [interface documentation](https://docs.opensea.io/v2.0/reference/seaport-overview) for more information on Seaport.



## Diagram

```mermaid
graph TD
    Offer & Consideration --> Order
    zone & conduitKey --> Order

    subgraph Seaport[ ]
    Order --> Fulfill & Match
    Order --> Validate & Cancel
    end

    Validate --> Verify
    Cancel --> OrderStatus

    Fulfill & Match --> OrderCombiner --> OrderFulfiller

    OrderCombiner --> BasicOrderFulfiller --> OrderValidator
    OrderCombiner --> FulfillmentApplier

    OrderFulfiller --> CriteriaResolution
    OrderFulfiller --> AmountDeriver
    OrderFulfiller --> OrderValidator

    OrderValidator --> ZoneInteraction
    OrderValidator --> Executor --> TokenTransferrer
    Executor --> Conduit --> TokenTransferrer
    Executor --> Verify

    subgraph Verifiers[ ]
    Verify --> Time & Signature & OrderStatus
    end
```

For a more thorough flowchart see [Seaport diagram](./diagrams/Seaport.drawio.svg).
