# 📖 BookMyTrip

A lightweight prototype of an online travel portal—search for trips, compare prices, book & pay, and retrieve confirmations—all under clean service contracts with automatic pre- and post-condition checks.

---

## 🚀 Table of Contents

1. [Use-Case Diagram](#1-use-case-diagram)  
2. [User Stories](#2-user-stories)  
3. [Domain Model](#3-domain-model)  
4. [Sequence Diagrams](#4-sequence-diagrams)  
5. [Service Contracts (OCL)](#5-service-contracts-ocl)  
6. [Validation](#6-validation)  

---

## 🌐 1. Use-Case Diagram

![Use-Case Diagram](docs/images/usecase.png)

**Actors & Use-Cases**  
- **User**: `searchTrip`, `comparePrices`, `userBooking`, `getConfirmations`  
- **TravelAgent**, **AffiliatePartner**, **Manager**, **SupportAgent** each have their own specialized UCs  

---

## ✏️ 2. User Stories

![User Stories – part 1](docs/images/UserStories1.png)  
![User Stories – part 2](docs/images/UserStories2.png)

**Examples**  
> **As a user**, I want to search for available trips so I can explore travel options.  
> **As an affiliate partner**, I want to promote offers and track referrals.  
> **As a system**, I want to integrate payment gateways, ensure uptime, and recover from failures.

---

## 📊 3. Domain Model

![Domain Model](docs/images/ConceptualClassDiagram.png)

**Key Entities**  
- **User**, **TravelPortal**, **Trips**, **Booking**, **Payment**, **PriceCompare**, **BookingSummary**, ...  
- Rich associations & inheritance (e.g. `TravelPortal → Payment`, `Booking → Trips`)

---

## 🎞 4. Sequence Diagrams

1. **Search Trip**  
   ![Search Trip Sequence](docs/images/Seq1.png)

2. **Compare Prices**  
   ![Compare Prices Sequence](docs/images/seq2.png)

3. **User Booking**  
   ![User Booking Sequence](docs/images/seq3.png)

---

## 📐 5. Service Contracts (OCL)

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

``` 
---


## 🛡️ 6. Validation

1. **Initial State**  
   ![Validation – initial blank](docs/images/Validation1.png)  
   At startup, all input fields are empty, no trips are listed, and the precondition panel shows green (`true`), since by default `destination <> "" and date <> null and travelers > 0` isn’t yet evaluated.

2. **Valid Input**  
   ![Validation – success](docs/images/Validation2.png)  
   When you enter a non-empty destination, a valid date, and a positive traveler count, the search operation runs successfully: the precondition and postcondition panels stay green and the matching trips (if any) would appear in the table.

3. **Invalid Input**  
   ![Validation – failure](docs/images/Validation3.png)  
   If any input fails the precondition (e.g. empty destination), the precondition panel turns red and a warning dialog pops up (“Precondition is not satisfied”), preventing the operation from executing.

