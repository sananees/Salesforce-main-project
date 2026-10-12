# Security Matrix

## Object-Level Access

| Persona | Warehouse | Zone | Bin | Product | Inventory Item | Stock Movement | Shipment | Carrier Event |
|---|---|---|---|---|---|---|---|---|
| Warehouse Associate | Read | Read | Read, Edit | Read | Read, Edit | Create, Read | Read | Read |
| Inventory Controller | Read | Read | Read, Edit | Read, Edit | Create, Read, Edit | Create, Read, Edit | Read | Read |
| Logistics Coordinator | Read | Read | Read | Read | Read | Read | Create, Read, Edit | Create, Read, Edit |
| Operations Manager | View All | View All | View All | View All | View All | View All | View All | View All |

## Sensitive Fields

| Field / Information | Warehouse Associate | Inventory Controller | Logistics Coordinator | Operations Manager |
|---|---|---|---|---|
| Warehouse External ID | Read | Read | Read | Read, Edit |

| Shipment Quantity | Read | Read | Read, Edit | Read, Edit |
| Shipment Status | Read | Read | Read, Edit | Read, Edit |
| Data Complete | Read | Read | Read | Read |
| Missing Data Message | Read | Read | Read | Read |

## Record-Level Access and Ownership

| Persona | Record Access | Ownership |
|---|---|---|
| Warehouse Associate | Access only to warehouse records needed for daily work. | Can own records they create, such as Stock Movement records. |
| Inventory Controller | Access to inventory, product, bin, and stock movement records needed for inventory control. | Can own Inventory Item and Stock Movement records they create. |
| Logistics Coordinator | Access to Shipment and Carrier Event records needed for logistics work. | Can own Shipment and Carrier Event records they create. |
| Operations Manager | Can view all warehouse and logistics records for oversight. | Can access records owned by users below them when required. |

## Security Approach

Object-level permissions control which project objects each persona can use.

Field-level security controls whether sensitive fields are visible or editable.

Record-level security controls which individual records each user can access. Organization-Wide Defaults, role hierarchy, and sharing rules can be used to provide the correct record access.

## Organization-Wide Defaults Decisions

| Object | OWD | Decision |
|---|---|---|
| Warehouse | Private | Private is used as the restrictive baseline. |
| Product | Private | Private is used as the restrictive baseline. |
| Stock Movement | Private | Private is used as the restrictive baseline. |
| Warehouse Shipment | Private | Private is used because shipment records should not be visible to all users by default. |
| Carrier Event | Private | Private is used because carrier event records are related to logistics activity and should be restricted. |
| Bin | Controlled by Parent | Deviation from Private because the data model supports inherited access from its parent. |
| Zone | Controlled by Parent | Deviation from Private because access is inherited from the parent record. |
| Inventory Item | Controlled by Parent | Deviation from Private because access is inherited from the parent record. |

## Record Sharing Decision

### Role Hierarchy
Operations Manager
- Warehouse Associate
- Inventory Controller
- Logistics Coordinator

The Operations Manager role is above the operational personas to reflect management access.

### Sharing Rule
Stock Movement records owned by users in the Warehouse Associate role are shared with users in the Inventory Controller role with Read/Write access.

This rule is needed because Stock Movement uses Private organization-wide defaults, while Inventory Controllers need access to review and update Stock Movement records created by Warehouse Associates.

Manual sharing and Apex managed sharing are not required because the declarative sharing rule meets the requirement.

| # | Test User | Test | Expected Result |
|---|---|---|---|
| 1 | Warehouse Associate | Open a Warehouse record | **Allowed – Read** |
| 2 | Warehouse Associate | Try to edit a Warehouse record | **DENIED** |
| 3 | Warehouse Associate | Create a Stock Movement | **Allowed** |
| 4 | Warehouse Associate | Try to delete a Stock Movement | **DENIED** |
| 5 | Warehouse Associate | Open Shipment Quantity and Status | **Visible but not editable** |
| 6 | Inventory Controller | Open Warehouse Associate-owned Stock Movement | **Allowed – Read/Write** |
| 7 | Inventory Controller | Try to delete that Stock Movement | **DENIED** |
| 8 | Inventory Controller | Try to edit Warehouse Shipment | **DENIED** |
| 9 | Logistics Coordinator | Create or edit a Warehouse Shipment | **Allowed** |
| 10 | Logistics Coordinator | Try to edit a Bin | **DENIED** |
| 11 | Logistics Coordinator | Try to edit Product | **DENIED** |
| 12 | Operations Manager | View records across the project objects | **Allowed – View All** |
| 13 | Operations Manager | Try to delete a Warehouse record | **DENIED** |
| 14 | Any test user | Open Reports/navigation | **Should only show/access what their permissions allow** |
## Access Matrix Test Results

| Test | Expected | Result |
|---|---|---|
| Warehouse Associate views own Warehouse | Allowed | PASS |
| Warehouse Associate edits Warehouse | Denied | PASS |
| Warehouse Associate creates Stock Movement | Allowed | PASS |
| Warehouse Associate edits/deletes Stock Movement | Denied | PASS |
| Inventory Controller accesses Warehouse Associate Stock Movement | Read/Write allowed | PASS |
| Inventory Controller edits Warehouse Shipment | Denied | PASS |
| Inventory Controller cannot see unrelated private Shipment | Denied | PASS |
| Bin calculated/sensitive fields remain read-only | Denied edit | PASS |
| Warehouse Associate opens Reports | Allowed | PASS |