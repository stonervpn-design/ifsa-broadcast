# NFC version — Feline Emergency Broadcast

Tap-to-open NFC payload that launches the broadcast page:
**https://stonervpn-design.github.io/ifsa-broadcast/**

## `feline-broadcast-ntag215.nfc`
A Flipper Zero **NTAG215** dump containing a single **NDEF URI record** for the page.

- **Write to a real tag:** Flipper → NFC → load this file → **Write** onto a blank NTAG213/215/216.
- **Emulate (no tag needed):** Flipper → NFC → load → **Emulate**, then tap a phone to it.
- Most phones open the URL automatically on tap.

## Write it with anything else
It's just an NDEF URI record for the URL above — write the same URL with any tool:
- Phone app (NFC Tools, etc.) → Write → URL/URI → paste the link.
- **Bruce** (with a PN532) → NFC → write an NDEF URL.

Raw NDEF URI record (hex): `D1 01 2B 55 04 73 74 6F 6E 65 72 76 70 6E 2D 64 65 73 69 67 6E 2E 67 69 74 68 75 62 2E 69 6F 2F 69 66 73 61 2D 62 72 6F 61 64 63 61 73 74 2F`
(`D1 01 <len> 55 04` = NDEF well-known URI record, prefix `04` = `https://`.)

## Bruce version — `feline-broadcast-bruce.nfc`
Native Bruce format (`Filetype: Bruce RFID File`, NTAG215) with the same NDEF URL. Copy it to your SD card's `/nfc` folder, then on the device:
**NFC → Load File → feline-broadcast-bruce → Emulate** (tap a phone) or **Write** (onto a blank NTAG213/215/216).

### Hardware note (T-Embed CC1101 Plus)
NFC is 13.56 MHz; the **CC1101 is sub-GHz**, so the T-Embed CC1101 Plus has **no built-in NFC**. To use this on it you must attach an NFC reader — **PN532** (I2C or SPI), RC522, or an M5 RFID2 — and set its pins in Bruce (Config → Pins → PN532/RFID). With no NFC module attached, no `.nfc` can be written or emulated on that device.
