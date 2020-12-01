# FusionCfg_gen
This script will generate BGP configuration for fusion device. The output file will contain configuration for all the fusion devices connected to SD-Access border. The configuration output file is split in multiple sections per on borders and L3 hand-off interface neighbour device.

The script will read the Border devices BGP configuration pushed by the DNAC and accordingly the neighbour devices(Fusion) BGP configuration is generated. Hence, before executing the script ensure you have configured L3-Hand-off from DNAC for the borders and in all desired Virtual networks.

## How to Execute

The script is executable from the DANC SSH session.

*1*. Download the script (FusionCfg_gen_vX.X) and copy (SCP or your preferred method) to DANC /tmp folder

*2*. Provide execute access to the file.<br/>
_/snip/_<br/>
$ sudo  chmod 777 FusionCfg_gen_v1.1<br/>
[sudo] password for maglev:<br/>
[Tue Dec 01 19:52:34 IST] maglev@192.168.5.11 (maglev-master-1) fusion_cfg<br/>
$ ls -l FusionCfg_gen_v1.1<br/>
-rwxrwxrwx 1 maglev maglev 5887712 Dec  1 18:53 FusionCfg_gen_v1.1<br/>
[Tue Dec 01 19:52:45 IST] maglev@192.168.5.11 (maglev-master-1) fusion_cfg<br/>
_/snip/_<br/>

*3*. Execute the file as any any other script, like -  “./“+filename <br/>
_/snip/_<br/>
$ ./FusionCfg_gen_v1.1 <br/>
_/snip/_<br/>


## Execution Example:<br/>

### Execution
$ ./FusionCfg_gen_v1.1 

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

Enter DANC IP address : _you IP-address_ <br/>
Enter DANC admin username : _admin_ <br/>
Enter DNAC admin password : _password_ <br/>

***---*** Initiating data Collection ***---***

The output file will be stored in the same location or path of the binary file as *FusionCofig_Dec-01-2020_19-59.txt*

***---*** Fusion configuration generation is completed ***---***

### _Configuration File_

$ ls -l<br/>
total 5756<br/>
-rwxrwxrwx 1 maglev maglev 5887712 Dec  1 18:53 FusionCfg_gen_v1.1<br/>
-rw-r----- 1 maglev maglev    3338 Dec  1 19:59 FusionCofig_Dec-01-2020_19-59.txt<br/>

$ cat FusionCofig_Dec-01-2020_19-59.txt <br/>


BLR_BORDER.cisco.com external interface TenGigabitEthernet1/0/9 neighbor device Configuration <br/>

router bgp 65000<br/>
  bgp log-neighbor-changes <br/>
  neighbor remote-as192.5.100.13 65005<br/>
  neighbor 192.5.100.13 update-source vlan3007<br/>
  neighbor remote-as192.5.100.17 65005<br/>
  neighbor 192.5.100.17 update-source vlan3008<br/>

 address-family ipv4 <br/>
  neighbor 192.5.100.13 activate <br/>
  neighbor 192.5.100.13 weight 65535 <br/>
  neighbor 192.5.100.17 activate <br/>
  neighbor 192.5.100.17 weight 65535 <br/>

vlan 3007 <br/>
 name BLR_BORDER_BGP_Int <br/>

interface vlan 3007 <br/>
 description BGP_Int_BLR_BORDER_TenGigabitEthernet1/0/9 <br/>
 ip address 192.5.100.14 255.255.255.252 <br/>
 no shutdown <br/>

vlan 3008 <br/>
 name BLR_BORDER_BGP_Int <br/>

interface vlan 3008 <br/>
 description BGP_Int_BLR_BORDER_TenGigabitEthernet1/0/9 <br/>
 ip address 192.5.100.18 255.255.255.252 <br/>
 no shutdown <br/>

 
 *********************** end of device BLR_BORDER.cisco.com- interface TenGigabitEthernet1/0/9*********************** <br/>


BLR_BORDER.cisco.com external interface TenGigabitEthernet1/0/8 neighbor device Configuration <br/>

router bgp 65000 <br/>
  bgp log-neighbor-changes <br/>
  neighbor remote-as192.5.100.1 65005 <br/>
  neighbor 192.5.100.1 update-source vlan3001 <br/>
  neighbor remote-as192.5.100.5 65005 <br/>
  neighbor 192.5.100.5 update-source vlan3002 <br/>
  neighbor remote-as192.5.100.9 65005 <br/>
  neighbor 192.5.100.9 update-source vlan3006 <br/>

 address-family ipv4 <br/>
  neighbor 192.5.100.1 activate <br/>
  neighbor 192.5.100.1 weight 65535 <br/>
  neighbor 192.5.100.5 activate <br/>
  neighbor 192.5.100.5 weight 65535 <br/>
  neighbor 192.5.100.9 activate <br/>
  neighbor 192.5.100.9 weight 65535 <br/>

vlan 3006 <br/>
 name BLR_BORDER_BGP_Int <br/>

interface vlan 3006<br/>
 description BGP_Int_BLR_BORDER_TenGigabitEthernet1/0/8<br/>
 ip address 192.5.100.10 255.255.255.252<br/>
 no shutdown <br/>

vlan 3001<br/>
 name BLR_BORDER_BGP_Int<br/>

interface vlan 3001<br/>
 description BGP_Int_BLR_BORDER_TenGigabitEthernet1/0/8<br/>
 ip address 192.5.100.2 255.255.255.252<br/>
 no shutdown <br/>

vlan 3002<br/>
 name BLR_BORDER_BGP_Int<br/>

interface vlan 3002<br/>
 description BGP_Int_BLR_BORDER_TenGigabitEthernet1/0/8<br/>
 ip address 192.5.100.6 255.255.255.252<br/>
 no shutdown <br/>

 
 *********************** end of device BLR_BORDER.cisco.com- interface TenGigabitEthernet1/0/8*********************** <br/>

 
 ------------------------------------ end of device BLR_BORDER.cisco.com------------------------------------


CHN_BORDER.cisco.com external interface TenGigabitEthernet1/0/8 neighbor device Configuration <br/>

router bgp 65000<br/>
  bgp log-neighbor-changes <br/>
  neighbor remote-as192.5.200.9 65015<br/>
  neighbor 192.5.200.9 update-source vlan3003<br/>
  neighbor remote-as192.5.200.13 65015<br/>
  neighbor 192.5.200.13 update-source vlan3004<br/>

 address-family ipv4 <br/>
  neighbor 192.5.200.9 activate<br/>
  neighbor 192.5.200.9 weight 65535<br/>
  neighbor 192.5.200.13 activate<br/>
  neighbor 192.5.200.13 weight 65535<br/>

vlan 3004<br/>
 name CHN_BORDER_BGP_Int<br/>

interface vlan 3004<br/>
 description BGP_Int_CHN_BORDER_TenGigabitEthernet1/0/8<br/>
 ip address 192.5.200.14 255.255.255.252<br/>
 no shutdown <br/>

vlan 3003<br/>
 name CHN_BORDER_BGP_Int<br/>

interface vlan 3003<br/>
 description BGP_Int_CHN_BORDER_TenGigabitEthernet1/0/8<br/>
 ip address 192.5.200.10 255.255.255.252<br/>
 no shutdown <br/>

 
 *********************** end of device CHN_BORDER.cisco.com- interface TenGigabitEthernet1/0/8*********************** 

 
 ------------------------------------ end of device CHN_BORDER.cisco.com------------------------------------
