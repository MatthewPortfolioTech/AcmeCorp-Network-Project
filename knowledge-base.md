# AcmeCorp Network — Knowledge Base

## VLAN Issues
### Native VLAN mismatch
Symptom: CDP warning, STP blocking port
Cause: Both ends of trunk must have same native VLAN
Fix: switchport trunk native vlan 99 on BOTH ends

## Routing Issues
### Asymmetric routing
Symptom: Ping times out even though route exists
Cause: Return path missing on remote router
Fix: Add static/OSPF route back to source network

### OSPF neighbour not forming
Symptom: show ip ospf neighbor shows nothing
Cause: Network statement wrong, area mismatch, 
       passive-interface on wrong port
Fix: Check network statements and wildcard masks

## Switch Issues
### PC can't reach gateway
Symptom: Ping to default gateway times out
Cause: PC port assigned to wrong VLAN or 
       VLAN doesn't exist on switch
Fix: show vlan brief — check port assignment

## Saving Config
### write memory fails
Symptom: Invalid input detected
Cause: Still in config mode not privileged mode
Fix: type exit until prompt shows hostname#
     then use wr or copy run start

## Password Reference (Note: Project only)
Console:  Acme-Con!
VTY:      Acme-VTY!
Enable:   AcmeCorp2024!

## Key Commands Cheat Sheet
show ip interface brief    — check interface status
show ip route              — check routing table
show ip ospf neighbor      — check OSPF adjacencies
show vlan brief            — check VLAN assignments
show interfaces trunk      — check trunk ports
ping X.X.X.X              — test connectivity