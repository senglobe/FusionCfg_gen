# FusionCfg_gen
This script will generate BGP configuration for fusion device. The output file will contain configuration for all the fusion devices. However, within file the configuration is split based on borders L3 hand-off interface neighbour device.

The script is executable from the DANC SSH session. 

download the script (FusionCfg_gen_v1.0) and scp to DANC tmp folder. Then execute the file by just providing the file name.

example:

[Fri Jul 10 04:48:20 IST] maglev@192.168.5.11 (maglev-master-1) ~
$ FusionCfg_gen_v1.0

 ******************************************************************************************************************* 
 
This tool will generate BGP configuration for your fusion router(s) 

 - Developed for Cisco engineers internal consumption, no official support will be provided for this tool 
 - The tool will generate bgp, VLAN and interface VLAN configurations based on L3hand-off configured on DNAC 
 - Configuration will be generated for all the borders and its all neighbors(not just for newly created L3 Handoff)
 - configuration is generated assuming all the neighbors are in ipv4 address-family (no vpnv4 address-family support in tthis tool release) 
 - The output 'FusionConfig_currenttime' will be saved in the same directory from where the tool has been executed 
 - DO NOT copy and past all the configuration in one go 
 - Please feel free to share your feedback on senthku2cisco.com 
 
*******************************************************************************************************************

Enter DANC IP address :10.105.192.135
Enter DANC admin username : admin
Enter DNAC admin password : 

***---*** Initiating data Collection ***---***

The output file will be stored in the same location or path of the binary file as *FusionCofig_Jul-10-2020_04-49.txt*

***---*** Fusion configuration generation is completed ***---***

[Fri Jul 10 04:49:02 IST] maglev@192.168.5.11 (maglev-master-1) ~
$   



Output:
$ sudo cat FusionCofig_Jul-10-2020_04-49.txt


BLR_BORDER.cisco.com external interface TenGigabitEthernet1/0/9 neighbor device Configuration 

router bgp 65000
  bgp log-neighbor-changes 
  neighbor 192.5.100.13 65005
  neighbor 192.5.100.13 update-source 3007
  neighbor 192.5.100.17 65005
  neighbor 192.5.100.17 update-source 3008

 address-family ipv4 
  neighbor 192.5.100.13 activate
  neighbor 192.5.100.13 weight 65535
  neighbor 192.5.100.17 activate
  neighbor 192.5.100.17 weight 65535

vlan 3007
 
inteface vlan 3007
 ip address 192.5.100.14255.255.255.252
 no shutdown 

vlan 3008
 
inteface vlan 3008
 ip address 192.5.100.18255.255.255.252
 no shutdown 

 
 *********************** end of device BLR_BORDER.cisco.com- interface TenGigabitEthernet1/0/9*********************** 


BLR_BORDER.cisco.com external interface TenGigabitEthernet1/0/8 neighbor device Configuration 

router bgp 65000
  bgp log-neighbor-changes 
  neighbor 192.5.100.1 65005
  neighbor 192.5.100.1 update-source 3001
  neighbor 192.5.100.5 65005
  neighbor 192.5.100.5 update-source 3002
  neighbor 192.5.100.9 65005
  neighbor 192.5.100.9 update-source 3006

 address-family ipv4 
  neighbor 192.5.100.1 activate
  neighbor 192.5.100.1 weight 65535
  neighbor 192.5.100.5 activate
  neighbor 192.5.100.5 weight 65535
  neighbor 192.5.100.9 activate
  neighbor 192.5.100.9 weight 65535

vlan 3006
 
inteface vlan 3006
 ip address 192.5.100.10255.255.255.252
 no shutdown 

vlan 3001
 
inteface vlan 3001
 ip address 192.5.100.2255.255.255.252
 no shutdown 

vlan 3002
 
inteface vlan 3002
 ip address 192.5.100.6255.255.255.252
 no shutdown 

 
 *********************** end of device BLR_BORDER.cisco.com- interface TenGigabitEthernet1/0/8*********************** 

 
 ------------------------------------ end of device BLR_BORDER.cisco.com------------------------------------


CHN_BORDER.cisco.com external interface TenGigabitEthernet1/0/8 neighbor device Configuration 

router bgp 65000
  bgp log-neighbor-changes 
  neighbor 192.5.200.9 65015
  neighbor 192.5.200.9 update-source 3003
  neighbor 192.5.200.13 65015
  neighbor 192.5.200.13 update-source 3004

 address-family ipv4 
  neighbor 192.5.200.9 activate
  neighbor 192.5.200.9 weight 65535
  neighbor 192.5.200.13 activate
  neighbor 192.5.200.13 weight 65535

vlan 3004
 
inteface vlan 3004
 ip address 192.5.200.14255.255.255.252
 no shutdown 

vlan 3003
 
inteface vlan 3003
 ip address 192.5.200.10255.255.255.252
 no shutdown 

 
 *********************** end of device CHN_BORDER.cisco.com- interface TenGigabitEthernet1/0/8*********************** 

 
 ------------------------------------ end of device CHN_BORDER.cisco.com------------------------------------

[Fri Jul 10 04:49:54 IST] maglev@192.168.5.11 (maglev-master-1) ~
