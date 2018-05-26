# Windows Automation with Chef Workshop
**Note:** Additional notes from the author can be found at <https://github.com/smurawski/chefconf2018>.
## Getting started
 * RDP information (for me):
   - Group 1: `cc2018.southcentralus.cloudapp.azure.com`
   - Port: `5000` + your assigned number
     + My number: 2
     + Port: `5002`
   - U/N: `ChefPowerShell`
   - P/W: `P2ssw0rd!`
 * Setup steps:
   1. Install chocolatey
   2. Setup developer Workstation
     - See <https://github.com/smurawski/chefconf2018>

## DevSec Windows Baseline compliance
 * Windows Baseline compliance profiles are provided as part of Chef Automate.
 
### Get your machine details
 * Open the kitchen file in your editor ( found in `<COOKBOOK_DIR>/.kitchen/default-windows-server-2016.yml`).
 * Grab the username / password / address

### View the DevSec Windows Baseline
 * <https://github.com/dev-sec/windows-baseline>
 
### Scan your machine w/ the Baseline InSpec profile
  * `inspec exec https://github.com/dev-sec/windows-baseline -t winrm://[username]@[host]`
    - Implication: This means we can put our DevSec stuff in a private GIT repo and dynamically pull that as part of a compliance run.
  * Note: your definition of "secure" will vary and should vary. If you blindly apply every recommended security setting, you'll have a nearly unusable system!


