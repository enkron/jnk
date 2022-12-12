# Networking

<details>

<summary>Table of content</summary>

- [main](#main)
    * [nmcli](#nmcli)

</details>


# [main]

## [nmcli]
```bash
# Identify a WI-FI access point (scan for nearby wifi networks)
nmcli d wifi list

# Connect to WI-FI
sudo nmcli d wifi connect <SSID> password <PSWD>
sudo nmcli --ask d wifi connect <SSID> # in case WEP/WPA security is on

# Manage connections
nmcli c show # view all saved connections
nmcli c down <SSID> # disconnect from a particular network
nmcli c up <SSID> # connect to another saved network
```
