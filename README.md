DataModem
=========

Data (RS-232/Serial) to Audio Modem

Usage
-----

Connect the DataModem to your computer's serial port (or USB-to-Serial adapter) and to an audio input/output device (like a cassette recorder or audio interface). Use terminal software to send and receive data through the modem.

Configuration
--------------

- **Baud Rate**: 300 baud (recommended for best reliability)
- **Tone Frequency**: Approximately 4kHz
- **RV1**: Adjusts output signal strength to the cassette recorder
- **RV2**: Adjusts the triggering sensitivity of the Schmitt trigger for playback

How It Works
------------

The DataModem uses a simple one-tone encoding system where the presence of a tone represents a 1 bit and silence represents a 0 bit.

**Recording Data**: When transmitting, a 555 timer (U2) generates a ~4kHz square wave tone when the UART input is high. The tone is buffered and AC-coupled before being fed to the cassette recorder input. When the UART input is low, the 555 is disabled and produces no tone.

**Playing Back Data**: During playback, a Schmitt trigger detects the presence of the recorded tone. A retriggerable 555 monostable circuit (U3) converts the rapid tone pulses into a steady output signal. The monostable stays on for 300μs when triggered, and continuous triggers from the 4kHz tone keep it active, producing a clean digital output that matches the original UART signal.

The circuit is designed for 300 baud operation, providing excellent reliability with minimal bit loss when properly calibrated.


Licence
-------

This project is licensed under the CERN Open Hardware Licence Version 2 - Permissive License - see the [LICENSE](LICENSE) file for details.

Credits
-------

This project is inspired by and based on the following works:

- [Datacorder](https://www.mitchelectronics.co.uk/documents/DATACORD.pdf) by Mitchell Electronics
- [UART Cassette Tape Interface](https://maker.pro/pcb/projects/make-uart-cassette-tape-interface) by Robin Mitchell