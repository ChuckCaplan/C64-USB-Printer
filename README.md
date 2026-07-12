# C64-USB-Printer

**Print from a real Commodore 64 to a modern USB or Wi-Fi printer — no vintage dot-matrix required.**

This project intercepts the print output your Commodore 64 sends over the IEC bus originally destined for a 1980s printer and redirects it to a modern printer. When printing from an application like The Print Shop, the resulting page is produced on your USB or Wi-Fi printer moments later.

**How it works:**

```
  Commodore 64  ──IEC bus──▶  Arduino UNO R4 WiFi  ──USB/WiFi──▶  Raspberry Pi / Mac / PC  ──lp──▶  USB or WiFi Printer
   (hits print)               (speaks IEC protocol)                (Python: raw data ──▶ PDF)          (prints the page)
```

1. The **C64** prints as it always has, sending data out the IEC port.
2. An **Arduino UNO R4 WiFi** handles the IEC protocol handshake and forwards the raw print data.
3. A **Python script** on a Raspberry Pi (or Mac, PC, etc.) converts that raw data into a PDF and sends it to any printer via the `lp` command.

Originally forked from https://github.com/smdprutser/IEC-printer, now using [dhansel/IECDevice](https://github.com/dhansel/IECDevice) for IEC protocol communication.

Working:
 * The Print Shop: Signs, greeting cards, letterheads, and multi-page banners
 * Certificate Maker
 * Newsroom
 * GeoPaint
 * Presumably other software that prints in graphics mode to an MPS-803 printer

Not Working:
 * Text-based printing like word processors

# Project Folder Structure
 * /arduino - Arduino sketch to be uploaded to an Arduino UNO R4 Wifi to handle IEC protocol communication and send to a Python script running on a Raspberry PI (or other system) for printing.

* /scripts - A Python script that runs on a system like a Raspberry Pi Zero W and listens for raw print data from the Arduino. It then converts the raw print data to PDF and prints via the lp command.

# Installation
1. [Arduino Installation](./arduino/README.md)
2. [Python Script Installation](./scripts/README.md)

# Example
 This PDF was generated from The Print Shop on a real C64, passed to an Arduino UNO R4 Wifi, converted to PDF on a Raspberry Pi Zero W, and printed to a Brother wifi printer.\
 [![Example](examples/1760386301.316215.png)](examples/1760386301.316215.pdf)\
 Other Pics Outlining Workflow:
 * [C64 Setup](examples/1setup.jpeg)
 * [Print Shop Main Menu](examples/2ps_menu.jpeg)
 * [Print Shop Printing Screen](examples/3ps_printing.jpeg)
 * [Arduino UNO R4 Wifi (unplugged in this pic)](examples/4arduino.jpeg)
 * [Raspberry Pi Zero W](examples/5raspberrypi.jpeg)
 * [Printer](examples/6printer.jpeg)
 * [Printout](examples/7printout.jpeg)




# Printer Support
This project currently supports the [Commodore MPS-803](https://www.historybit.it/wp-content/uploads/2020/06/Manual_MPS-803.pdf) printer, but could be extended to support other printers with some additional work. It also only supports graphics mode. Text mode, including PETSCII characters and control codes for underlining, bold, etc. is not currently supported. This was tested with Broderbund The Print Shop and Springboard Certificate Maker printing to what the C64 thought was an MPS-803 printer.

# License
This code is distributed under the GNU Public License which can be found at http://www.gnu.org/licenses/gpl.txt

# DISCLAIMER:
The author is in no way responsible for any problems or damage caused by using this code. Use at your own risk.
