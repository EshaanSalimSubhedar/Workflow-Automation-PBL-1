# Assignment 2 — Logistics & Shipment Exception Management

## Scope
Start: shipper books a shipment. End: shipment is delivered and closed, returned to sender, cancelled, or declared lost.

## Participants / lanes
Shipper / Customer; Control Tower / Dispatcher; Pickup Agent; Hub / Warehouse; Delivery Agent; Recipient; Claims Department.

## Main sequence (happy path)
1. **User Task:** Create shipment booking.
2. **Business Rule Task:** Validate address, weight, service level; calculate charges.
3. **Service Task:** Schedule pickup and assign driver.
4. **User/Manual Task:** Collect parcel and scan it.
5. **Parallel Gateway (split):** parcel movement; tracking update and shipper notification.
6. **Parallel Gateway (join):** wait for both branches.
7. **Sub-process:** hub sorting/scanning and line-haul transit (repeat per leg).
8. **Send Task:** notify recipient that parcel is out for delivery.
9. **User Task:** deliver parcel and capture proof of delivery.
10. **Service Task:** close shipment and generate invoice.
11. **End Event:** Shipment Delivered.

## Gateway conditions
- **Exclusive:** valid booking? insured damage? delivered / refused / COD failed? address surcharge required?
- **Parallel:** movement and tracking run concurrently; join before downstream handling.
- **Event-based:** after dispatch, wait for a delay message or a timer; whichever event occurs first determines the next action.

## Intermediate events and boundary events
- **Timer:** no scan for 48 hours starts tracing; five-day tracing limit declares lost; customs documents have a five-day deadline; depot hold lasts seven days.
- **Error boundary:** scanner or tracking update fails; supervisor enters the scan manually and reconciliation follows.
- **Message boundary:** shipper cancels while parcel is in transit; stop movement and start return/compensation.
- **Message intermediate events:** request missing customs documents and wait for the shipper's response.
- **Escalation:** pickup or tracing exception exceeds its retry/time limit.

## Critical path
Booking → validation → pickup scheduling → pickup/scan → parallel transit and tracking → hub processing → out-for-delivery notification → delivery/proof → close/invoice → delivered.

## Alternate paths
- Invalid booking details: return to shipper for correction, then revalidate.
- Pickup failed: reschedule twice; if still unsuccessful, cancel and apply cancellation fee.
- Damage: inspect; if insured, route to claims/refund/replacement/reshipment; otherwise record and notify shipper.
- Lost: no scan for 48 hours → trace → if still missing after five days, declare lost and compensate.
- Transit delay: timer/message event → notify customer → reroute or assign alternate vehicle and update ETA.
- Customs hold: request documents; if not supplied within five days, return to origin.
- Recipient unavailable: up to three attempts → depot hold for seven days → return to sender.
- Refusal/COD failure: return to sender and adjust charges.
- Scan-system error: manual correction → reconciliation.
- Cancellation in transit: stop movement → return parcel → refund less applicable fee.

## Modeling checks
- Label all gateway branches with conditions.
- Use a parallel join only when both parallel branches are expected to complete.
- Attach boundary events to the correct activity or sub-process.
- Give every retry a limit and each terminal outcome a clear end event.
