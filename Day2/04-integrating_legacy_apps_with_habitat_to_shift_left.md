# Use Habitat to "Shift Left" Legacy and Corporate Applications

## Motivation
* Consolidation. Habitat allows for one build of an app to deploy in multiple environments.


## Facts and Myths:
 * Myth: There are no changes at all.
   + However, it is possible to make only a few changes to a system and slowly shift a legacy system left.

## Example Application
"Scalable Low-latency Asynchronous Communication" (SLACK)
 * IRC
 * HTML5 / CSS3
 * Yarn
 * React
 * Go language
 * Web sockets
 * PubSub
 * RethinkDB
 

## Goals for "Shifting Left"
 * What is the **Least disruptive** route we can take to ensure
  * Success
  * **`***GET FROM NOTES***`**
 
## Keys to successful migration
 * Bi-Directional Service Discovery.
 * Service discovery: 2 perspectives
   + Onsite the habitat cluster (new)
   + Outside the Habitat cluster
     - Can't take advantage of proxy service
     - **`***FINISH***`**
 * Habitat service discovery (inside habitat)
   + Habitat Supervisor Ring.
   + `hab svc load myorigin/myapp --bind foo:foo.default`
 * Habitat service discovery (outside habitat)
   + Habitat needs to talk to legacy nodes
   + Legacy nodes need to talk to habitat.
   + Method 1: Service Proxy (Habitat service Proxy Pattern)
     - Deploy a special application (service proxy) that sits in a while loop and sleeps. This service loads a configuration into the service ring that makes the legacy apps available to other Habitat applications.
     - Habitat Consumers / Producers:
       * API has a port and a secret. Database has a driver port.
     - One can instead of deploying full apps deploy wrappers to legacy apps.
       * **`***COMMAND GOES HERE***`**
     - Outcomes
       * Direct control of service registration.
       * Inflexible with regard to change.
       * One way.
   + Method 2: Consul Integration
     - Take traditional infrastructure and add it all to consul.
     - Deploy into habitat deployment a consul proxy, have it reach out to consul to get service discovery information.
   
   
## Mixing solutions:
 * Plans (Bindings are optional)

## Questions:
 * Can I have a copy of your slides?
   + Give presenter email later (maybe).
   + <http://github.com/predominant/slacker-api>
   + <http://github.com/predominant/slacker-ui>
