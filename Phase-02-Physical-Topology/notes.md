## Progress update
- Placed all HQ Sydney devices
- Cabled topology correctly
- Configured HQ-SYD-R1 with correct IPs from addressing plan
- Configured ISP-CORE serial interface
- WAN link between HQ and ISP confirmed up/up
- First successful ping HQ-SYD-R1 -> ISP-CORE 10.1.254.2

## Lessons learned
- Save commands only work from # mode not config mode
- exit backs you out one level at a time
- Ctrl+Z jumps straight back to # from anywhere
- !!!!! is the best sight in networking

## Key lesson learned
Ping from PC1 to ISP router was failing even though 
the router had correct routes. Problem was the ISP 
router had no return route back to 10.1.1.0/24.

Fixed by adding static route on ISP-CORE:
ip route 10.1.1.0 255.255.255.0 10.1.254.1

Lesson: Routing must work in BOTH directions.
Outbound path AND return path must exist.
This is called asymmetric routing when one 
direction works but the other doesn't.