# Building and Running ASP.NET Applications in Habitat
**Matt Wrok:** Chef.

## Scope of app
 * IIS.
 * SQL Server backend.
 * All software requirements installed automatically.
 * Deployed to Containers.


## URLs of Interest:
 * <https://www.habitat.sh/>
   + Docs
   + Tutorials
   + Builder
 * Our ASP.net plan:
   + <https://github.com/habitat-sh/habitat-aspnet-eff
 * Running Habitat as a service:
   + <https://github.com/habitat-sh/windows-service>
 * SQL Server plan:
   + In core habitat plans (GitHub)


## Installing Habitat on Windows
 * `choco install habitat`
 * There's also the installer on the habitat website.

## Sample app:
 * Microsoft's Entity Framework sample application from the MS Code Samples site.
 * Build mechanisms: nuget and msbuild.
   + nuget:   installed as a build dependency.
   + msbuild: installed via nuget.
   + Invocation: the same as by hand or by script.
   + Build using the "webPublish" configuration to publish it to a variable: `$pkg_prefix/www/`
   + IIS installation / configuration: baked into Windows OS. Needs to be turned on by using DSC and associated chef resources.
     - Need to add a package dependency to `$pkg_deps` called `core/dsc-core`.
     - All the application pool configuration is also handled via similar deterministic configuration mechanisms.
     - Use PowerShell Core to bundle the exact version of PowerShell your Habitat scripts will run against.
   + .NET installation: treat it as a piece of infrastructure, leave it for things like chef to handle installation of that prerequesite.
 * Build steps: findable on <http://www.habitat.sh>.
 * Deploying: also findable on <http://www.habitat.sh>.
   


# Misc.
 * Handling Windows Features that require a reboot:
   + Handle it in the provisioning 
 * "AE DEBUG": Popup box of death killer.
   + Look at:
     - <https://madvirtualizer.wordpress.com/tag/aedebug/>
     - <https://msdn.microsoft.com/en-us/library/windows/desktop/ff406271(v=vs.85).aspx>
     - <https://msdn.microsoft.com/en-us/library/windows/desktop/dd744765(v=vs.85).aspx>
     - <https://answers.microsoft.com/en-us/windows/forum/windows_7-performance/disabling-applicationexe-not-responding-dialog/6cabdc8c-b68b-4cdb-8e77-b874401ccc95>


## Questions
 * How can one run (1) test suites, (2) regression test suites, (3) security scans (example: klocwork, coverity, protex)?
   + Use "build callbacks" to invoke unit tests, regression test suites. Failures == fail the build.
   + There are also test hooks that can be used as well.
 * Can one run different classes of "releases" (aka. a "nightly" release only runs the test suite, "release candidate" runs all of the above)?"
   + Achievable via a combination of habitat configurations.