## Chocolatey
 * Traditional tools
   - Manual conf.
   - Golden images (aka. Sacred Cows).
   - Endpoint management tools.
   - None of these integrate with Configuration Management systems like Chef.
 * Modernizing automation:
   - Software management / package management systems account for 50% -- 90% of your automation.
   - Lots of variability in installing packages on Windows.
 * Chocolatey
   - Easy to manage software lifecycle
   - Universal format for managing all aspects of Windows software (msi, scripts, zips, binaries, etc).
   - PowerShell module simplifies work.
   - Packages are independent building blocks
   - Integrates with configuration management systems.
 * You write a software deployment once, then deploy it anywhere with everything, then manage and track that software over time (even without installers).
 * FOSS vs Chocolatey for Business (C4B)
   - FOSS == package management
     + Works well in org use
   - C4B == complete software management
     + Smother experience.
     + Builds on top of FOSS
     + Better GUIs
       * ChocolateyGUI.
         * Great for self-service Management (C4B).
 * Automatic uninstallation
   - Automatic uninstall of 80% -- 90% of packages.
 * Integrates with Everything
   - <https://chocolatey.org/docs/features-infrastructure-automation>
   - All major Configuration Management (CM) systems .
 * Inventory - Comprehensive Software Audits:
   - Tracks installation of all things installed...including at least some things not managed by  `choco list -lo ***FILL IN***`
   - Package Synchronizer (C4B): lists *all* packages installed...not just the ones managed by Chocolatey.
   - Compliance - audit out of date software: `choco outdated`.
 * Community Package Repository:
   - **Organizations should avoid**
     + Not fully reliable. Subject to distribution rights (download CDN cache features helps).
     + Trust and control.
 * Hosting our own package server
   - Artifactory Pro
   - Private Chocolatey server
   - There are others, but these two will do. :)
 * Creating Chocolatey Packages
   - Terminology: "Package" is nupkg file, "Software" is binaries or installers.
   - <https://chocolatey.org/docs/create-packages>
   - `choco new`
   - Package Builder (C4B) - "Generate software deployment packages in seconds".
     + Feed it a msi / exe / zip and it generates the package automatically...
       * Except for things like SQL Server. Those must still be done by hand (bet there's sources online that cover this too...)
     + Can convert existing packages to 100% offline and reliable packages.
 * How it works:
   + Package Synchronizer (Licensed) - Auto Sync
     - Choco maintains state based on packages. System states can be manipulated outside of chocolatey.
     - Any chocolatey command will trigger synchronization in licensed systems.
     - Other features
       * Great docs.
       * Internal sources (like ProGet)
       * `choco upgrade all` - Windows update for 3rd party and internal software.
       * Shimming.
       * Pass install arguments directly through to installers.
       * Package parameters to adjust logic in packages.
       * Handles locking on upgrades in package folders
       * Great reference docs: **FINISH**
       * (C4B)
         + Uninstall non-Chocolatey managed software
         + Direct installer
         + Runtime malware protection
         + CDN Cache
         + Professional Packaging Services.
         + Professional support.
 * Chocolatey Fest 2018: October 8th, one day, San Francisco.
   
## Using DSC resource in Chef recipes
 * DSC: **D**esired **S**tate **C**onfiguration
 * Starting with in-box resources
   + Just use the `dsc_resource`:
     ```ruby
     dsc_resource 'IIS' do
       resource :windowsfeature
       property :name, 'web-server'
     end
     ```
   + Advantage: Using chef resource makes DSC operations ordered.
 * Note: DSC is a "feature", not a "product".
 * Caveat: For "core" Microsoft services (SQL Server, IIS, etc), use DSC.
 * Counter-Caveat: If you can't test it, _it's not automated!_ Make sure you are testing for the intended state of the node post DSC.
 * Chef can provide the ecosystem that DSC needs.
   + Personal note: DSC seems out-classed by the likes of Chocolatey and unless DSC does more, I anticipate that Chocolatey will overtake and deprecate DSC within five years, especially with Microsoft now actively embracing Chocolatey.
 * Alternate resource: `windows_feature`
   + Is a core chef feature, supports arrays.
   + They are similar now.
   + `windows_feature` will get faster as PowerShell advances.
   

## Windows tips-and-tricks:
### Domain Joining
 * When should we do it?
   + Machine provisioning (aka: `sysprep`)?
   + Runtime (aka: `chef-client`)?
     + There's also `windows_ad_join` (name might not be exact).
   + Other options?
 * The answer: it depends on the context.
 * However, domain joining may be going the way of the dodo in the cloud, as domains don't handle cases where nodes are pulled in / out of domain frequently.
   + In short, think about why you are needing to join the domain, consider whether there is a real business need for it.

## Windows Updates
 * Short answer: Don't manager individual updates
 * Manage the update client
   + Windows update / WSUS have databases designed to do this.
   + WSUS: is a server.
   + Uses either a Windows internal database (if you're crazy) or a SQL Server.
   + Patching groups.
   + Approve patches.
   + Decline patches.
   + Look for Trevor Hess's GitHub page. He has a demo for how to setup WSUS server.

## Resources to know
 * `powershell_script`
 * `windows_package`
 * `dsc_resource`
 * `powershell_package`
 * `chocolatey_package`
 * `msu_package` (MSU == **M**icro**s**oft **U**pdate)

## Test Images and Tooling
 * Packer.
 * WSUS Offline Tool: <http://download.wsusoffline.net>
   + A utility for creating a big "iso" to use to patch a fleet of Win2k8 systems, create base images.
 * Existing Vagrant boxes.
   + Better than nothing, but not the image you deploy in production.
   + Reach out to Microsoft Cloud advocates.
     - Tweet at @WindowsServer.
 * Cloud providers.
 * VMware Templates.


## Misc notes
 * Do _not_ use `chef-client` to push individual windows patches: that's what WSUS (**W**indows **S**erver **U**pdate **S**ervice) is for. Use the appropriate resource for WSUS instead.
   - Relevant supermarket cookbooks:
     + <https://supermarket.chef.io/cookbooks/wsus-client>
     + <https://supermarket.chef.io/cookbooks/wsus-server>
 * Testing
   - As a rule, InSpec should come before chefspec, as chefspec doesn't test the state of the IUT (**I**tem **U**nder **T**est).
   - Cases where chefspec is useful:
     1. When you are writing custom resources.
     2. When you have complex recipes.
   - Chefspec uses "fohai" (Fake OHAI) data as part of it's mock chef runs.
   - In a nutshell:
     + ChefSpec: Tests to confrim that the _expected properties_ of a chef run are the ones that get returned.
     + InSpec: Tests to confirm that your chef-run actually runs as expected in the IUT.
 * Existing automation scripts can be copied and pasted into chef recipes.
   + That's perfectly OK, but you need to be sure you remain idempotent.
 * Look into the windows OHAI plugin. Profiles system, Windows features, stores it on Chef server.


## Questions:
 * Chocolatey:
   + I run into cases where using the `chocolatey` supermarket cookbook to install chocolatey where running the `chocolatey_package` resource fail in succeeding recipes. What is the proper way to install chocolatey if it's not installed the first time?
   + Why isn't Chocolatey installed as part of the `chef-client` installation?
     - **AR**: File a PR request against chefdk: it should.
   + Can I have the slides for the presentation?
