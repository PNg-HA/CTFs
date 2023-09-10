Challenge link: https://play.picoctf.org/practice/challenge/103?category=4&page=1

Hint: `What are some other ways to hide data?`

Open the file with Wireshark. Wireshark -> Statistics -> Conversation -> IPv4:
![image](https://github.com/PNg-HA/CTFs/assets/93396414/a2af95a1-b799-4e39-8117-52d5203ab97c)
Ignore the part 192.168... because those belongs to SSDP, not related to this challenge much.
Wireshark -> Statistics -> Protocol Hierarchy:
![image](https://github.com/PNg-HA/CTFs/assets/93396414/f3248494-9857-48b2-8e6d-39ad0eabf2db)
Notice the data in TFTP. There are a lot of bytes.
Type TFTP in display filter:
![image](https://github.com/PNg-HA/CTFs/assets/93396414/8d09b53c-0c61-4b1c-8250-1e27f340a41e)
Logic of TFTP Write:

A -----Request_Write-----> B

A <---------ACK----------  B

A --------Data-----------> B

A <---------ACK----------  B

Logic of TFTP Read:

A -----Request_Read------> B

A <--------Data----------- B

A ---------ACK-----------> B

The pcap file has captured the TFTP conservation of two vmware, IP .11 and .12. But for short, File->Export->TFTP and download those file transferd by TFTP:
![image](https://github.com/PNg-HA/CTFs/assets/93396414/283919b3-836b-4117-860a-fa7c4651466c)
The text in instrucstion.txt: `GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
`
Paste it to the Rot13 https://rot13.com/: `TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN`. Just another hint that there is a means to hide data in TFTP, which is a plaintext-data-transfer protocol.

