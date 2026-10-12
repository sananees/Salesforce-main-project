# Warehouse & Logistics — Data Quality Tests

# Warehouse & Logistics — Data Quality Tests

## Proposed Test Design

Main process record: custom Shipment.
Proposed statuses: Draft, Review, Approved, Shipped.
Proposed business fields: Bin, Quantity, Shipment Reference.
Persona: Warehouse User (training persona).

Business rules:
- Bin and Shipment Reference are required before leaving Draft.
- Quantity cannot be negative.
- A shipment must pass through Review before becoming Approved.
- Only an Approved shipment can move to Shipped.
- Shipment Reference must identify a shipment uniquely.

These are planned requirements, not confirmed existing configuration.
Match field and status names to the Salesforce setup before testing.

## Test Matrix

| Test ID | Persona | Input | Expected Result | Actual Result | Evidence |
|---|---|---|---|---|---|

| V01 | Warehouse User | Create an Outbound Shipment with Warehouse populated, Status Draft, and Quantity 10. | Shipment saves successfully. | Pass — Outbound Shipment saved successfully in Draft status. | Screenshot —V01-Draft.png|
| V02 | Warehouse User | Change a Draft shipment to Review with Warehouse populated and Quantity 10. | Status changes to Review successfully. | Pass — Shipment changed from Draft to Review successfully | Screenshot — V02-Review.png|
| V03 | Warehouse User | Change a Review shipment to Approved with valid Warehouse and Quantity. | Status changes to Approved successfully. | Pass — Shipment changed from Review to Approved successfully. | Screenshot — V03-Approved.png |
| I01 | Warehouse User | Change a Draft shipment to Review with Warehouse blank and Quantity 10. | Save is blocked because Warehouse is required after Draft. | Pass — Save was blocked when moving Draft to Review with Warehouse blank. |Screenshot — I01-Warehouse-Error.png |
| I02 | Warehouse User | Save a shipment with Quantity -5. | Save is blocked because Quantity cannot be negative. | Pass — Save was blocked when Quantity was -5. | I02-Quantity-Error.png |
| I03 | Warehouse User | Change a shipment directly from Draft to Approved. | Save is blocked because the shipment must go through Review first. |Pass — Save was blocked when changing directly from Draft to Approved.| Screenshot - I03-Status-Error.png |


## Record Type Design

Object: Warehouse Shipment (Warehouse_Shipment__c)

### Inbound Shipment
Used for goods arriving at the warehouse.
Status values: Draft, Review, Approved, Receiving, Putaway,
Completed, Exception.
Default: Draft.

### Outbound Shipment
Used for goods leaving the warehouse.
Status values: Draft, Review, Approved, Picking, Packing,
Shipped, Completed, Exception.
Default: Draft.

### Reason for Two Record Types
Incoming shipments need receiving and putaway stages.
Outgoing shipments need picking, packing, and shipping stages.
Separate record types give users the relevant status choices.

Cycle counting and replenishment are internal inventory activities,
so this design does not add shipment record types for them.
Exception is available for both shipment processes.

### Page Layout Assignment
System Administrator uses Shipment Layout for both record types.
Both currently need the same fields, so they share one layout.