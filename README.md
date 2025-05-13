
---

## 🌐 1. Use-Case Diagram

![Use-Case Diagram](docs/images/usecase.png)

Actors & UC’s:

- **User**: searchTrip, comparePrices, userBooking, getConfirmations  
- **TravelAgent**, **AffiliatePartner**, **Manager**, **SupportAgent** with their own UCs  

---

## ✏️ 2. User Stories

![User Stories – part 1](docs/images/userstories1.png)  
![User Stories – part 2](docs/images/userstories2.png)

Examples:

> **As a user**, I want to search for available trips so I can explore travel options.  
> **As an affiliate partner**, I want to promote offers and track referrals.  
> **As a system**, I want to integrate payment gateways, ensure uptime, and recover from failures.

---

## 📊 3. Domain Model

![Domain Model](docs/images/domainmodel.png)

Key entities:

- **User**, **TravelPortal**, **Trips**, **Booking**, **Payment**, **PriceCompare**, **BookingSummary**, …  
- Associations and inheritance (e.g. TravelPortal → Payment, Booking → Trips)

---

## 📐 4. Service Contracts (OCL)

### a) `SearchTripService::search(...)`

```ocl
Contract SearchTripService::search(
    destination:String,
    date:Date,
    travelers:Integer
) : Set(Trips) {
  definition:
    selectedTrips:Set(Trips) =
      Trips.allInstance()
           ->select(t | t.Destination = destination
                     and t.TripDate = date)
  precondition:
    destination <> "" and
    date <> null      and
    travelers > 0
  postcondition:
    result = selectedTrips
}
