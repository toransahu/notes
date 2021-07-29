<h1>MAC</h1>

[TOC]

Media Access Control

- The IEEE manages MAC addresses
-

## How many combinations / Sufficient?

- 12 digits (0-F i.e. 16 possible chars)
  - 12 hex digits
  - 6 bytes
  - 46 bits
- 16^12=2.81E14
- 281 trillion
- 281, 474, 980, 000, 000
- two hundred and eighty-one trillion, four hundred and seventy-four billion, nine hundred and eighty million
- [40k MAC per person on earth](https://stackoverflow.com/questions/44873804/will-mac-address-ever-run-out-of-combinations)

## OUI

Organization Unique Identifier

- first 6 digits
  - 3 bytes
  - 24 bits
- identifies the vendor/manufacturer
- purchased from IEEE registration authority

## Are MAC addresses really unique?

Or are there any (maybe cloned?) network interface cards that have the same MAC address as another NIC?

What is the probability of having two identical MAC addresses within one network?

- The hardware identification addresses that the IEEE distributes are unique. That makes the probability of matching MAC addresses zero.
- On the other hand, some hardware MAC addresses are programmable, which makes them spoofable. This means that it is possible for two machines in the same network to have the same MAC address.

## MAC Randomization

- Apple release with iOS 8 in 2014
- Android followed the same and introduced with android 8, in 2017; made it default ON with android 10+
- Earlier it was used for probing purpose, later adapted it for association as well
- Random MAC could be identified by looking at the 2nd digit of the MAC, it should be 2, 6, a, e
- Affects N/W vendors and service providers

Ref:

- https://www.mist.com/get-to-know-mac-address-randomization-in-2020/
- https://securityaffairs.co/wordpress/57076/uncategorized/mac-address-randomization-flaws.html
- https://hsc.com/Resources/Blog/Effect-of-Apples-MAC-Randomization-Feature-on-Enterprises
- https://globalreachtech.com/blog-mac-randomisation-apple/

## List of MAC series vs Vendors

- https://regauth.standards.ieee.org/standards-ra-web/pub/view.html#registries
- https://devtools360.com/en/macaddress/vendorMacs.xml
- https://gist.github.com/aallan/b4bb86db86079509e6159810ae9bd3e4

# Read More

1. [IEEE Standards](https://standards.ieee.org/)
1. [IEEE MAC Addresss](https://standards.ieee.org/products-services/regauth/index.html)
