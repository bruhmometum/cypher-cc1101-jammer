# Cypher CC1101 Jammer PCB files & schematics.

### Open-source RF Pentesting Device using ESP32-WROOM ESP8266 and a CC1101 Module



### Order my PCB from PCBWay & get a $10 coupon ^_^ : https://pcbway.com/g/87Pi52

# cc1101-tool
RF tool based on CC1101 module and Arduino Pro Micro 8VMHz/3.3V. Allows using CLI to control CC1101 board over USB interface. Putty or any other serial terminal can be used. It has similar functionality to YardStick One but is cheaper and does not need specialized software. Allows for RF jamming and replay attacks as well. It has RAW  recording/replaying function which works exactly the same as in the Flipper Zero. Additional function is Radio Chat communicator

You simply connect your Arduino Pro Micro (Arduino Leonardo clone from Sparkfun) to USB port of your PC and launch Putty terminal to communicate with CC1101 module over USB Serial port ( /dev/ttyACM0 port in Linux, COMxx in Windows).

Also you may connect this device to Android OTG USB port in your smartphone for portable hacking and use USB Serial Terminal application with option CDC driver set to communicate with the device ( app : https://play.google.com/store/apps/details?id=de.kai_morich.serial_usb_terminal  ). When using Serial Terminal app on Android first go to the Settings in the app on your smartphone then upper side of the screen select "Send" and then set "Newline" as CR only. It is sending to many characters to the device and  extra character of Newline sometimes stops some of commands like "rxraw" for example.

Following commands are available :

    setmodulation <mode>         // set modulation mode. 0 = 2-FSK, 1 = GFSK, 2 = ASK/OOK, 3 = 4-FSK, 4 = MSK. 
    
    setmhz <frequency>           // Here you can set your basic frequency. default = 433.92).The cc1101 can: 300-348 MHZ, 387-464MHZ and 779-928MHZ.
    
    setdeviation <deviation>     // Set the Frequency deviation in kHz. Value from 1.58 to 380.85. Default is 47.60 kHz.
    
    setchannel <channel>         // Set the Channelnumber from 0 to 255. Default is channel 0.
    
    setchsp <spacing>            // The channel spacing is multiplied by the channel number CHAN and added to the base frequency in kHz. Value from 25.39 to 405.45. Default is 199.95 kHz. 
    
    setrxbw <Receive bandwidh>   // Set the Receive Bandwidth in kHz. Value from 58.03 to 812.50. Default is 812.50 kHz.
    
    setdrate <datarate>          // Set the Data Rate in kBaud. Value from 0.02 to 1621.83. Default is 99.97 kBaud!
    
    setpa <power value>          // Set TxPower. The following settings are possible depending on the frequency band.  (-30  -20  -15  -10  -6    0    5    7    10   11   12) Default is max!
    
    setsyncmode  <sync mode>     // Combined sync-word qualifier mode. 0 = No preamble/sync. 1 = 16 sync word bits detected. 2 = 16/16 sync word bits detected. 3 = 30/32 sync word bits detected. 4 = No preamble/sync, carrier-sense above threshold. 5 = 15/16 + carrier-sense above threshold. 6 = 16/16 + carrier-sense above threshold. 7 = 30/32 + carrier-sense above threshold.
    
    setsyncword <LOW, HIGH>      // Set sync word. Must be the same for the transmitter and receiver. (Syncword high, Syncword low)
    
    setadrchk <address check>    // Controls address check configuration of received packages. 0 = No address check. 1 = Address check, no broadcast. 2 = Address check and 0 (0x00) broadcast. 3 = Address check and 0 (0x00) and 255 (0xFF) broadcast.
    
    setaddr <address>            // Address used for packet filtration. Optional broadcast addresses are 0 (0x00) and 255 (0xFF).

    setwhitedata <whitening>     // Turn data whitening on / off. 0 = Whitening off. 1 = Whitening on.
    
    setpktformat <pkt format>    // Format of RX and TX data. 0 = Normal mode, use FIFOs for RX and TX. 1 = Synchronous serial mode, Data in on GDO0 and data out on either of the GDOx pins. 2 = Random TX mode; sends random data using PN9 generator. Used for test. Works as normal mode, setting 0 (00), in RX. 3 = Asynchronous serial mode, Data in on GDO0 and data out on either of the GDOx pins.
    
    setlengthconfig <mode>       // 0 = Fixed packet length mode. 1 = Variable packet length mode. 2 = Infinite packet length mode. 3 = Reserved 
    
    setpacketlength <mode>       // Indicates the packet length when fixed packet length mode is enabled. If variable packet length mode is used, this value indicates the maximum packet length allowed.
    
    setcrc <mode>                // 1 = CRC calculation in TX and CRC check in RX enabled. 0 = CRC disabled for TX and RX.

    setcrcaf <mode>             // Enable automatic flush of RX FIFO when CRC is not OK. This requires that only one packet is in the RXIFIFO and that packet length is limited to the RX FIFO size.

    setdcfilteroff <mode>        // Disable digital DC blocking filter before demodulator. Only for data rates ≤ 250 kBaud The recommended IF frequency changes when the DC blocking is disabled. 1 = Disable (current optimized). 0 = Enable (better sensitivity).

    setmanchester <mode>         // Enables Manchester encoding/decoding. 0 = Disable. 1 = Enable.

    setfec <mode>                // Enable Forward Error Correction (FEC) with interleaving for packet payload (Only supported for fixed packet length mode. 0 = Disable. 1 = Enable.

    setpre <mode>                // Sets the minimum number of preamble bytes to be transmitted. Values: 0 : 2, 1 : 3, 2 : 4, 3 : 6, 4 : 8, 5 : 12, 6 : 16, 7 : 24

    setpqt <mode>                // Preamble quality estimator threshold. The preamble quality estimator increases an internal counter by one each time a bit is received that is different from the previous bit, and decreases the counter by 8 each time a bit is received that is the same as the last bit. A threshold of 4∙PQT for this counter is used to gate sync word detection. When PQT=0 a sync word is always accepted.

    setappendstatus <mode>       // When enabled, two status bytes will be appended to the payload of the packet. The status bytes contain RSSI and LQI values, as well as CRC OK.

    getrssi                      // Shows radio quality information about last received RF data frame.
    
    scan <start freq> <end freq> // Scan frequency range for the highest signal and display results

    rx                           // Enable or disable printing of received RF packets on serial terminal.

    tx  <hex-vals>               // Send the packet of max 60 bytes < hex values > hex values over RF 

    jam                          // Enable or disable continous jamming on selected band with selected modulation etc... 

    brute <usec> <nb-of-bits>    // Brute force garage gate with <number-of-bits> keyword where symbol length is <microseconds>

    rec                          // Enable or disable recording frames in the buffer.
    
    show                         // Show content of recording buffer
    
    add <hex-vals>               // Manually add single frame payload (max 60 hex values) to the buffer so it can be replayed
    
    flush                        // Clear the recording buffer

    play <N>                     // Replay 0 = all frames or N-th recorded frame

    rxraw <microseconds>         // Sniffs radio by sampling with <microsecond> interval and prints received bytes in hex

    addraw <hex-vals>            // Manually add chunks (max 60 hex values) to the buffer so they can be further replayed.

    recraw <microseconds>        // Recording RAW RF data with <microsecond> sampling interval
    
    showraw                      // Showing content of recording buffer in RAW format

    showbit                      // Showing content of recording buffer in RAW format as a stream of bits.

    playraw <microseconds>       // Replaying previously recorded RAW RF data with <microsecond> sampling interval

    save                         // Store recording buffer content in non-volatile memory
    
    load                         // Load the content from non-volatile memory to the recording buffer

    echo <mode>                  // Enable or disable Echo on serial terminal. 1 = enabled, 0 = disabled
    
    chat                         // switching device into chat mode 
    
    x                            // Stops activities like jamming/receiving/recording packets
    
    init                         // Restarts CC1101 board with default parameters 
 
The code uses SmartRC library (modified Electrohouse library by Little_S@tan) which allows to customize ALL transmission parameters in human readable format without using SmartRF studio from TI (CC1101 parameter customization tool). To use it please download following ZIP library from following github link https://github.com/LSatan/SmartRC-CC1101-Driver-Lib and attach it to the script in Arduino IDE.
