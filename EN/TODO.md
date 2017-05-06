# List of future "Should"/"Would-Like"s to re-factor or improve current bird\*-uci and luci-app-bird\*.
> Caution: this is not a priority list and it has not been sorted in any way to show preference or feasibility to be done.

1. Switch all LUCI strings into "translate" entities
2. Re-factor LUCI pages into LUCI tabs in order to make it easier to use XHR.Poll or XHR.Get (i.e. openVPN & privoxy)
3. Re-factor LUCI Status page to make it simpler and visual following "openVPN" approach
4. Add all the missing non-critical properties/attributes for each protocol
5. Verify correctness of current IPv4 OSPF configuration. Add any critical property/attribute and align this configuration with bird6-uci and luci-app-bird6
6. Log File Page should show a textbox to select how often the page is refreshed.
7. BGP Instances must have all the properties as optional and let BGP Template populate them. Add a strong WARNING to admins that if they do not configure a template, they are forced to set all the settings appropiately.
8. Add an automated procedure to set the Kernel Tables added through LUCI UI in the /etc/iproute2/rt\_tables file.
9. Add "primary" option to the Device protocol.
10. Find out why adding optional settings or new protocol instances does not save the "anchor" point and moves the user to the top of the page (already asking to #lede-dev in IRC).
11. Remove commented options if they are not required (i.e. "*# disabled;*", "*#   next hop self;*" or "*# rr client;*").
12. Add a warning on the Log configuration. Setting the debug information on may fill system's storage quickly. Provide a way to flush the Log information through the UI. Provide a field to set how often the log page should get refreshed.
13. Look for possible alternatives to the "Additional Field". Add all the *global/common* extra fields to each protocol.
14. Move Static Protocol in LUCI close to Routes definition.
15. Special Static Routes option should be a *List Value* to enhance UX.
16. Interface Static Routes changes to get ANY interface were not committed (re-add fix).
