# domain driven design notes

## basics

- domain
- subdomain [^1]
  - core: provides competitive advantage for a company, has to be developed in-house
  - generic: no competitive advantage and high entry barrier, can reuse existing third-party solution
  - supporting: no competitive advantage and low entry barrier, can be outsourced
- bounded context (bc)
- entity
- repository

## examples of subdomains [^1]

- ticket sales and distribution company
  - core
    - recommendation engine
    - data anonymization
    - mobile app
  - generic
    - encryption of users data
    - accounting
    - payments
    - identity
  - supporting
    - integration with music streaming services
    - integration with social networks
    - attended events discovery module


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


## references

[^1]: https://www.amazon.ca/Learning-Domain-Driven-Design-Aligning-Architecture/dp/1098100131
