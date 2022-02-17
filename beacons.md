# Routing Beacons

RIS Route Collectors originate a small number of prefixes. These serve to better understand the state of the global BGP Internet routing system.

These prefixes can be divided into 2 types:
   * Beacon prefixes: These prefixes are announced and withdrawn according to a set schedule. The propagation of the announcement and widthdrawal, or lack thereof, can inform us about the state of the Internet BGP routing system
   * Anchor prefixes: These prefixes are supposed to be announced all the time. Typically, one pair of a beacon and anchor prefix is announced from a specific route collector (RRC). This way anchor prefixes can be used to differentiate between activity seen as a result of changes on the originating RRC and that seen for other reasons. iF the anchor flaps, it could mean that the RRC was reloaded and activity of the corresponding beacon can be ignored when doing analysis of the RIS data.

We ask our peers to accept and propagate our anchor and beacon prefixes, and we try to make an effort to have them seen globally, but it must be noted that
global visibility of these prefixes is not guaranteed. If you notice any of these prefixes not propagating globally, please let us know at ris@ripe.net

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

If one wants to make special arrangements for routing beacons, contact us at ris@ripe.net , but keep in mind that in IPv4 the address space that we have available is very limited. An alternative for experiments with routing beacons is the [PEERING project](https://peering.ee.columbia.edu/).

# Current Beaconing Setup

| IPv4 prefix      | IPv6 prefix        | type     | origin RRC (IXP/multihop)   |peer location(s)|
|:-----------------|:-------------------|:---------|:----------------------------|:---------------|
|84.205.64.0/24	   | 2001:7FB:FE00::/48 | beacon   | RRC00 (multihop)            | global         |
|84.205.65.0/24	   | 2001:7FB:FE01::/48 | beacon   | RRC01 (LINX/LONAP)          | GB             |
|84.205.67.0/24	   | 2001:7FB:FE03::/48 | beacon   | RRC03 (AMS-IX, NL-IX).      | NL,DK          |
|84.205.68.0/24	   | 2001:7FB:FE04::/48 | beacon   | RRC04 (CIXP)                | CH (FR?XXX)    |
|84.205.69.0/24	   | 2001:7FB:FE05::/48 | beacon   | RRC05 (VIX)                 | AT	            |
|84.205.70.0/24    | 2001:7FB:FE06::/48 | beacon   | RRC06 (DIX-IE)              | JP             |
|84.205.71.0/24	   | 2001:7FB:FE07::/48 | beacon   | RRC07 (NETNOD)              | SE	            |
|84.205.74.0/24    | 2001:7FB:FE0A::/48 | beacon   | RRC10 (MIX)                 | IT             |
|84.205.75.0/24	   | 2001:7FB:FE0B::/48 | beacon   | RRC11 (NYIIX)               | US             |
|84.205.76.0/24	   | 2001:7FB:FE0C::/48 | beacon   | RRC12 (DE-CIX)              | DE             |
|84.205.77.0/24    | 2001:7FB:FE0D::/48 | beacon   | RRC13 (MSK-IX)              | RU	            |
|84.205.78.0/24	   | 2001:7FB:FE0E::/48 | beacon   | RRC14 (PAIX)                | US             |
|84.205.79.0/24	   | 2001:7FB:FE0F::/48 | beacon   | RRC15 (PTTMetro-SP)         | BR             |
|84.205.73.0/24    | 2001:7FB:FE10::/48 | beacon   | RRC16 (NOTA	Miami)         | US             |
|                  | 2001:7FB:FE12::/48 | beacon   | RRC18 (CATNIX)              | ES             |
|84.205.82.0/24    | 2001:7FB:FE13::/48 | beacon   | RRC19 (NAP Africa JB)       | ZA 	          |
|                  | 2001:7FB:FE14::/48 | beacon   | RRC20 (SwissIX)             | CH             |
|93.175.149.0/24	 | 2001:7FB:FE15::/48 | beacon   | RRC21 (FranceIX PAR/MAR)    | FR             |
|                  | 2001:7FB:FE16::/48 | beacon   | RRC22 (InterLAN)            | RO             |
|93.175.151.0/24	 | 2001:7FB:FE17::/48 | beacon   | RRC23 (Equinix Singapore)   | SG             |
|93.175.153.0/24   | 2001:7FB:FE18::/48 | beacon   | RRC24 (multihop)            | LACNIC region  |


# History

Routing beacons started with XXX . RIS has been long-running

Current routing beacon information in machine readable format can be found here:
   
   ris-routing-beacons.json XXX todo create this file
