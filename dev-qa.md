# notes related to quality assurance practices in software

## clusters

- failure scenarios
  - more than half of the cluster nodes lose connection with the cluster, resulting in quorum loss
    - cluster recovery process may be involved
    - it better be automated and tested beforehand

- synthetic testing (synthetic monitoring, proactive monitoring)
  - is a method of understanding a user’s experience of your application
  - is a way to identify performance issues with key user journeys and application endpoints before they degrade user experience
  - connect to test servers (usually in different locations around the world) and use behavioral scripts to simulate the typical actions of end-users
