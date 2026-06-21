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

## Serial interface numbering
Serial port slot numbers vary depending on which 
physical slot the NIM-2T module is installed in.
Always run 'show ip interface brief' first to 
confirm the actual interface name before configuring!

## Serial link troubleshooting
Commands to diagnose serial link issues:
- show controllers Serial0/x/x
- Must show DCE on provider/ISP end
- Must show clock rate configured
- "No serial cable attached" = cable on wrong port!

Common mistakes:
1. Wrong end selected as DCE when cabling
2. Clock rate not set on DCE end
3. Cable connected to wrong serial port
4. Interface has IP on wrong port number

Fix process:
1. show controllers → check DCE/DTE and clock
2. show ip interface brief → check which port is down/down vs admin down
3. Delete cable → reconnect to correct ports
4. Set clock rate on DCE end
5. Make sure IP is on correct interface


## DHCP verification commands
show ip dhcp binding   ← see all leased IPs + MAC addresses
show ip dhcp pool      ← see pool stats, leased vs available
show ip dhcp conflict  ← check for duplicate IPs (should be empty!)

## DHCP best practices
- Always exclude infrastructure IPs (.1 to .9)
- One pool per subnet/VLAN
- lease command not supported in older PT versions
- dns-server and domain-name make PCs fully configured

## NAT Troubleshooting
Symptoms: ping timing out after NAT configured

Checklist:
1. Default route on inside router pointing to ISP
2. NAT outside interface has PUBLIC IP not private
3. show ip nat translations — Inside Global must 
   show public IP not private
4. ISP router knows route to NAT public subnet
5. Internet-side routers have return route back 
   to NAT public IP

Key commands:
clear ip nat translation *  ← clear old translations
show ip nat translations    ← verify NAT working
show ip nat statistics      ← check hit/miss counts