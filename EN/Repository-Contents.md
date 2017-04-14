# Repository composition

## 1. Root Directory
This directory includes root documents related to the whole repository.

**/** root directory
 
**/AUTHORS** Authors information

**/COPYING** License information

**/DOCUMENTATION** Package usage information

**/README.md** Repository information and package compilation and installation

**/packages/bird-openwrt/** Packages' directory

## 2. Packages' Directory
This directory is a symlink to packages/bird-openwrt to facilitate the integration of any Pull Requests to the official *openwrt-routing* repository for Bird{4|6}-uci & bird{4|6}-luci packages.

**\*/bird4-openwrt** Bird4 UCI and LUCI packages' directory

**\*/bird6-openwrt** Bird6 UCI and LUCI packages' directory

## 3. Bird{4|6}-OpenWRT Package Directory

**\*/src/** Package's source directory

**\*/Makefile** Package's build & install recipe using `Make`

### 3.1 Source Directory

**\*/config/** UCI configuration directory

**\*/controller/** LUCI WebPages presentation controller directory

**\*/init.d/** Bird service handler directory

**\*/model/** LUCI configuration WebPages skeleton and functions directory

**\*/uci-defaults/** Installation/on-Boot time scripts directory

#### 3.1.1 Config Directory

**\*/bird{4|6}** Bird4/6 UCI configuration file (used by init.d scripts to create the bird-alike configuration)

#### 3.1.2 Controller Directory

**\*/bird{4|6}.lua** Bird4/6 Web configuration presentation controller (order of the tabs shown, which pages are shown, configuration handling functions...)

#### 3.1.3 Init.d Directory

**\*/bird{4|6}** Bird service handler (start, stop, restart and status). This script translates the UCI configuration in /config into Bird-alike configuration

**\*/bird{4|6}-lib.sh** Functions library file for /init.d/bird{4|6}. This script includes encapsulated functions to do the UCI to Bird-alike translation

#### 3.1.4 Model Directory
All Model LUA scripts are installed under /cbi/bird{4|6} folder and their function is to organise and represent the UCI configuration in a HTML Formulary.

**\*/bgp_proto.lua** BGP Protocol Web UI configuration

**\*/filters.lua** Bird's Filters files Web UI editing

**\*/functions.lua** Bird's Functions files Web UI editing

**\*/gen_proto.lua** Bird's main Protocols Web UI configuration

**\*/log.lua** Bird's Log file Web UI visualization (refreshed each 5 seconds)

**\*/overview.lua** Bird's general settings Web UI configuration

**\*/status.lua**  Bird service Web UI handling

#### 3.1.5 Uci-defaults Directory

**\*/99-relocate-filters** Script to be executed on installation time. This script will look for configured filters & functions in the UCI configuration and will move them to the +v0.3 default location. This script will remove itself after being executed

**\*/bird-uci-install-init.d** Script to be executed on installation time. This script will create a backup of the original Bird{4|6} init.d script and replace it with a link to our init.d version

#### 3.1.6 View Directory
This directory includes any HTML-Lua-JS template to be used by a script in the Model directory or to be called directly by a Controller

**\*/log.htm** Complete page with Auto-refresh configured for each 5 seconds to present the last 30 lines in the Log file for Bird.

**\*/tvalue.htm** Text Value template to be used in filters.lua and functions.lua to present file contents using a *Monospace*-like font. This is a copy of the default /view/cbi/tvalue.htm template.