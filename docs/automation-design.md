# Week 07 Automation Design

## Process Phases

The Warehouse Management & Logistics App includes these process phases:

1. Receiving
2. Putaway
3. Cycle Counting
4. Replenishment
5. Picking
6. Packing
7. Shipping
8. Exception Handling

## Automation Design

| Process Phase | Trigger | Condition | Field Updates | Related Records | Notification | Failure Behavior | Automation Type |
|---|---|---|---|---|---|---|---|
| Receiving | Warehouse Shipment is created or updated | Shipment reaches Received status | Update shipment status and receiving information | Update or create related Inventory Item records when needed | Notify warehouse staff if receiving is complete | Leave the shipment unchanged and record the error if related updates fail | After-Save Flow |
| Putaway | Stock Movement is created | A valid source and destination Bin are selected | Update movement status and destination information | Update related Inventory Item/Bin information | No notification for normal putaway | Show or record an error when required Bin information is missing | After-Save Flow |
| Cycle Counting | User starts a count | User selects an Inventory Item or Bin to count | Save the confirmed quantity | Update the selected Inventory Item | Show confirmation to the user | Display an error and do not save an invalid quantity | Screen Flow |
| Replenishment | Runs on a schedule | Available quantity is at or below the reorder point | Update stock-risk/replenishment status if required | Create a task or replenishment record when needed | Notify Inventory Controller | Skip invalid records and log the failure | Scheduled Flow |
| Picking | Inventory Item or Stock Movement changes | Item is ready to be picked | Update Pick Status on the same record | No related record update required for the simple status change | None | Prevent the update if required information is missing | Before-Save Flow |
| Packing | Shipment is ready after picking | Picking is complete | Update shipment to Packed | Update related shipment information if required | Notify Logistics Coordinator when packing is complete | Keep the prior status if the update fails | After-Save Flow |
| Shipping | Warehouse Shipment changes to Shipped | Shipment is approved and ready to leave | Update shipping status/details | Create a related Carrier Event | Notify Logistics Coordinator or Operations Manager | Do not create duplicate Carrier Events; record the error | After-Save Flow |
| Exception Handling | Called when another automation detects a problem | Required data is missing or a process fails | Update an exception/status field when appropriate | May create a task or error record | Notify the correct operational user | Log the issue for review instead of silently failing | Subflow |

## Automation Classification

- **Before-Save Flow:** Use for simple updates to the same record, such as Pick Status.
- **After-Save Flow:** Use when related records must be created or updated, such as Inventory Items or Carrier Events.
- **Screen Flow:** Use when a warehouse user must enter or confirm information, such as cycle counting.
- **Scheduled Flow:** Use for recurring checks, such as replenishment.
- **Subflow:** Use reusable exception-handling logic that can be called by other flows.
- **Apex Later:** Consider Apex only if processing becomes highly complex, high-volume, or cannot be handled efficiently with Flow.
- **Manual:** Keep processes manual when automation would not provide a clear business benefit.

## Overlap Check

Each automation has one clear responsibility.

- Receiving automation owns receiving-related shipment processing.
- Picking automation owns Pick Status updates.
- Packing automation handles the transition to Packed.
- Shipping automation handles the transition to Shipped and creates Carrier Events.
- Replenishment automation handles scheduled low-stock checks.
- Exception Handling does not duplicate normal business updates; it only handles failures.

No two automations update the same field for the same event.

## Design Decision

The project will use Flow as the main automation layer because most warehouse processes are simple to moderately complex. Apex will be considered later only if a requirement needs complex logic, large-volume processing, or additional transaction control.