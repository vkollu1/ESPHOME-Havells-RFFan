# ESPHOME-Havells-RFFan
Fan automation using ESPHome to automate the RF remote for havells fan
This project uses ESPHome to automate the RF remotes integrated to the Home assistant. This has been tested using Havells Stealth Air BLDC fans. 

**Required hardware:**
- ESP32 micro controller
- RF Transmitter - I recommend using STX882 433MHz transmitter with the antenna
- RF reciever - To analyze the remote codes - use to determine the code. you dont need to keep it connected in the board
- Connector wires and accessories

This setup could be used to control multiple fans. you dont need multiple devices as the range for STX882 is 100m(Make sure to connect the power to 5V instead of 3.3V for maximum performance). 
