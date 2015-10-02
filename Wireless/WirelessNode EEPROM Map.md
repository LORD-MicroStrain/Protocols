# Wireless Node EEPROM Map

#### Standard Settings

| EEPROM Address    | Option                            | Type   | Valid Values | Description                                                                                              | Min FW Version |
|-------------------|-----------------------------------|--------|--------------|----------------------------------------------------------------------------------------------------------|----------------|
| 0                 | Current Datalogging Page          | `uint16` |              | The flash memory page that will be used for the next datalogging session. If current page offset >= 264, multiply by 2 and add 1, else multiply by 2. Do Not Change. | 1.00           |
| 2                 | Current Datalogging Page Offset   | `uint16` |              | The byte offset for the next datalogging session. If current page offset >= 264, subtract 264. Do Not Change. | 1.00           |
| 4                 | # of Datalogging Sessions Stored  | `uint16` |              | The number of datalogging sessions (triggers) stored in flash memory. Do Not Change.                     | 1.00           |
| 6                 | (LEGACY) Sensor Trigger Value     | `uint16` |              |                                                                                                          | 1.00           |
| 8                 | (LEGACY) Sensor Trigger Channel   | `uint16` |              |                                                                                                          | 1.00           |
| 10                | (LEGACY) Sensor Trigger Type      | `uint16` |              |                                                                                                          | 1.00           |
| 12                | Active Channel Mask               | `uint16` | see notes    | The channels that are enabled/disabled for sampling.                                                     | 1.00           |
| 14                | Datalogging Sample Rate           | `uint16` | see notes    | The sample rate for Armed Datalogging sampling.                                                          | 1.00           |
| 16                | # of Sweeps                       | `uint16` |              | The number of sweeps (samples per data set) to sample for.                                               | 1.00           |
| 18                | Default Mode                      | `uint16` | see notes    | The default mode to perform on startup and user inactivity timeout.                                      | 1.00           |
| 20                | Serial ID                         | `uint32` |              | The serial id for the device. Combine with the model number and model option for the full Serial Number. | 1.00           |
| 24                | Sampling Mode                     | `uint16` | see notes    | The sampling mode that the device was last placed in (needs to be user updated).                         | 1.00           |
| 26                | Hardware Offset 1                 | `uint16` |              | The hardware offset for balancing the sensors output and compensating for sensor offset. (1)             | 1.00           |
| 28                | Hardware Offset 2                 | `uint16` |              | The hardware offset for balancing the sensors output and compensating for sensor offset. (2)             | 1.00           |
| 30                | Hardware Offset 3                 | `uint16` |              | The hardware offset for balancing the sensors output and compensating for sensor offset. (3)             | 1.00           |
| 32                | Hardware Offset 4                 | `uint16` |              | The hardware offset for balancing the sensors output and compensating for sensor offset. (4)             | 1.00           |
| 34                | Sampling Delay                    | `uint16` | see notes    | The delay to use before sampling, for low-impedance sensors with slow rise/settling times.               | 1.00           |
| 36                | TDMA Address                      | `uint16` |              | The TDMA Address for Synchronized Sampling.                                                              | 7.00           |
| 38                | Data Collection Mode              | `uint16` | see notes    | The Data collection mode for Non-Sync and Sync Sampling.                                                 | 1.00           |
| 40                | # of Buffered Packets             | `uint16` | 1 - 48       | The payload packet size for Non-Sync sampling.                                                           | 7.00           |
| 44                | # of Retransmission Attempts      | `uint16` |              | The number of retransmission attempts during Lossless sampling before entering a low-power state.        | 7.00           |
| 46                | Model Number                      | `uint16` |              | The model number of the device.                                                                          | 8.00           |
| 48                | Model Option                      | `uint16` |              | The model option of the device.                                                                          | 8.00           |
| 50                | Node Address                      | `uint16` | 1 - 65534    | The address of the device.                                                                               | 1.00           |
| 56                | (LEGACY) Calibration              | `uint16` |              | (LEGACY) Used in performing an onboard calibration of strain sensors.                                    | 1.00           |
| 66                | Set to Idle Interval              | `uint16` | see notes    | How often the Node wakes up and listens for a 'set to idle' command.                                     | 1.00           |
| 70                | User Inactivity Timeout           | `uint16` | 5 - 65535    | The time, in seconds, before a Node enters sleep mode, if there is no user activity.                     | 1.00           |
| 72                | Sample Rate                       | `uint16` | see notes    | The sample rate for Non-Sync and Sync Sampling.                                                          | 1.00           |
| 74                | Auto Balance Interval             | `uint16` |              |                                                                                                          | 1.00           |
| 76                | Data Format                       | `uint16` | see notes    | The format that data is transferred in for Non-Sync and Sync Sampling modes.                             | 1.00           |
| 78                | Sniff Duration                    | `uint16` | 1 - 50       | The amount of time the Node listens for a Set to Idle packet for each check (see Set to Idle Interval).  | 1.00           |
| 80                | (LEGACY) Manual Trigger Config    | `uint16` |              |                                                                                                          | 1.00           |
| 82                | Clock Timer Control               | `uint16` | 0 - 15       | Internal Use Only. Do Not Change.                                                                        | 1.00           |
| 88                | Radio Broadcast Filter            | `uint16` |              | Prevents the node from hearing "broadcast" packets in certain modes. 0 = disabled, 1 = sleep mode        | 7.00           |
| 90                | Radio Frequency                   | `uint16` | 11 - 26      | The radio frequency of the device. Needs to be on the same frequency as the BaseStation to communicate with it. | 1.00           |
| 94                | [Transmit Power Level](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/WirelessIDs.md#transmit-power) | `uint16` | see notes    | The transmit output power of the radio.                                                                  | 1.00           |
| 96                | Return Node Address               | `uint16` | 4660         | Internal Use. Do Not Change.                                                                             | 1.00           |
| 100               | Unlimited Sampling                | `uint16` | 0 - 1        | Enables (1) or Disables (0) unlimited duration of Non-Sync and Sync Sampling.                            | 1.00           |
| 102               | Unlimited Armed Datalogging       | `uint16` | 0 - 1        | Enables (1) or Disables (0) unlimited duration of Armed Datalogging Sampling.                            | 1.00           |
| 108               | [Firmware Version (1)](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/WirelessIDs.md#firmware-version) | `uint16` | see notes    | The firmware version of the device (Part 1).                                                             | 4.00           |
| 110               | [Firmware Version (2)](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/WirelessIDs.md#firmware-version) | `uint16` | see notes    | The firmware version of the device (Part 2).                                                             | 4.00           |
| 112               | (LEGACY) Model Number             | `uint16` |              | (LEGACY, Replaced by EEPROMs 46 + 48) The model number of the device.                                    | 1.00           |
| 114               | (LEGACY) Serial ID                | `uint16` |              | (LEGACY, Replaced by EEPROM 20) The serial id for the device.                                            | 1.00           |
| 116               | Max Memory                        | `uint16` |              | The maximum number of pages available on the flash memory.                                               | 1.00           |
| 118               | Radio ID                          | `uint16` |              | The id of the radio on the device.                                                                       | 1.00           |
| 120               | Microcontroller ID                | `uint16` |              | The id of the microcontroller on the device.                                                             | 1.00           |
| 122               | Firmware Arch Version             | `uint16` |              | The architecture version of the device used to determine which version of firmware can be applied to it. | 3.00           |
| 128               | Hardware Gain 1                 | `uint16` |              | The hardware gain for applied to the Node. (1)             | 1.00           |
| 130               | Hardware Gain 2                 | `uint16` |              | The hardware gain for applied to the Node. (2)             | 1.00           |
| 132               | Hardware Gain 3                 | `uint16` |              | The hardware gain for applied to the Node. (3)             | 1.00           |
| 134               | Hardware Gain 4                 | `uint16` |              | The hardware gain for applied to the Node. (4)             | 1.00           |
| 150               | Action ID - Ch1                 | `uint16` | see notes    | The action id (unit and equation) for channel 1.           | 1.00           |
| 152               | Slope - Ch1                     | `float` |               | The slope for channel 1.                                   | 1.00           |
| 156               | Offset - Ch1                    | `float` |               | The offset for channel 1.                                  | 1.00           |
| 160               | Action ID - Ch2                 | `uint16` | see notes    | The action id (unit and equation) for channel 2.           | 1.00           |
| 162               | Slope - Ch2                     | `float` |               | The slope for channel 2.                                   | 1.00           |
| 166               | Offset - Ch2                    | `float` |               | The offset for channel 2.                                  | 1.00           |
| 170               | Action ID - Ch3                 | `uint16` | see notes    | The action id (unit and equation) for channel 3.           | 1.00           |
| 172               | Slope - Ch3                     | `float` |               | The slope for channel 3.                                   | 1.00           |
| 176               | Offset - Ch3                    | `float` |               | The offset for channel 3.                                  | 1.00           |
| 180               | Action ID - Ch4                 | `uint16` | see notes    | The action id (unit and equation) for channel 4.           | 1.00           |
| 182               | Slope - Ch4                     | `float` |               | The slope for channel 4.                                   | 1.00           |
| 186               | Offset - Ch4                    | `float` |               | The offset for channel 4.                                  | 1.00           |
| 190               | Action ID - Ch5                 | `uint16` | see notes    | The action id (unit and equation) for channel 5.           | 1.00           |
| 192               | Slope - Ch5                     | `float` |               | The slope for channel 5.                                   | 1.00           |
| 196               | Offset - Ch5                    | `float` |               | The offset for channel 5.                                  | 1.00           |
| 200               | Action ID - Ch6                 | `uint16` | see notes    | The action id (unit and equation) for channel 6.           | 1.00           |
| 202               | Slope - Ch6                     | `float` |               | The slope for channel 6.                                   | 1.00           |
| 206               | Offset - Ch6                    | `float` |               | The offset for channel 6.                                  | 1.00           |
| 210               | Action ID - Ch7                 | `uint16` | see notes    | The action id (unit and equation) for channel 7.           | 1.00           |
| 212               | Slope - Ch7                     | `float` |               | The slope for channel 7.                                   | 1.00           |
| 216               | Offset - Ch7                    | `float` |               | The offset for channel 7.                                  | 1.00           |
| 220               | Action ID - Ch8                 | `uint16` | see notes    | The action id (unit and equation) for channel 8.           | 1.00           |
| 222               | Slope - Ch8                     | `float` |               | The slope for channel 8.                                   | 1.00           |
| 226               | Offset - Ch8                    | `float` |               | The offset for channel 8.                                  | 1.00           |
| 230               | Bootload Page Address           | `uint16` |              | Internal Use Only. Do Not Change.                          | 1.00           |
| 232               | Bootload Enable Flag            | `uint16` |              | Internal Use Only. Do Not Change.                          | 1.00           |
| 234               | Bootload Checksum               | `uint16` |              | Internal Use Only. Do Not Change.                          | 1.00           |
| 236               | Bootload Version                | `uint16` |              | Internal Use Only. Do Not Change.                          | 1.00           |
| 238               | Bootload Options                | `uint16` |              | Internal Use Only. Do Not Change.                          | 1.00           |
| 240               | Bootload Counter                | `uint16` |              | Internal Use Only. Do Not Change.                          | 1.00           |
| 246               | Reset Counter                   | `uint16` |              | Records the number  of times the device has been reset (both soft reset and power cycling).              | 1.00           |
| 248               | Brown Out Reset Enable          | `uint16` |              | Enables (1) or Disables (0) the brown out reset function of the microcontroller during sleep.  If a value of 0 is used, the brown out reset is disabled during sleep.  This will result in the lowest sleep power consumption, but it may be difficult to turn off or reset a sleeping node.  (The power switch may need to be placed in the off position for up to 30 seconds).  If any non zero value is written, the brown out reset will be enabled during sleep.  This will add approximately 40 uA to the overall sleep current, but the node will turn off immediately when the switch is powered off. | 1.00           |
| 250               | [Cycle Power](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/BaseStationCommands.md#cycle-power--radio) | `uint16` | see notes    | Used to cycle the power on the device.                                                                   | 1.00           |
| 258               | Radio Options                   | `uint16` |              | The radio options of the Node.              | 1.00           |
| 260               | Lost Beacon Timeout             | `uint16` |              | Set a value in minutes between 2 and 600.  If a node is in synchronized sampling mode and loses the beacon for a length of time greater than this value, then the node drops into a sleep mode.  The node will re-enter synchronized sampling within 2 minutes of the beacon re-appearing.  This feature is disabled when the value entered in the field is greater than 600.              | 1.00           |
| 280               | [Region Code](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/WirelessIDs.md#region-code) | `uint16` | see notes    | The region the device will be operated in.                                                               | 3.00           |

#### Node Specific Settings

| EEPROM Address    | Option                            | Type   | Valid Values | Description                                                                                              | Min FW Version |
|-------------------|-----------------------------------|--------|--------------|----------------------------------------------------------------------------------------------------------|----------------|
| 130               | Filter (1)                        | `uint16` |            | The first filter value for nodes with filter functionality (ie. TC-Link)             | 1.00           |
| 134               | Filter (2)                        | `uint16` |            | The second filter value for nodes with 2 filter functionality (ie. ENV-Link Pro)             | 1.00           |
