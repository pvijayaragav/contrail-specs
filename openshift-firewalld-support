# 1. Introduction
  Openshift installs Contrail components on the master infra and compute nodes. 
For contrail services to work the iptables should not block the ports where our
services are running. 

# 2. Problem statement
#### Provide registered blueprint URL for this feature
#### Blueprint must provide a brief description of the problem being solved
  Today in openshift we open up all contrail service ports using
the native "iptables" tool in the kernel. We do this by setting an ENV variable 
called CONFIGURE_IPTABLES in our init container, since we run our init container
before all our actual service containers. We get the chain where the iptable rule
has to be created from a ENV called IPTABLES_CHAIN and the contrail service name
from NODE_TYPE and configure the iptables accordingly. We dont support firewalld,
however openshift support firewall configurations through firewalld. We need to 
use firewalld to open up contrail service ports on the hosts.

# 3. Proposed solution
#### Describe the proposed solution

  Implement a similar functionality for firewalld to open up ports and configure 
firewall.
1. define a ENV, say CONFIGURE_FIREWALLD 
2. define a ENV for chain, say FIREWALLD_CHAIN
Get the zone / chain information from Openshift manifest and populate above ENVs

# 4. Alternatives considered
#### Describe pros and cons of alternatives considered
1. Since firewalld is internally implemented using iptables, we can consider 
directly configuring the iptables, but customers wont have control. 
Hence we are proceeding with configuring the firewall using firewalld

# 5. API schema changes
#### Describe api schema changes and impact to REST APIs
NA

# 6. UI changes
#### Describe any UI change applicable to this feature
#### Modifications to existing UI work flow with appropriate justifications
NA

# 7. Notification impact
#### Describe any log, UVE, alarm changes
#### Describe all new elements added as part of this feature
NA

# 8. Provisioning changes
#### Describe how this feature will be automatically provisioned
#### Describe all applicable envs like Kubernetes, RHOSP, JuJu, openshift, etc.
#### Describe any change to notifications provided to client systems
No changes will be provided by user, user simply specifies openshift_use_firewalld 
in their inventory file and we will act up on that flag and input the desired
ENVs variables into our containers through the manifests

# 9. Implementation
#### Describe changes in all affected components such as controller, agent, etc.
#### Describe all data model schema changes applicable to this feature
#### Describe changes to key data structures
#### Describe synchronous/asynchronous nature of any API calls being made if any
#### Describe the impact on the feature during process restart if any
#### Describe all logs and debug messages associated with this feature
#### Describe all high availability considerations
Changes in only the node-init container, which does not impact other installations

# 10. Performance and scaling impact
#### API and control plane
#### Scaling and performance for API and control plane
#### Scaling and performance for API and forwarding
NA

# 11. Upgrade
#### Describe upgrade impact of the feature, including ISSU
#### Schema migration/transition
NA

# 12. Deprecations
#### If this feature deprecates any older feature or API then list it here
NA

# 13. Dependencies
#### Describe dependent features or components
#### Describe any new infrastructure component required
NA

# 14. Testing
#### Unit tests
#### Dev tests
#### System tests
1. ut should include installing contrail and checking if the corresponding
iptables and firewalld rules are created.
2. all pods should be created and pods should be in ready/running state

# 15. Documentation Impact
NA

# 16. References
NA
