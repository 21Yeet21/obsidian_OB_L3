
You might find convenient to execute the following sequence of commands before doing any other configuration or troubleshooting tasks on your Cisco device, in order to improve your workflow on the terminal.

You will find a command-and-explanation table right below, and a text box with the same command sequence **you can copy and paste on your device's terminal** after that.
## 📑 Table of Contents

- [Configuration Modes](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#configuration-modes)
    
- [Important `show` Commands](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#important-show-commands)
    
- [Filtering Information from `show` Commands](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#filtering-information-from-show-commands)
    
- [Managing Multiple Interfaces](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#Managing-Multiple-Interfaces)
    
- [VLANs](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#VLANs)
    
- [Trunks](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#Trunks)
    
- [VLAN Troubleshooting](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#VLAN-Troubleshooting)
    
- [Voice VLANs](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#Voice-VLANs)
    
- [SSH](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#SSH)
    
- [Dynamic Port Security](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#Dynamic-Port-Security)
    

Note: These commands work on both Cisco routers and switches.

|Command|Additional Notes|
|---|---|
|`CDevice>enable`||
|`CDevice#configure terminal`||
|`CDevice(config)#no ip domain-lookup`|disable DNS lookup|
|`CDevice(config)#cdp run`|ensure CDP is running 💡(although it is running on Cisco devices by default)|
|`CDevice(config)#line console 0`||
|`CDevice(config-line)#logging synchronous`||
|`CDevice(config-line)#history size [lines]`|specify the size (number of lines) for the history of executed commands (you can view your history with `R1#show history`)|
|`CDevice(config-line)#exec-timeout [minutes] [seconds]`||
|`CDevice(config-line)#end`|exit to EXEC privileged mode, where the next command will be executed|
|`CDevice#copy running-config startup-config`|Saves the running configuration to the NVRAM|

You can copy the same sequence, contained in the text box below, and paste it in your Cisco device, whether it is a real-world physical Cisco device, or a simulated device in an environment like Packet Tracer.  
💡 Note that the commands below are abbreviated. Still. They should work just fine.  
💡 Be sure to select and copy up to the blank line below the last command. That way, such last command will be executed without you having to manually press enter.

```
ena
conf t
no ip domain-lookup
cdp run
line con 0
logging syn
his size 50
exec-timeout 25 0
end
copy run start

<< select and copy up to the line above this "marker" with your cursor
```

## Other tips and hints for your initial configurations


💡If there are non-Cisco devices on your network, you might also want to enable LLDP (Link-Layer Discovery Protocol), use:  
`CDevice(config)#lldp run`


---

## Configuration Modes

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#configuration-modes)

```shell
Switch>                # User EXEC mode
Switch> enable         # Privileged EXEC mode
Switch# configure terminal   # Global config mode
Switch(config)# interface fa0/1
Switch(config-if)# description Uplink-to-Router
```

---

## Important `show` Commands

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#important-show-commands)

```shell
show running-config        # Displays the active configuration in RAM
show startup-config        # Displays the saved config in NVRAM (loaded on boot)
show vlan brief            # Lists VLANs, names, status, and assigned ports
show interfaces status     # Shows interface status (UP/DOWN, VLAN, speed, duplex)
show mac address-table     # Displays learned MAC addresses and their ports
show spanning-tree         # Shows STP information (root bridge, port roles/states)
```

---

## Filtering Information from `show` Commands

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#filtering-information-from-show-commands)

```shell
show running-config | include vlan        # Show only lines containing "vlan"
show interfaces | begin GigabitEthernet0/1   # Display output starting from Gi0/1
show mac address-table | exclude dynamic  # Hide all lines with the word "dynamic"
```

---

## Managing Multiple Interfaces

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#managing-multiple-interfaces)

```shell
interface range gi0/1 - 10     # Select multiple interfaces at once (Gi0/1 to Gi0/10)
switchport mode access         # Set all selected ports to access mode
switchport access vlan 20      # Assign VLAN 20 to all selected ports
```

---

## VLANs

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#vlans)

### Creating VLANs

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#creating-vlans)

```shell
vlan 10              # Create VLAN 10
name VLAN10           # Assign a name ("VLAN10") to the VLAN
exit                 # Exit VLAN configuration mode
```

### Deleting VLANs

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#deleting-vlans)

```shell
no vlan 10           # Delete VLAN 10
delete flash:vlan.dat   # Delete the entire VLAN database from flash
```

### Assigning Interfaces to a VLAN

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#assigning-interfaces-to-a-vlan)

```shell
interface gi0/1             # Enter interface Gi0/1
switchport mode access       # Set port as access
switchport access vlan 10    # Assign VLAN 10 to the port
```

---

## Trunks

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#trunks)

### Configuring Trunks

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#configuring-trunks)

```shell
interface gi0/24                          # Enter trunk interface (Gi0/24)
switchport mode trunk                     # Set port as trunk
switchport trunk allowed vlan 10,20,30    # Allow only VLANs 10, 20, and 30
switchport trunk native vlan 99           # Set VLAN 99 as the native VLAN
```

### Dynamic Trunking Protocol (DTP)

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#dynamic-trunking-protocol-dtp)

```shell
switchport mode dynamic desirable   # Actively try to form a trunk
switchport mode dynamic auto        # Passively form a trunk if other side is trunk/desirable
switchport nonegotiate              # Disable DTP negotiation
```

---

## VLAN Troubleshooting

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#vlan-troubleshooting)

```shell
show vlan brief             # Display all VLANs and their assigned ports
show interfaces trunk       # Verify trunk ports and allowed VLANs
show mac address-table      # View MAC addresses learned on the switch
show running-config         # Check VLAN and interface configurations
```

---

## Voice VLANs

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#voice-vlans)

```shell
interface gi0/5              # Enter interface Gi0/5
switchport mode access       # Set port as access
switchport access vlan 10    # Assign VLAN 10 for data
switchport voice vlan 20     # Assign VLAN 20 for voice traffic (IP phones)
```

---

## SSH

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#ssh)

### Initial SSH Setup

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#initial-ssh-setup)

```shell
hostname Switch1                        # Set device hostname  
ip domain-name example.com              # Define domain name (needed for RSA key)  
crypto key generate rsa                 # Generate RSA keys for SSH  
username admin privilege 15 secret cisco123   # Create local admin user  
line vty 0 4                            # Enter VTY line configuration (remote access)  
 transport input ssh                    # Allow only SSH (disable Telnet)  
 login local                            # Use local user database for login  
```

### Modifying SSH Config

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#modifying-ssh-config)

```shell
ip ssh version 2                        # Enable SSH version 2 (more secure)  
ip ssh time-out 60                      # Set SSH idle timeout to 60 seconds  
ip ssh authentication-retries 3         # Allow max 3 login attempts  
```

---

## Port Security

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#port-security)

### Dynamic Port Security

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#dynamic-port-security)

```shell
interface gi0/2                              # Enter interface  
switchport mode access                       # Set interface to access mode  
switchport port-security                     # Enable port security  
switchport port-security maximum 2           # Allow max 2 MAC addresses  
switchport port-security violation shutdown  # Shutdown port if violation occurs  
```

### Sticky Port Security

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#sticky-port-security)

```shell
interface gi0/2                              # Enter interface  
switchport port-security mac-address sticky  # Learn & save MAC addresses dynamically  
```

### Verifying Port Security

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#verifying-port-security)

```shell
show port-security interface gi0/2           # Check security settings for interface  
show port-security address                   # View secure MAC addresses learned  
```

### Err-Disabled Interfaces

[](https://github.com/hyprblaze/Cisco-IOS-Switch-Command-Cheat-Sheet#err-disabled-interfaces)

```shell
show interface status err-disabled           # Show interfaces in error-disabled state  
errdisable recovery cause psecure-violation  # Enable automatic recovery for port-security violations  
errdisable recovery interval 300             # Set recovery interval (300 seconds)  
```

# Enable SSH

[](https://github.com/gmh5225/networking-cheat-sheet/blob/master/enable-ssh.md#enable-ssh)

- Cisco switches have 0 - 15 vty lines
- Cisco routers have 0 - 4 vty lines

Verify SSH support

```
> show ip ssh
```

Configure IP domain

```
(config)# ip domain-name domain name
```

Generate RSA key pair and enable SSH server

```
(config)# crypto key generate rsa # give 1024 when prompted or accept default 512
```

- Note: if you need to delete an RSA key pair and disable the SSH server, run

```
(config)# crypto key zeroize rsa
```

Configure user authentication (local)

```
(config)# username {username} secret {secret}
```

Configure vty lines

```
(config)# line vty 0 15
(config-line)# transport input ssh 
(config-line)# login local
(config-line)# exit
(config)# ip ssh version 2
(config)# exit
```

View SSH connections to the device

```
# show ssh
```

Configure a Switch Virtual Interface for remote management

```
# conf t
(config)# int vlan {management VLAN number}
(config-if)# ip address {ip} {mask}
(config-if)# no shut
(config-if)# exit
(config)# ip default-gateway {ip}
```