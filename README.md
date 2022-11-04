# Overview

Based on https://github.com/DhavalKapil/icmptunnel https://github.com/lucadibello/WeaponizedPing 

Based on MITRE Tactics: T1572 Protocol Tunneling, T1030 Data Transfer Size Limits, T1567 Exfiltration Over Web Service, T1090 Multi-hop Proxy

Encrypted version for ICMP tunneling. 

Exfiltration of data in a restricted network environment can be a tough thing to do. When you do things like plugging USB, moving and sending files across networks to yourself. It all leaves an audit trail. This audit trail can be even stronger when used with powerful endpoint protection tools like CrowdStrike. Even when you try to cover your tracks and footprints, using VPNs and deleting logs files, there is still a possibility of being traced back to you when digital forensics is being conducted. This could result in the court ordering ISP, service providers to give up subscriber’s VPN information. 

ICMP packets are usually used for troubleshooting throughout networks or to check whether hosts are alive. We utilise this to send information or files out to other public endhosts.  

This is for testing purposes only. Use it at your own risk and only at authorised computers. Some of the stuff are hardcoded so better look before using anything. Thanks

## Topology 
Exfiltration of data scenario
![ICMP an0nymizer (1)](https://user-images.githubusercontent.com/91510432/199385807-3f38685b-4c55-4eba-bd30-271af9bc2d56.png)

### Overview of an encrypted packet
![Screenshot_3](https://user-images.githubusercontent.com/91510432/199401514-62c5d4ef-88d5-4632-8312-259aee4c9328.png)


### Usage 
1. `pip3 install -r requirements.txt`

2. Move the Documents folder to your Desktop (Windows victim)

3. Using another Linux machine. You can use VPN or proxychains here whatever.
    - Move your private.pem key here.
    - Move decryptor.py here.

4. Sniffing of packets and decrypting it (Sniffing and reconstructing files or information)
    - If you are sniffing through SSH from a server. Run the command `ssh -i webserver.pem root@<ip address> tcpdump -U -s0 -w - 'not port 22' | wireshark -k -i -`
    - If you are sniffing through a normal private network. Run wireshark and save the pcap file.
    - Copy the temporary wireshark pcap filepath output
    - On the victim machine, execute the python command `python ./ping.py` OR run the ping.exe file.
    - Monitor wireshark for ICMP pings with bigger than usual data blocks. Stop when all packets are sent
    - Run the command to start the reconstructing files with the filepath copied `python ./decryptor.py -p <paste copied filepath here>`
