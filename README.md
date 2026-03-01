# ESPHOME-Havells-RFFan
Fan automation using ESPHome to automate the RF remote for havells fan
This project uses ESPHome to automate the RF remotes integrated to the Home assistant. This has been tested using Havells Stealth Air BLDC fans. 

**Required hardware:**
- ESP32 micro controller
- RF Transmitter - I recommend using STX882 433MHz transmitter with the antenna
- RF reciever - To analyze the remote codes - use to determine the code. you dont need to keep it connected in the board
- Connector wires and accessories

This setup could be used to control multiple fans. you dont need multiple devices as the range for STX882 is 100m(Make sure to connect the power to 5V instead of 3.3V for maximum performance). 

**How does the RF remote works**
RF Code Structure & Patterns
Every 32-bit code sent by the remote can be divided into three parts. Let's look at 9FB20678 (Power On) as an example:
Prefix / Device ID (First 5 Hex Digits - 9FB20): This is constant across every single button press. It identifies your specific remote/device.
Action Command (The 6th Hex Digit - 6): This single hex character determines what action the fan should take.
Rolling Counter (Last 2 Hex Digits - 78): This is a sequential counter that changes with every button press on the remote, regardless of which button is pressed.**
**The Action Mappings**
By isolating the 6th hex digit, we can perfectly map the buttons:
- Power Off: E
- Power On: 6
- Speed 1: 5
- Speed 2: F
- Speed 3: 4
- Speed 4: 3
- Speed 5: 2

**The Rolling Counter Pattern**
If you look at the last two characters across sequence presses, they cycle through 8 specific states. They increment by 0x0F (decimal 15) with every press and wrap around after 8 steps:
0F ➔ 1E ➔ 2D ➔ 3C ➔ 4B ➔ 5A ➔ 69 ➔ 78 ➔ (wraps back to 0F)

**Approach**
Instead of using the rolling codes, the code will send all the 8 codes one after another.
