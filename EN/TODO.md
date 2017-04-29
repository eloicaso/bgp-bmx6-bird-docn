# List of future "Should"/"Would-Like"s to re-factor or improve current bird\*-uci and luci-app-bird\*.
> Caution: this is not a priority list and it has not been sorted in any way to show preference or feasibility to be done.

1. Switch all LUCI strings into "translate" entities
2. Re-factor LUCI pages into LUCI tabs in order to make it easier to use XHR.Poll or XHR.Get (i.e. openVPN & privoxy)
3. Re-factor LUCI Status page to make it simpler and visual following "openVPN" approach
4. Add all the missing non-critical properties/attributes for each protocol
5. Verify correctness of current OSPF configuration. Add any critical property/attribute and align this configuration with bird6-uci and luci-app-bird6
6. Log File Page should show a textbox to select how often the page is refreshed.
7. BGP Instances must have all the properties as optional and let BGP Template populate them. Add a strong WARNING to admins that if they do not configure a template, they are forced to set all the settings appropiately.
