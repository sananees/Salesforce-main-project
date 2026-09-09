# Initial Warehouse User-Story Backlog

## First Usable Release

The following four stories are required for the first usable release:

- US-01 — Record an Incoming Shipment
- US-02 — Assign a Putaway Location
- US-07 — Pick and Pack an Order
- US-09 — Create a Shipment and Tracking Number

---

## US-01 — Record an Incoming Shipment

**Priority:** Must  
**Release:** First usable release

**User Story:** As a Warehouse Associate, I want to record an incoming shipment so that received products are added to warehouse inventory.

### Acceptance Criteria

1. **Given** a valid purchase order and delivery, **when** the associate enters the products and quantities, **then** a receiving record is created.
2. **Given** damaged, missing, or incorrect products, **when** the associate records the problem, **then** an exception is created.
3. **Given** a completed receiving record, **when** it is saved, **then** the inventory quantity is updated.

---

## US-02 — Assign a Putaway Location

**Priority:** Must  
**Release:** First usable release

**User Story:** As a Warehouse Associate, I want to assign received products to storage locations so that employees can find them later.

### Acceptance Criteria

1. **Given** a received product awaiting putaway, **when** the associate opens the task, **then** available locations are displayed.
2. **Given** a valid location with enough capacity, **when** it is selected, **then** the product location is updated.
3. **Given** a full or incorrect location, **when** the associate selects it, **then** the system prevents the update and shows an error.

---

## US-03 — Perform a Cycle Count

**Priority:** Should  
**Release:** Future release

**User Story:** As an Inventory Controller, I want to perform scheduled cycle counts so that physical inventory matches system inventory.

### Acceptance Criteria

1. **Given** a scheduled cycle count, **when** the controller opens it, **then** the assigned products and locations are displayed.
2. **Given** matching physical and system quantities, **when** the count is submitted, **then** it is marked complete.
3. **Given** different quantities, **when** the count is submitted, **then** an inventory-variance record is created.

---

## US-04 — Approve an Inventory Adjustment

**Priority:** Should  
**Release:** Future release

**User Story:** As an Operations Manager, I want to approve important inventory adjustments so that stock changes are controlled.

### Acceptance Criteria

1. **Given** a variance above the allowed amount, **when** an adjustment is submitted, **then** its status becomes Pending Approval.
2. **Given** an authorized manager’s approval, **when** the approval is completed, **then** inventory is updated and the action is recorded.
3. **Given** an unauthorized user, **when** the user attempts to approve an adjustment, **then** access is denied.

---

## US-05 — Create a Replenishment Request

**Priority:** Should  
**Release:** Future release

**User Story:** As an Inventory Controller, I want to create replenishment requests so that picking locations have enough stock.

### Acceptance Criteria

1. **Given** stock below the selected minimum, **when** the inventory is checked, **then** a replenishment request is created.
2. **Given** enough reserve stock, **when** the request is assigned, **then** a replenishment task is created.
3. **Given** insufficient reserve stock, **when** the request is processed, **then** an exception is created.

---

## US-06 — Generate a Pick List

**Priority:** Must  
**Release:** Future release

**User Story:** As a Warehouse Associate, I want to view an order pick list so that I can collect the correct products.

### Acceptance Criteria

1. **Given** an approved customer order, **when** picking begins, **then** a pick list is generated.
2. **Given** available inventory, **when** the pick list is generated, **then** it shows each product, quantity, and location.
3. **Given** insufficient inventory, **when** the pick list is generated, **then** the affected order item is marked as an exception.

---

## US-07 — Pick and Pack an Order

**Priority:** Must  
**Release:** First usable release

**User Story:** As a Warehouse Associate, I want to pick and pack an order so that it is ready for shipping.

### Acceptance Criteria

1. **Given** an assigned pick list, **when** the correct products are scanned, **then** their status becomes Picked.
2. **Given** an incorrect product or quantity, **when** it is scanned, **then** the system displays an error.
3. **Given** all correct products are packed, **when** the associate completes the task, **then** the order status becomes Packed.

---

## US-08 — Verify a Shipping Label

**Priority:** Could  
**Release:** Future release

**User Story:** As a Logistics Coordinator, I want to verify shipping labels so that packages are delivered to the correct address.

### Acceptance Criteria

1. **Given** a packed order, **when** its label and delivery address match, **then** the package is marked Verified.
2. **Given** an address or label mismatch, **when** verification occurs, **then** shipping is blocked and an exception is created.
3. **Given** a user without shipping permission, **when** the user attempts to view the customer’s address, **then** access to the sensitive information is denied.

---

## US-09 — Create a Shipment and Tracking Number

**Priority:** Must  
**Release:** First usable release

**User Story:** As a Logistics Coordinator, I want to create a shipment and tracking number so that the package can be monitored.

### Acceptance Criteria

1. **Given** a verified packed order, **when** it is submitted to the carrier, **then** a shipment record is created.
2. **Given** carrier acceptance, **when** a tracking number is returned, **then** it is saved on the shipment.
3. **Given** a carrier-integration failure, **when** submission fails, **then** the shipment is marked Failed and an exception is created.

---

## US-10 — Resolve a Shipping Exception

**Priority:** Should  
**Release:** Future release

**User Story:** As a Logistics Coordinator, I want to resolve shipping exceptions so that delayed or rejected shipments can continue.

### Acceptance Criteria

1. **Given** a rejected or delayed shipment, **when** the carrier reports the problem, **then** an exception is created.
2. **Given** a correctable problem, **when** the coordinator updates the information, **then** the shipment can be submitted again.
3. **Given** an unresolved shipping problem, **when** the coordinator cannot correct it, **then** it is escalated to the Operations Manager.

---

## US-11 — Manage Warehouse Exceptions

**Priority:** Must  
**Release:** Future release

**User Story:** As an Operations Manager, I want to manage warehouse exceptions so that serious problems are resolved and recorded.

### Acceptance Criteria

1. **Given** an exception from any warehouse phase, **when** it is created, **then** it is assigned to the responsible person.
2. **Given** a completed corrective action, **when** the resolution is saved, **then** the exception is marked Resolved.
3. **Given** an exception requiring approval, **when** someone attempts to close it, **then** only an authorized Operations Manager can approve it.

---

## US-12 — View a Warehouse Dashboard

**Priority:** Later  
**Release:** Future release

**User Story:** As an Operations Manager, I want to view warehouse performance so that I can identify delays and inventory problems.

### Acceptance Criteria

1. **Given** an authorized manager, **when** the dashboard opens, **then** it displays inventory accuracy, open exceptions, and shipment performance.
2. **Given** selected date and warehouse filters, **when** they are applied, **then** the dashboard results are updated.
3. **Given** an unauthorized user, **when** the user attempts to open confidential management reports, **then** access is denied.