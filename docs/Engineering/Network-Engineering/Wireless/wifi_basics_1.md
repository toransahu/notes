# Wireless Basics - 1

[TOC]

Sources:

1. [https://courses.mist.com/dashboard](https://courses.mist.com/dashboard)
1. [https://www.mist.com/documentation/wi-fi-basics-1/](https://www.mist.com/documentation/wi-fi-basics-1/)

# IEEE & Wi-Fi Alliance

## IEEE

Institute of Electrical & Electronics Engineers

- creates standard
- like:
    - 802.15.1 (BlueTooth)
    - 802.15.4 (Zigbee)
    - IEEE 1394 (FireWire)
    - 802.3 (Ethernet)
    - 802.11 (Wi-Fi)

## Wi-Fi Alliance

Composed of major players in the wireless industry/space

- Apple
- Comcast
- Sony
- Motorola
- Intel
- Qualcomm
- T-Mobile

Provides branding for Wi-Fi

- "Wi-Fi"
- WPA/WPA2/WPA3
    - 802.11i
- WMM
- Wi-Fi 6

Ensures interoperability between diff vendors

# Wi-Fi Frequencies

## 2.4 GHz & 5 GHz
- unlicensed spectrum

```
.-.   .-.   .-.   .-.   .-.   .-.   .-.   .-.   .-.
   '-'   '-'   '-'   '-'   '-'   '-'   '-'   '-'   '-'
```

## 2.4 GHz Band
- low freq
    - punch stuffs
    - tend to attenuate
- longer wavelength
    - 4.9 inch long
- more range
    - 300 ft ?
- more _crowded_
- more non Wi-Fi interference
- 802.11b/g/n/ax

## 5 GHz Band
- higher freq
- shorter wavelength
    - 2.5 inch long
- less range
    - 90 ft ?
- less _crowded_
- less non Wi-Fi interference
- 802.11a/n/ac/ax

Q. Can a Wi-Fi adapter support multiple bands?  
    Yes, depends on capabilities. Its called Dual-band.


# Wi-Fi History

## Major 802.11 Amendments

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 12-20-23.png" />

Q. Band vs Channel?  
Within these (2.4/5) Wi-Fi frequency bands, we have smaller bands which are referred to as Wi-Fi channels.
A Wi-Fi channel is the medium through which our wireless networks can send and receive data. For routers made in the U.S., the 2.4 GHz band has 11 channels and the 5 GHz band has 45 channels.

Q. Why should I care what Wi-Fi channel I'm on?  
The reason that certain channels aren't the best choice to use is because they have interference. There are a couple different ways this interference is caused: Co-Channel interference results when there are numerous devices all competing for time to talk on the same channel. Adjacent-Channel interference occurs when devices from overlapping channels are trying to talk over each other.

Channels that have interference from other devices are considered to be 'crowded'. The time it takes to transmit data is increased and you are left waiting for your Internet request to be made. The channels with the most interference are those that overlap with each other. 

To further explain channel overlapping, let's look at the 2.4 GHz band, where each channel is allotted 20 MHz and separated by 5 MHz. Considering the 2.4 GHz band is only 100 MHz wide, the 11 channels of 20 MHz overlap with one another. This is what causes the interference on your network and and a lag in your Wi-Fi's performance.

Certain channels yield better Wi-Fi performance than others because they are non-overlapping. Yes, there are some channels in the 2.4 GHz spectrum that don't overlap with the other channels. These are the channels you ought to look for, especially if experiencing Wi-Fi problems: Channels 1, 6, and 11.

Read more: 
1. https://www.minim.com/blog/wifi-channels-explained
1. https://www.electronics-notes.com/articles/connectivity/wifi-ieee-802-11/channels-frequencies-bands-bandwidth.php

Note: There are also 24 non-overlapping channels in the 5 GHz band spectrum.

# 2.4 GHz Band Channels

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 12-22-36.png" />

- 20 MHz wide
- 11 channels

Q. Different Country vs Channels? Possible?  
Yes. Europe has 12,13 as well. Japan has 14 as well.


# Wi-Fi 2.4 Ghz and Interference

# Wi-Fi Adjacent Channel Interference
STAs on overlapping channels will corrupt each other's transmission.

# Half Duplex Wi-Fi
Only one device can transmit on a channel at a time.


<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 12-37-48.png" />

_Ethernet cables are made up of multiple twisted pair of copper, they MUX. They can talk & listen at the same time._

# Co-channel interference
Slow devices on the channel consume more airtime.

# 2.4 GHz Channel Re-Use

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 12-57-59.png" />

But avoiding interference in 2.4GHz is hard due to high range.

NOTE: Mist use channels 1,6,11 world-wide. (btw, they support all)

# Wi-Fi 5 Ghz

# Wi-Fi 5 Ghz Channels
- lot more channels
- thus lot more throughput


<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 13-17-10.png" />


# Wi-Fi DFS

Dynamic frequency selection

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 13-43-37.png" />

If detected radar, move to other channel. Announce to move other APs as well.


# Wi-Fi Channel Bonding

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 13-52-02.png" />

haha typo.

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 13-56-13.png" />

haha typo again.


# 5 GHz Channel Re-Use

Channel reuse is much easier in 5 GHz band.

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 13-59-04.png" />


# Wi-Fi Signal Strength

Unit/repr: dB
and dBm for absolute values.

_dB quantifies the ratio between two values, whereas dBm expresses the absolute power level. dBm is an absolute unit, whereas dB is a dimensionless unit. dBm is always relative to 1mW, while dB is expressed in watts and can be relative to other powers._

the unit is logarithmic & not linear, so lets see 3 & 10 rule for simiplicty:

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 14-09-04.png" />

Isn't there something in positive scale? Yes, _mW_. :D  LOL! see the figures in mW.

```bash
iwconfig

# for streaming results
watch -n1 iwconfig
```

# BSSID, SSID and ESSIDs

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 14-31-40.png" />

- 128 clients per SSID per radio is a kind of hard limit amongs different vendors
- ~30 clients per SSID per radio is a kind of best practice to avoid poor bandwidth

# Other Wireless Technologies

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 14-36-51.png" />

# Bluetooth Low Energy (BLE)

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 14-40-26.png" />


# Wi-Fi NICs vs Ethernet
<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 14-45-53.png" />


# SNR and Data Rates

## SNR

How much signal above the background noise.

Unit: dB

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 15-11-33.png" />

## Data Rate
The same "Maximum Signaling Rate". Defined per standards 802.11xyz.
Unit: Mbps

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 16-44-53.png" />

Good the SNR, Can choose/set higher Data rates.

Q. Signaling Rate vs Throughput?  
TBD

### MCS
Modulation and Coding scheme.

Ref:

1. http://mcsindex.com/
1. https://www.wlanpros.com/mcs-index-charts/

# Network Packets vs Frame
TBD

# Wi-Fi Frame Types and Timing

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 16-50-48.png" />

_STA (Station): In IEEE 802.11 (Wi-Fi) terminology, a station (abbreviated as STA) is a device that has the capability to use the 802.11 protocol. For example, a station may be a laptop, a desktop PC, PDA, access point or Wi-Fi phone._

## Airtime Arbitration Process

How wireless devices decides, who's going to talk next?

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 16-57-05.png" />

# Wi-Fi Roaming
<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/" />

# Wi-Fi Security

_Ethernet is a bounded medium, inheritently & physically secure. What about security of unbounded Wi-Fi?_

A Wi-Fi adapter in monitor mode can eavesdrop.. can capture all the packets nearby.. hmm..

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 17-19-13.png" />

What Mist supports today:

- WPA-2/PSK with passphrase
- WPA-2/EAP (802.1X)
- Open Access
- WPA-2/PSK with multiple passphrases
- WPA-PSK/TKIP
- WPA2-PSK/TKIP
- WEP
- Multi-mode/PSK with passphrase
- Multi-mode/EAP (802.1X)
- OWE Transition
- OWE
    - Opportunistic Wireless Encryption
- MAC address authentication by RADIUS lookup

# Roaming
Every client device has its own green diamond. :D
Some can roam, some are not designed to roam.

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-03 17-25-55.png" />

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-03 17-27-21.png" />

# Wi-Fi Design

How to design a wireless network? Probably for a customer.. :p

## Determine requirements

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-02 17-22-24.png" />

### Client channel support

Some devices might not support some channels, so plan accordingly.

Ref: https://clients.mikealbano.com/ (Mike - Our OpenConfig guy, from Wireless N/W Team, Google) ;)

### Further Define Metrics

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-03 17-40-32.png" />


# Wi-Fi Ekahau Design

Software to design a Wireless network.

<img src="../../../../statics/notes/docs/industrial/networking/wireless/img/Screenshot from 2021-02-03 17-41-55.png" />
