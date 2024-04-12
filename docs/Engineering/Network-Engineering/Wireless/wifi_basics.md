# How Wireless Works

- As Radio Frequency (RF)
- Travels in a portion of electromagnetic spectrum (RF is part of electromagnetic spectrum)
- What is electromagnetic spectrum? 
    - The range of all possible electromagnetic radiation
    - Waves that can move through matter or space
- Electromagnetic Spectrum (in decreasing wavelength top to down)

    ```
                        - - Broadcast band (10^3 meters or 1 kilometer) 
                        | -
                        | - Radio (10^0 m or 1 meter)
    Radio Spectrum    --| -
                        | - Radar (10^-3 m or 1 millimeter) 
                        | -
                        - - Microwaves 
                        | -
                        | - Infrared (IR) (10^-6 m or 1 micrometer )
                        | - <--- Visible lights to human (700 nanometers to 400 nanometers)
                        | -
    Optical Spectrum  --| - Ultraviolet (UV)
     (can be seen       | -
     using some tool)   | - X-rays (10^-9 m or 1 nanometer)
                        | -
                        | - Gamma rays
                        | -
                        - - Cosmic rays (10^-12 m or 1 picometer)
    ```
- WiFi access point transmits RF signal at a particular wavelength
    - The characteristic of __wavelength__ and __environment__ determines how far the signal can travel and deliver data


# Wireless SWOTs

(think w.r.t. a Wi-Fi client)

## Strength

- Convenience (access without a wire)
- Mobility (clients can move)
- Productivity (access from various locations)
- Deployment (no cabling)
- Extendability (easily scale up & down)
- Expense (lower ownership & maintenance cost)

## Weakness

- Security (data travels through RF and can be captured by unknows in between; need encyption)
- Range (is limited)
- Speed (usually no faster than 54 Mbps - will improve in near future)
- Complexity (wavelenght, channel, band, spectrum etc)

## Opportunity

- Increased Speed (802.11ac promise drastic improvement)
- Better Security (continues to improve, VLAN, etc.)

## Threat

- Usual security threats
    - Denial of Service (DoS)
    - Rogue WAPs
    - Poorly configured WAPs
    - Sniffing
    - Wireless Driver Attacks


# Wireless Signal Characteristics

(Defined by law of Physics)

## Wavelength

- What: Distance between one complete oscillation (from positive crest to negative valley & back)
- Unit:

## Frequency

- What: No. of times a signal occurs in a given time period
- Unit: Hz (by Heirich Rudolf Hertz)
- A cycle that occurs 1 time in 1 second = 1 Hz
- A cycle that occurs 500 times in 1 second = 500 Hz
- Frequency is inversly proportional to Wavelength

## Amplitude

- What: The strength or power of the signal
- Unit:

## Phase

- What: The relationship between 2 or more signals
- Unit: Degree
- If peaks are exactly aligned, they are in same phase else out of phase
- 2 signal in same phase results in much greater signal strength (potentially as much as twice the amplitude)
- 2 signal exactly 180 degree out of phase cancel outs each other 


# Wireless Components

- Simply
    - Wireless access point (WAP)
        - various types
        - based on 802.11
        - utilizes diff. freq.
    - Wireless client (Receiver)
        - diff. NIC (Network Interface Card) have diff. performance
- In-depth
    - Frequency
        - e.g. 2.4GHz vs 5GHz
    - Environment
        - Lighting, Fog, Humidity etc
    - RF interference
        - 2.4GHz range is shared by phone, microwaves, and other devices as well
    - Electrical interference
        - Computer, appliances, fan etc.
    - Obstacles
    - Signal delivery
        - Diff. signal technologies have their pros & cons
        - FHSS, DSSS, OFDM etc.


# Measuring Wireless Power

Major performance concerns

- Coverage
    - Distance
    - Area
- Performance
    - Speed of data transfer
    - Simultaneous connections

This boils down to power. Understanding power and signal measurement helps. Especially in design phase.

Things about measurement

- A lot of things are measured as relative & absolute/actual value
- power is measure as absolute value
- unit is watt (W)
- where 1 milliwatt (mW) = 1000th of a watt
- most 802.11 equipments uses 300 mW of transmit power or less
- max power is limited by FCC in the US
- However, changes in power is measured in `decibels (dB)`
    - decibel is unit of comparision, not unit of power
    - to represent diff. between two power value
    - e.g. diff. between power of two transmitters
    - e.g. output of a transmitter/antenna Vs  signal received by the receiver/client
- A unit `bel` is the ratio of a 10 to 1 difference (came from Bell Labs)
- A decibel is 1/10 of a `bel` (i.e. 100 to 1 ratio diff.)
- $dB = 10log_{10}(\frac{A}{B})$  where $A$ & $B$ are power values

Example:

```
                                  ┌───────┐
                          10mW    │       │
                       ┌─────────►│Laptop1│
                       │          │       │
┌────────────┐         │          └───────┘
│            │  100mW  │
│Access Point├─────────┤
│            │         │
└────────────┘         │          ┌───────┐
                       │  1mW     │       │
                       └─────────►│Laptop2│
                                  │       │
                                  └───────┘
```

__Q. Here, what is the diff. in signal received by two laptops?__  
__A.__ Laptop1's signal is 1 bel or 10 decibel more than Laptop2.  
Because, Laptop1=10mW; Laptop2=1mW  
Thus, $dB = 10log_{10}(\frac{10}{1}) = 10$  


__Q. Here, what is the diff. in signal transmitted by AP vs received by Laptop2?__  
__A.__ AP's signal is 20 dB more than Laptop2.  
Because, AP=100mW; Laptop2=1mW  
Thus, $dB = 10log_{10}(\frac{100}{1}) = 20$  

Ref: https://support.huawei.com/enterprise/en/doc/EDOC1000113315/c3242b10/power-and-signal-strength


# Wireless Topologies

Wireless network can be designed in various physical arrangements.

802.11 standard defines 4 wireless topologies:

## Basic Service Set (BSS)

## Extended Service Set (ESS)

## Independent Basic Service Set (IBSS)

## Mesh Basic Service Set (MBSS)
