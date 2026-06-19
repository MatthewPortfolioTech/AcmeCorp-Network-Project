## Troubleshooting lesson
Sydney to Tokyo ping was failing even though:
- OSPF routes were correct on both routers
- Router to router pings worked fine
- PC config was correct

Root cause: TYO-SW-FLOOR1 had PC ports assigned 
to VLAN 10 but TYO-R1 had no subinterfaces configured.
PC traffic was tagged VLAN 10 but router expected 
untagged traffic — mismatch caused drop.

Fix: Moved PC ports back to VLAN 1 to match 
the router's untagged interface.

Lesson: Always make sure switch port VLAN 
assignment matches what the router expects!