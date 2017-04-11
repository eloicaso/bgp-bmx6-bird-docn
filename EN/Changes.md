# Changes between Bird-OpenWRT v0.2 and v0.3

`Latest update 11/04/17`

* Refreshed package and tested using Bird Daemon v1.6.3 and LEDE17.01-RC1
   * Apply standardised code style (i.e. ${variable} or $(_command_))
   * Added Filters and Functions folders (/etc/bird\*/{filters|functions}) and create an upgrade path for v0.2 users
   * Fix some bugs from v0.2
   * Re-added Pipe and Direct protocol functions
   * Removed hardcoded references to Bird4/Bird6 and unified (where possible) using variables
   * Some enhancements in Makefile (i.e. Preserve configuration on sysupgrade)
   * Aligned Bird4 and Bird6 code (pending: finish and align OSPF Protocol)
* Changes in UCI's config (/etc/config/bird\*)
  * Removed non-critical configuration used as an example in the previous version
  * Added base configuration in bird6 (Router\_ID _0xCAFEBABE_)
* Changes in Service script (/etc/init.d/bird\*)
  * Detached UCI transformation functions into a separate script (bird\*-lib.sh) to simplify init.d script and move forward possible future automated tests
  * Switched from service commands to background bird\* binary calls
     * Service calls were not returning exit code
     * Service calls were not returning stdout/stderr
     * Bird binaries allow fine-grained configuration (i.e. specify PID\_file or LOG\_file) and to be ran in background
  * Added an error control system to improve customer's feedback and service handling
  * Created a temporary Bird configuration backup (re-generated each service start)
  * Added Status function to return Bird service's current state
  * Added _quiet_ service handling functions to execute _start/stop/restart/status_ functions with no Terminal highlighting (used in LUCI Web calls)
     * Functions are named "service\_quiet"
* Changes in LUCI scritps (Web Configuration Interface)
   * Updated controller scripts
      * Updated script and re-sorted
      * Added Status, Log, Filters and Functions tabs
    * Status Page
      * Present Service Bird\* _status_ text (using status_quiet)
      * Present Service Bird\* _start/restart/stop_ buttons (using \*\_quiet)
    * Log Page `(Work In Progress)`
      * Present configured Bird\* Log file. Auto-refresh each 5 seconds
    * Filters & Functions Page `(Work In Progress)`
      * Allow selecting a file under /etc/bird\*/{filters OR functions}/ or create a new one using current Time
      * Load selected File in a Text Box and allow editing it
      * Save changes in the file
