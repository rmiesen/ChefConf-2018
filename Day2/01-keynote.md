# Keynote presentations
## Opening presentation
**Presenter:** Barry Crist, CEO of Chef.


 * Enterprise Paradox: 90% have identified Automation, DevOps, and agile practices as critical to the business, yet <15% have done so.
 * Digital transformation: going from infra-centric to app-centric; Enterprise to FAANG (Facebook Apple Amazon Netflix Google).
 * Method: Act like a Digital Native.
   + A customer shouldn't be able to tell if you were a digital company or a "traditional" company.


### IT: Acting like a Digital Native
 * Bring organizational confidence.


### Digital Natives:
 * Deliver effortless infrastructure to app teams w/ automation (immediate, scalable, secure).
 * Ruthlessly eliminate all velocity obstacles.
   + Compliance is a velocity problem.
   + Solve compliance tool fatigue by shifting left.
 * One way to build, deploy, and manage all applications.
   + Biggest divide between FAANG vs the Enterprise.
   + Enterprise stumbling blocks:
     - COTS (**C**ommercial **O**ff **T**he **S**helf software)
     - Legacy
   + One path vs. a thousand paths.


### Chef Software's Ambition
 * Our platform is the single way to build, deploy, and manage all software in all environments.
 * Legacy, COTS, Containers, Kubernetes---all of it.


## How to transform a company to a Digital Native company
**Cory Scobie:** Senior VP of Products and Engineering.

 * Two facets: Scaleability and Repeatability.

### Progress (on Chef)
 * Continuous automation.
 * Effortless infrastructure.
 * Any app, anywhere.
 * Chef Automate is designed to help companies get there.

### Principles
 * Smaller, more atomic.
   + Developers can make a single change in a line of code and then watch it ripple through the build, validation, and deployment process.
 * Isolation.
   + The more a change can be isolated, the more confident we can be in a change's validity, stability, and sanity.
   + One change at a time.
 * Velocity
   + Change to operationalizability (DevOps).
   + Gating function: the Latency in the development pipelines.

## Chef Automate Demo notes
### Presenters:
 * **Nell Shamrell-Harrington:** Senior Software Development Engineer, core development on Habitat.
 * **Mike Krasnow:** Product Manager, Infrastructure Automation.

### Pieces of Chef
 * Habitat Plan
   + Policyfile is the artifact
   + Chef Client is a dependency.
   + run_list
     - DevSec Linux Baseline Scan.

### Big changes in Chef Automate 2.0
 * <http://automate.chef.io>
 * Habitat is now a central build system.
 * It is now possible ot use Habitat and Policyfiles to setup a CI/CD system for infrastructure.
 * It is possible to "Detect and Correct" nodes out of compliance, sync, or otherwise broken.

### Major Features
 * Actionable insights and operational visibility.
 * Scan and report on compliance in any environment.
 * Re-architected for speeed and flexibility.

### Habitat
 * On-premises depot
   + Note taker's opinion:
     - Could be _very useful_for replacing legacy build systems.
     - Could even potentially supercede and replace systems like Jenkins for CI/CD...without the baggage and grief that comes with it!
     - However, a POC needs to be done first.
 * Kubernetes operator.
 * Export to Azure and Helm
 * Open service broker.
 * Splunk.

#### Demo
 * (notes added to previous section).

### Chef Workstation Beta
 * New desktop experience for Chef.
 * Ad-hoc tasks in infrastructure made easy.
 * Makes it easier to get started with Chef
 * <http://www.chef.sh>


#### New features:
**Seth Thomas:** Senior Community Engineer.

 * Ad-hoc tasks:
   + Ad-hoc execution of resoruces and recipes.
   * Called "chf-run".
   + Run ad-hoc resources: `chef -run rhel-01 package ntp action=install`
     - rhel-01 is a node that already exists, but doesn't have to be part of a chef server.
     - Uses Policyfiles (silently).
   + Apply cookbook: `chef-run rhel-01 deploy_website`
     - `deploy_website` is a cookbook (uses the "default" recipe)
   + Apply cookbook to multiple nodes: `chef-run rhel-0[1:3] deploy_website`
     - Tasks are executed in parallel.

### Time is precious:
 * The goal is to speed up infrastructure and development tasks.
   + Instead of weeks and days, it should take hours, minutes, and seconds.

### Continuous Automation:
 * The key to shifting left.
 * Application as the unit of deployment is a _game changer_.

## Do Change
**Jeremy Winter:** Partner Director of Program Management, Microsoft.

### Habitat in Azure
 * Azure: Productive + Hybrid + Intelligent + Trusted.
   + Hybrid: Support for diverse cloud, legacy environments.
 * Azure Kubernetes Service (AKS)
   + Fully managed Kubernetes orchestration service.
   + Auto patching, auto scaling, auto updates.
   + Use  the full Kubernetes ecosystem.
 * Habitat walkthrough:
   + Start with either `hab init` or a Visual Studio plugin to scaffold out a Habitat configuration file (called a "plan").
     - See <https://www.habitat.sh/docs/glossary/#glossary-scaffolding> and <https://www.habitat.sh/tutorials/sample-app/mac/> for examples, more details.
   + Build the Habitat package and upload it to the on-premises enterprise server or public FOSS (not for Enterprise, obviously), then deploy it to Azure as a container (or anything else really)
 * Azure cloud shell: contains a lot of developer tools and the azure CLI (azcli). Now ships with InSpec.

### Advice:
> (About change) "Stagnation is more dangerous than change." (printed out on a color dot matrix printer by a departing Microsoft manager in 2008).

#### Questions:
 * For Habitat: what about running test suites and validation suites as part of Habitat? Is that possible?
 * For ad-hoc automation: is it possible to automatically create new infrastructure ad-hoc too?
   + Answer: not yet, but it is very likely that such ad-hoc infrastructure creation---called "orchestration"---will be added to a later version of Chef Automate.
