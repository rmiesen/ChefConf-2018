# VMware and Chef: What is the Ecosystem Like and Where Does Everything Fit?
Presenter: **JJ Asghar**, chef
 * Partner architect on the Technical Alliances team.
 * I own the major integrations with Chef and VMware
 * vEXPERT award awarded by VMware.

## Why Chef and VMware together
 * Provisioning and conf.
 * Patch and drift management.
 * Datacenter modernization.
 * Cloud infra migration
 * Compliance Auditing.
 * More dynamic vs. templates
   + IaC instead of heavy golden images.
 * Continual validation of the state of the node.
 * Your cookbooks and integrations work both on VMware on-premise and VMware on AWS.

## From Idea to Ship with Chef and VMware
 * ***FILL IN***

## Where does everything fit?
 * vRealize Orchestrator (VRO)
   + kitchen-vro
   + kitchen-vrealize
 * vRealize (VRA)
   + kitchen-vra
   + kitchen-vcenter
 * vCenter (uses SOAP API)
   + knife-vsphere
   + knife-vcenter
 * We can drive the VMware stack with the same tooling we drive other infra stacks.

## Infra automation driving your VMware Software Defined Data Center:
 * Three main integration points: knife-vcenter, kitchen-vcenter, and knife-vsphere.
 * The vcenter plugins work with AWS.
 * The VRA and VRO plugins have integration points from within VRA and VRO.
 * VRO is essentially a GUI version of knife.

## Three Best Practices
 * No chef-client in your VMware templates.
   + Use the VMware plugins instead to get chef-client on there
 * Using Terraform, vCenter, and Chef.
 * Use InSpec for both integration testing and Compliance Automation.

## Future Plans
 * InSpec profiles and demos validating.
   + ESXi: hypervisor configuration.
   + NSX: network configuration.
 * 6.7 vCenter validation.
 * Reference implementations of common VMware deployments integrated with Chef and InSpec.



## TODO:
 * Look into vSphere cloning API changes in 6.7.
