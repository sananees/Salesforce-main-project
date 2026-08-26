# Application Personas

## 1. Warehouse Associate

### Goals

* Receive, store, pick, and pack products correctly.
* Complete assigned warehouse work on time.
* Report damaged, missing, or incorrect products.

### Daily Tasks

* Record received products.
* Put products in assigned storage locations.
* Pick and pack products for orders.
* Update task statuses.
* Report warehouse exceptions.

### Records Created

* Receiving records
* Putaway records
* Picking and packing records
* Exception records

### Records Reviewed

* Assigned warehouse tasks
* Product and storage-location information
* Order item details

### Decisions Made

* Confirm whether the received quantity is correct.
* Select the correct storage location.
* Decide when damaged or missing products must be reported.

### Information They Must Not See

* Employee payroll or personal information
* Supplier contracts and confidential prices
* Management-only reports
* Salesforce passwords, tokens, or system settings

### Frustration or Risk

Incorrect or unclear product information could cause an item to be stored or shipped incorrectly.

### Measurable Success Outcome

At least 98% of assigned warehouse tasks are completed accurately during the employee’s shift.

---

## 2. Inventory Controller

### Goals

* Keep system inventory equal to the physical inventory.
* Find and correct inventory differences.
* Ensure picking locations have enough stock.

### Daily Tasks

* Perform cycle counts.
* Review inventory levels.
* Investigate stock differences.
* Create replenishment requests.
* Review inventory adjustments.

### Records Created

* Cycle-count records
* Inventory-adjustment records
* Replenishment requests
* Inventory exception records

### Records Reviewed

* Inventory item records
* Storage-location records
* Receiving and picking records
* Previous inventory adjustments

### Decisions Made

* Approve or reject inventory adjustments.
* Decide when stock must be replenished.
* Decide when an inventory difference requires investigation.

### Information They Must Not See

* Employee payroll or personal information
* Customer payment information
* Salesforce authentication credentials
* Information unrelated to inventory control

### Frustration or Risk

Late or incorrect warehouse updates could make the system inventory different from the physical inventory.

### Measurable Success Outcome

Maintain at least 98% inventory accuracy and investigate important differences within one business day.

---

## 3. Logistics Coordinator

### Goals

* Prepare shipments correctly and on time.
* Coordinate carriers and delivery information.
* Resolve shipping delays and exceptions.

### Daily Tasks

* Review packed orders.
* Create shipment records.
* Enter tracking and carrier details.
* Update shipment statuses.
* Investigate delayed or failed shipments.

### Records Created

* Shipment records
* Tracking records
* Delivery exception records
* Carrier communication notes

### Records Reviewed

* Orders ready for shipping
* Packing records
* Customer delivery details
* Shipment and tracking statuses

### Decisions Made

* Select the correct carrier or shipping service.
* Decide whether an order is ready to ship.
* Escalate delayed, missing, or damaged shipments.

### Information They Must Not See

* Employee payroll information
* Unrelated supplier contracts
* Salesforce passwords and access tokens
* Private management information unrelated to shipping

### Frustration or Risk

Incorrect addresses, missing tracking information, or late packing could delay a shipment.

### Measurable Success Outcome

At least 95% of completed orders are shipped on time with correct tracking information.

---

## 4. Operations Manager

### Goals

* Keep warehouse operations safe, accurate, and efficient.
* Monitor performance across receiving, inventory, picking, and shipping.
* Resolve serious operational problems.

### Daily Tasks

* Review warehouse dashboards.
* Monitor inventory accuracy and order progress.
* Review exceptions and delays.
* Assign priorities to warehouse teams.
* Approve important operational decisions.

### Records Created

* Management notes
* Corrective-action records
* Escalation records
* Operational improvement requests

### Records Reviewed

* Receiving and putaway records
* Inventory and cycle-count records
* Picking and packing records
* Shipment and exception records
* Warehouse performance reports

### Decisions Made

* Prioritize urgent orders and warehouse work.
* Approve important inventory corrections.
* Reassign employees or resources.
* Escalate serious delays, shortages, or safety problems.

### Information They Must Not See

* Salesforce passwords, tokens, and authentication files
* Information outside their authorized business area
* Private system-administration credentials
* Unnecessary personal employee information

### Frustration or Risk

Incomplete or delayed information could cause the manager to make the wrong operational decision.

### Measurable Success Outcome

At least 95% of warehouse orders meet the expected processing and shipping time.
