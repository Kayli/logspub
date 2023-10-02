# notes about software systems security and related stuff

## basics

- data breaches
  - unfortunate reality is that data breaches are a cost of doing business in the modern world 
    and will continue to be a concern to both companies and users

- zero-day
  - computer-software vulnerability previously unknown to those who should be interested in its mitigation
  - until the vulnerability is mitigated, hackers can exploit it to adversely affect programs, data, 
    additional computers or a network

- zero-day exploit 
  - an exploit directed at a zero-day is called a zero-day exploit, or zero-day attack

- malware
  - is any software intentionally designed to cause disruption to a target
  - typical targets: computer, server, client, computer network
  - typical goals: leak private information, gain unauthorized access to information or systems, 
    deprive users access to information or which unknowingly interferes with the user's computer 
    security and privacy

- worm
  - is a stand-alone malware
  - actively transmits itself over a network to infect other computers and can copy itself 
  - does not infect/damage files directly
  - almost always cause at least some harm to the network, even if only by consuming bandwidth
  - potentially marks attack surface of a target, likely a network

- virus
  - software usually hidden within another seemingly innocuous program 
  - can produce copies of itself and insert them into other programs or files
  - usually performs a harmful action

- shift left security practices
  - can significantly reduce the risk of releasing software with security vulnerabilities into production. 
  - helps to optimize the continuous delivery chain by making security part and parcel of the development process

- hard tokens: physical objects, used to grant access to a restricted digital asset
- soft tokens: pieces of software, used also grant access to digital assets


## penetration testing [2]

- basics
  - legal side of things is important, so learn more about that 
    - rules of engagement (RoE) document defines what is allowed during testing [1]

  - typical stages
    - planning, discovery, attack, reporting
    - incident response: containment, eradication & recovery

- attack methods [3]
  - ransomware: victim’s system is held hostage until they agree to pay a ransom to the attacker
  - web attacks
    - dos and ddos
    - man-in-the-middle
    - sql injection
    - xss
    - password
    - url interpretation
    - dns spoofing
    - session hijacking
  - brute force
  - insider threats
  - trojan horses: malicious program that is hidden inside a seemingly legitimate one
  - birthday: exploiting hash
  - cryptojacking
  - zero-day exploit
  - social engineering
    - phishing, whale-phishing
  
- levels of engagement with pentest team
  - white
  - gray
  - black: high risks of resources waste

- tools
  - scanning: nmap, nexpose 
  - jtripper
  - zenmap
  - searchsploit
  - wireshark
  - metasploit framework
    - https://docs.rapid7.com/metasploit/
    - projects with vulnerabilities
      - vulnerable linux vm built with vagrant https://github.com/rapid7/metasploitable3


## abbreviations

- waf: web application firewall


## references

[1]: https://hub.packtpub.com/penetration-testing-rules-of-engagement/
[2]: https://www.coursera.org/learn/ibm-penetration-testing-incident-response-forensics
[3]: https://www.fortinet.com/resources/cyberglossary/types-of-cyber-attacks
