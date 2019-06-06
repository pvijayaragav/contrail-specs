# 1. Introduction

  Openshift installs Contrail components on the master infra and compute nodes. 
For contrail services to work the iptables should not block the ports where our
services are running. 

# 2. Problem statement

  Today in openshift we open up all contrail service ports using
the native "iptables" tool in the kernel. We do this by setting an ENV variable 
called CONFIGURE_IPTABLES in our init container, since we run our init container
before all our actual service containers. We get the chain where the iptable rule
has to be created from a ENV called IPTABLES_CHAIN and the contrail service name
from NODE_TYPE and configure the iptables accordingly. We dont support firewalld,
however openshift support firewall configurations through firewalld. We need to 
use firewalld to open up contrail service ports on the hosts.

# 3. Proposed solution

  Implement a similar functionality for firewalld to open up ports and configure 
firewall.
1. define a ENV, say CONFIGURE_FIREWALLD 
2. define a ENV for chain, say FIREWALLD_CHAIN
Get the zone / chain information from Openshift manifest and populate above ENVs

# 4. Alternatives considered

1. Since firewalld is internally implemented using iptables, we can consider 
directly configuring the iptables, but customers wont have control. 
Hence we are proceeding with configuring the firewall using firewalld

# 5. API schema changes

NA

# 6. UI changes

NA

# 7. Notification impact

NA

# 8. Provisioning changes

No changes will be provided by user, user simply specifies openshift_use_firewalld 
in their inventory file and we will act up on that flag and input the desired
ENVs variables into our containers through the manifests

# 9. Implementation
Changes in only the node-init container, which does not impact other installations

# 10. Performance and scaling impact

NA

# 11. Upgrade

NA

# 12. Deprecations

NA

# 13. Dependencies

NA

# 14. Testing

1. ut should include installing contrail and checking if the corresponding
iptables and firewalld rules are created.
2. all pods should be created and pods should be in ready/running state

# 15. Documentation Impact
NA

# 16. References
NA
