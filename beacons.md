# Routing Beacons

RIS Route Collectors originate a small number of prefixes. These serve to better understand the state of the global BGP Internet routing system.

These prefixes can be divided into 2 types:
   * Beacon prefixes: These prefixes are announced and withdrawn according to a set schedule. The propagation of the announcement and widthdrawal, or lack thereof, can inform us about the state of the Internet BGP routing system
   * Anchor prefixes: These prefixes are supposed to be announced all the time. Typically, one pair of a beacon and anchor prefix is announced from a specific route collector (RRC). This way anchor prefixes can be used to differentiate between activity seen as a result of changes on the originating RRC and that seen for other reasons. iF the anchor flaps, it could mean that the RRC was reloaded and activity of the corresponding beacon can be ignored when doing analysis of the RIS data.

If one wants to make special arrangements for routing beacons, contact us at ris@ripe.net . Since we XXX . An alternative for experiments with these types of set-ups is the [PEERING project](https://peering.ee.columbia.edu/).

We ask our peers to accept and propagate our anchor and beacon prefixes, and try to make an effort to have them seen globally, but it must be noted that
global visibility of these prefixes is not guaranteed.  XXX this is too vague?

All IPv4 beacon prefixes are announced with additional attributes. We overload the BGP AGGREGATOR attribute to tag each announcement with a timestamp, a sequence number and the identifier of the RRC making the announcement. These are encoded as follows:

   * AGGREGATOR IP ADDRESS: 10.x.y.z, where x, y and z form a 24-bit count of the number of seconds between the start of the month and the time of the announcement.
   * AGGREGATOR AS NUMBER: 64512 + n, where n is a 10-bit number encoded as

    MSB                                   LSB
    +---+---+---+---+---+---+---+---+---+---+
    | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
    +---+---+---+---+---+---+---+---+---+---+
    |    RRC ID     |    Sequence Number    |
    +---+---+---+---+---+---+---+---+---+---+
  
Adding 64512 brings the resulting number into the private AS number range.


# History

Routing beacons started with XXX . RIS has been long-running

Current routing beacon information in machine readable format can be found here:
   
   ris-routing-beacons.json XXX todo create this file
