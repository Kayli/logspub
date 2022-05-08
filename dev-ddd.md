# domain driven design notes

## basics

- entity
- repository
- bounded context (bc)


## examples of bcs and entities

- online conference management system 
  - conferences management: organizer, conference, seat, company, country, user, attendee
  - orders and registrations: conference, buyer, seat, attendee, order, reservation, seat assignment
  - pricing and marketing: conference, promotion, seat
  - payment: payer, payment, gateway
  - customer service: customer, return

- online casino
  - game
  - bonus
  - fraud
  - payment
  - security
  - back-office
