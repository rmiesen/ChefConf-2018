# Keynotes
## Choir! Choir! Choir!
Summary: Someone at Chef Software thought it would be a really neat idea to have an unannounced hour long group Karaoke session at 8:30 in the morning. It wasn't.


## Serving up Containers using Chef
**Arun Gupta:** Principal Open Source Technologist, Amazon Web Services.

 * Containers make it easy to build, deploy, and scale apps.
 * Amazon Container SErvices:
   + Amazon ECS.
   + Amazon EKS (limited preview)
   + AWS Fargate (they just run your containers for you w/o you worrying about the Docker infrastructure)
 * Amazon EKS
   + Managed masters
   + Highly available
   + Auto upgrades
   + BYO Workers (Docker images) (AWS provides Packer scripts)
 * kops: CLI for deploying a Kubernetes cluster to AWS.
 * Chef Control Plane
   + EC2 instances, containers are bootstrapped by this control plane.

### Compliance of Nodes in a Kubernetes Cluster
 1. Launch Chef Server.
 2. Launch Kubernetes Server, bootstrap worker nodes to Chef Server.
 3. Run Compliance Profile.
