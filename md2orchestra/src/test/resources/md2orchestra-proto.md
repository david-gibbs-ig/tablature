# Rules of Engagement

#### Overview

Order messages and their elements.

## Message NewOrderSingle type 'D'

#### Synopsis

The new order message type is used by institutions wishing to electronically submit securities and forex orders to a broker for execution.

#### Elaboration

The NewOrderSingle(35=D) message type may also be used by institutions or retail intermediaries wishing to electronically submit Collective Investment Vehicle (CIV) orders to a broker or fund manager for execution.

| Name           | Tag | Presence                |
|----------------|----:|-------------------------|
| ClOrdID        | 11  | required                |
| Account        |     |                         |
| Instrument     | c   |                         |
| Side           |     | required                |
| Price          |     |                         |
| StopPx         |     | required when OrdType=3 |
| OrderQty       |     | required                |
| OrdType        |     | required                |
| MyUserDefined1 |     |                         |
| MyUserDefined2 | 6235|                         |	
| Parties        | g   |                         |

## Fields

| Name           | Tag | Type         |  Values          | Synopsis | Elaboration | TestCase |
|----------------|----:|--------------|------------------|----------|-------------|----------|
| Side           | 54  | SideCodeSet  |	                 |          |             | 1        |
| OrdType        | 40  | char         | 1=Market 2=Limit |          |             | 2        |
| MyUserDefined1 | 6234| UTCTimestamp |	                 |          |             | 3        |
| ContractMultiplierUnitCodeSet | 1437 | | | Indicates the type of multiplier being applied to the contract. | Can be optionally used to further define unit |

## Component Instrument 

The `Instrument` component block contains all the fields commonly used to describe a security or instrument.

| Name             | Tag | Presence  | Values |
|------------------|----:|-----------|--------|
| SecurityID       | 48  | required  |        |
| SecurityIDSource | 22  | constant  | 8      |

## Group Parties 

The Parties component block is used to identify and convey information on the entities both central and peripheral to the financial transaction represented by the FIX message containing the `Parties` Block. 

| Name           | Tag | Presence  | Values |
|----------------|----:|-----------|--------|
| NoParties      | 453 |           |        |
| PartyID        |     | required  |        |
| PartyIDSource  |     |           |        |
| PartyRole      |     | required  | 1=ExecutingFirm 2=BrokerOfCredit |

### Codeset SideCodeSet 

Side of an order

| Name     | Value | Documentation |
|----------|-------|---------------|
| Buy      | 1     |               |
| Sell     | 2     |               |
| Cross    | 8     | Cross (orders where counterparty is an exchange, valid for all messages *except* IOIs) |
| Opposite | C     | "Opposite" (for use with multileg instruments) |