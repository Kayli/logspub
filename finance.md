# self-paced course notes about finance


## roles of banks 

- for average joe
  - safety and security of storing liquid assets
  - simplification and digitalization of money exchange function
  - getting loans for buying real estate and goods

- for government
  - assessing credibility of potential borrowers
  - generation of new money surplus from loans


## top banks

- canadian big five
  - royal bank of canada (rbc)                assets: 825b
  - toronto-dominion bank (td)                assets: 811b
  - bank of nova scotia (scotiabank)          assets: 744b
  - bank of montreal (bmo)                    assets: 542b
  - canadian imperial bank of commerce (cibc) assets: 352b

- usa top six
  - JPMorgan Chase	            assets: $3,025b	cap: $401.24b
  - Bank of America	            assets:	$2,259b cap: $267.66b
  - Wells Fargo	San Francisco   assets:	$1,768b cap: $130.04b
  - Citigroup		                assets: $1,662b cap: $126.81b
  - Goldman Sachs		            assets: $1,163b	cap: $96.95b
  - Morgan Stanley		          assets: $1,115b	cap: $128.81b


## taxes

- citizens of canada pay taxes 3 times:
  - income tax
  - sales tax (except for basic food)
  - inflation
    - when government prints more money
    - when banks lend money


## verification

- canadian financial business services registry: fintrac
  - search by name https://www10.fintrac-canafe.gc.ca/msb-esm/public/msb-search/search-by-name/
- search for a federal corporation
  - https://www.ic.gc.ca/app/scr/cc/CorporationsCanada/fdrlCrpSrch.html


## currrency exchanges

- in-branch: negotiate rate
- offline: vbce, charlies
- online
  - www.knightsbridgefx.com (verified by fintrac)
    - takes up to 5 days for combination of withdrawal, exchange, deposit operations


## canadian savings accounts

- example scenario: say, we earned 10k somehow
  - and we are in a 30% tax bracket
  - and we deposit money for n years 
  - and it grows in total +50% for these n years
  - in one of 3 following types of accounts
    - rrsp account
      - invested 10k which resulted in 15k before taxes in the end
      - totals to 10.5k after taxes
      - but
        - subtract 50 cad for every withdrawal
        - withdrawals can’t be more than 5k cad/month (4k usd before tax, 3.6k usd after tax)
      - so in fact you can withdraw only 10.35k and only after 3 months
        - if case you want to minimize fees

    - tfsa account
      - paid taxes so that 7k left
      - invested 7k
      - got non-taxable income 3.5k
      - totals to 10.5k after taxes in the end

    - regular investment account
      - paid taxes so that 7k left
      - invested 7k
      - got taxable income 3.5k in the end
      - totals to 9.45k after taxes
    
  - todo: create graphs showing dynamics depending on
    - how long you hold on your investment
    - how much money you initially invested


## investment funds

- see <repo>/notes/investments.md


## online banking aspects to be careful with

- digital log as well as paper copy should be always available for all actions performed online
  - whenever its not possible: printing pages, taking screenshots, recording video is necessary
  - never subscribe for paperless option
    - there will be a 'software glitch' as they will frame it, and you wont be able to prove anything

- posted limit orders should be available in a log
  - verify that original price specified is there
  - when not available (rbc), make sure to record a video of placing the order

- avoid dealing with currency exchanges, unless absolutely necessary
  - rate negotiation process is not transparent and designed to rob or humiliate customers


## security measures

- record all phone conversations
  - don't use call recorder apps, as they may proxy your call and record elsewhere
    - basically overhearing all your communication
    - if they're doing it, they should pay for it, not me
  - ideally, solder your own splitter device for recording, it shouldn't be that complicated
  - store recordings in multiple (a couple) legit places
    - certified cloud (google, apple)
    - physical device (sony recorder)

- consider going to physical rbc branch for any kind of inquiry
  - use machines offered by bank
    - atms are okay for basic needs
    - ask if computers are offered for public use within a branch
    - you can't be certain about your isp, dns spoofing may take place, who knows what else
  - even if you just want to make a call to representative
    - as your security questions/answers may be overheard by neibourgs
      - its a reasonable concern
        - as i have no idea about who lives behind the wall
        - or who visited them recently, etc

- don't enter rbc credentials on third-party websites (duh)
  - not through 'iframe' not even through 'redirect to a trusted rbc domain' methods
    - unless its "trusted partner sign-in" (just two: cra or interac atm)
    - because otherwise rbc is not responsible for consequences


## questions to sort out

- how to fingerprint a recording on a device?
  - so that in a case of official investigation recording is considered a legit evidence
  - i should probably call vancouver police investigations department representative or something like that
    - to get official information on that topic


## rbc sketchy practices and things to improve

- front-running unethical practices are legitimized by the agreement 
  - personal trading (clause 5): representatives of RBC Direct Investing may have access to confidential 
    information regarding the trading activities of any client which such representative may use for 
    their own personal trading purposes, with a potential detriment to the client such as through placing 
    trades ahead of client trades (i.e. front-running)
  - https://www.rbcdirectinvesting.com/einserts/202103/DIREMAR2021.pdf
    - stored a copy in my cloud

- there is no "free text search" functionality over all transactions for my accounts
  - for example, i can't easily find all transactions charged by "the great courses" teaching company
- there are no transactions data prior to Aug 2014, need to explicitly request it
  - most likely because of 7 years data retention policy (are they trying to save on disk space or what?)
- last downloadable main account statement is
  - using ordinary interface
    - "account services" -> "download transactions" page
      - allows to downloading only last 30 records in csv format for main account
      - but interface looks like its about to download all available ones on file
    - "your documents" -> "account documents" page (new)
      - supposed to replace old "View and Manage Documents"
      - allows downloading statements starting August 2014 for both mastercard and main accounts

  - using "View and Manage Documents" page, "Search eDocuments" section
    - page considered to be obsolete, but somehow i can still navigate to it from main site
    - earliest are nov and december statements for 2016
    - there are only 2 statements for 2016
    - there are no statements for 2014, 2015
    - data for earlier years is not even accessable using ebanking interface
- they don't accept requests for paper copies via message center (secure message feature)
  - insist on visiting branch in-person
- multiple domain names showing same page
  - https://www.rbcroyalbank.com/personal.html
  - https://www1.royalbank.com/cgi-bin/rbaccess ....
  - despite the fact they've confirmed both domain names, it was only in their 'secure message' mode
    - which is bs, no copies of the messages are sent to email
      - so i have to print them manually or something
  - csr agent Daniel created ticket PER-39232535 to track the issue
    - on July 4, csr agent Jodie said 
      - 'you can also enter rbconlinebanking.com' to directly access the online sign in page'
      - however, she was very imprecise regarding which domain names i can use to sign in, i should re-
      confirm once again
- there is no free text search filter criteria in etf screener
  - but you can achieve similar results by clicking "show all results" after entering criteria in top right corner
  - this is a usability bug: there are no immediately visible references to this search page in UI
      
## terminology

- revolver [^1]
  - is a borrower who carries a balance from month to month, via a revolving credit line
  - can be an individual or a company


## references

[^1]: https://www.investopedia.com/terms/r/revolver.asp
