# notes about software systems security and related stuff

## basics

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


## penetration testing [^2]

- basics
  - legal side of things is important, so learn more about that 
    - rules of engagement (RoE) document defines what is allowed during testing [^1]

  - typical stages
    - planning, discovery, attack, reporting
    - incident response: containment, eradication & recovery

- attack methods [^3]
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

[^1]: https://hub.packtpub.com/penetration-testing-rules-of-engagement/
[^2]: https://www.coursera.org/learn/ibm-penetration-testing-incident-response-forensics
[^3]: https://www.fortinet.com/resources/cyberglossary/types-of-cyber-attacks
