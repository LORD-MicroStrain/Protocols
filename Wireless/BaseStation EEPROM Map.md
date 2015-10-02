# Base Station EEPROM Map

#### Standard Settings

| EEPROM Address    | Option                            | Type   | Valid Values | Description                                                                                              | Min FW Version |
|-------------------|-----------------------------------|--------|--------------|----------------------------------------------------------------------------------------------------------|----------------|
| 20                | Serial ID                         | uint32 |              | The serial id for the device. Combine with the model number and model option for the full Serial Number. | 1.00           |
| 40                | Beacon Configuration              | uint16 |              |                                                                                                          | 1.00           |
| 46                | Model Number                      | uint16 |              | The model number of the device.                                                                          | 3.00           |
| 48                | Model Option                      | uint16 |              | The model option of the device.                                                                          | 3.00           |
| 50                | Base Station Address              | uint16 | 4660         | The address of the device. This is the same for all Base Stations. Do Not Change.                        | 1.00           |
| 90                | Radio Frequency                   | uint16 | [11 - 26]    | The radio frequency of the device. Nodes on this same frequency can be communicated with.                | 1.00           |
| 94                | Transmit Power Level              | uint16 | see notes    | The transmit output power of the radio.                                                                  | 1.00           |
| 96                | Beacon Source                     | uint16 | see notes    | The source of the beacon clock.                                                                          | 3.00           |
| 108               | Firmware Version (1)              | uint16 | see notes    | The firmware version of the device (Part 1).                                                             | 4.00           |
| 110               | Firmware Version (2)              | uint16 | see notes    | The firmware version of the device (Part 2).                                                             | 4.00           |
| 112               | (LEGACY) Model Number             | uint16 |              | (LEGACY, Replaced by EEPROMs 46 + 48) The model number of the device.                                    | 1.00           |
| 114               | (LEGACY) Serial ID                | uint16 |              | (LEGACY, Replaced by EEPROM 20) The serial id for the device.                                            | 1.00           |
| 118               | Radio ID                          | uint16 |              | The id of the radio on the device.                                                                       | 1.00           |
| 120               | Microcontroller ID                | uint16 |              | The id of the microcontroller on the device.                                                             | 1.00           |
| 122               | Firmware Arch Version             | uint16 |              | The architecture version of the device used to determine which version of firmware can be applied to it. | 3.00           |
| 238               | LED Action                        | uint16 | see notes    | Controls the LED action of the device.                                                                   | 2.27           |
| 242               | Reset Counter                     | uint16 |              | Records the number  of times the device has been reset (both soft reset and power cycling).              | 1.00           |
| 250               | Cycle Power                       | uint16 | see notes    | Used to cycle the power on the device.                                                                   | 1.00           |
| 280               | Region Code                       | uint16 | see notes    | The region the device will be operated in.                                                               | 3.00           |

#### Analog Settings

| EEPROM Address    | Option                            | Type   | Valid Values | Description                                                                                              | Min FW Version |
|-------------------|-----------------------------------|--------|--------------|----------------------------------------------------------------------------------------------------------|----------------|
| 128               | Analog Port 1 - Node Address      | uint16 |              | The node address to associate with analog out, port 1.                                                   | 3.00           |
| 130               | Analog Port 1 - Channel           | uint16 |              | The node channel number to associate with analog out, port 1.                                            | 3.00           |
| 132               | Analog Port 1 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 1.                           | 3.00           |
| 136               | Analog Port 1 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 1.                           | 3.00           |
| 140               | Analog Port 2 - Node Address      | uint16 |              | The node address to associate with analog out, port 2.                                                   | 3.00           |
| 142               | Analog Port 2 - Channel           | uint16 |              | The node channel number to associate with analog out, port 2.                                            | 3.00           |
| 144               | Analog Port 2 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 2.                           | 3.00           |
| 148               | Analog Port 2 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 2.                           | 3.00           |
| 152               | Analog Port 3 - Node Address      | uint16 |              | The node address to associate with analog out, port 3.                                                   | 3.00           |
| 154               | Analog Port 3 - Channel           | uint16 |              | The node channel number to associate with analog out, port 3.                                            | 3.00           |
| 156               | Analog Port 3 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 3.                           | 3.00           |
| 160               | Analog Port 3 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 3.                           | 3.00           |
| 164               | Analog Port 4 - Node Address      | uint16 |              | The node address to associate with analog out, port 4.                                                   | 3.00           |
| 166               | Analog Port 4 - Channel           | uint16 |              | The node channel number to associate with analog out, port 4.                                            | 3.00           |
| 168               | Analog Port 4 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 4.                           | 3.00           |
| 172               | Analog Port 4 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 4.                           | 3.00           |
| 176               | Analog Port 5 - Node Address      | uint16 |              | The node address to associate with analog out, port 5.                                                   | 3.00           |
| 178               | Analog Port 5 - Channel           | uint16 |              | The node channel number to associate with analog out, port 5.                                            | 3.00           |
| 180               | Analog Port 5 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 5.                           | 3.00           |
| 184               | Analog Port 5 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 5.                           | 3.00           |
| 188               | Analog Port 6 - Node Address      | uint16 |              | The node address to associate with analog out, port 6.                                                   | 3.00           |
| 190               | Analog Port 6 - Channel           | uint16 |              | The node channel number to associate with analog out, port 6.                                            | 3.00           |
| 192               | Analog Port 6 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 6.                           | 3.00           |
| 196               | Analog Port 6 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 6.                           | 3.00           |
| 200               | Analog Port 7 - Node Address      | uint16 |              | The node address to associate with analog out, port 7.                                                   | 3.00           |
| 202               | Analog Port 7 - Channel           | uint16 |              | The node channel number to associate with analog out, port 7.                                            | 3.00           |
| 204               | Analog Port 7 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 7.                           | 3.00           |
| 208               | Analog Port 7 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 7.                           | 3.00           |
| 212               | Analog Port 8 - Node Address      | uint16 |              | The node address to associate with analog out, port 8.                                                   | 3.00           |
| 214               | Analog Port 8 - Channel           | uint16 |              | The node channel number to associate with analog out, port 8.                                            | 3.00           |
| 216               | Analog Port 8 - Max Float         | float  |              | The maximum float value if converting from float data with analog out, port 8.                           | 3.00           |
| 220               | Analog Port 8 - Min Float         | float  |              | The minimum float value if converting from float data with analog out, port 8.                           | 3.00           |
| 224               | Analog Out Enable                 | uint16 | [0 - 1]      | Whether analog pairing is enabled (1) or disabled (0).                                                   | 3.00           |
| 226               | Analog Out Timeout - Time         | uint16 |              | The number of seconds before an analog out port times out (0 disables timeout).                          | 3.00           |
| 228               | Analog Out Timeout - Voltage      | float  | [0.0 - 3.0]  | The voltage that the port will go to once it times out.                                                  | 3.00           |
| 348               | Analog Exceedance - Max           | float  |              | The maximum value for the analog exceedance setting.                                                     | 3.00           |
| 352               | Analog Exceedance - Min           | float  |              | The minimum value for the analog exceedance setting.                                                     | 3.00           |
| 356               | Analog Exceedance Enable          | uint16 | [0 - 1]      | Whether analog exceedance is enabled (1) or disabled (0).                                                | 3.00           |

#### Button Settings

| EEPROM Address    | Option                            | Type   | Valid Values | Description                                                                                              | Min FW Version |
|-------------------|-----------------------------------|--------|--------------|----------------------------------------------------------------------------------------------------------|----------------|
| 232               | Button 1 - Long Press - Function  | uint16 | see notes    | The function to use when button 1 is long-pressed.                                                       | 3.00           |
| 234               | Button 1 - Long Press - Node      | uint16 |              | The node address associated with button 1, long press.                                                   | 3.00           |
| 236               | Button 1 - Short Press - Function | uint16 | see notes    | The function to use when button 1 is short-pressed.                                                      | 3.00           |
| 256               | Button 1 - Short Press - Node     | uint16 |              | The node address associated with button 1, short press.                                                  | 3.00           |
| 258               | Button 2 - Long Press - Function  | uint16 | see notes    | The function to use when button 2 is long-pressed.                                                       | 3.00           |
| 260               | Button 2 - Long Press - Node      | uint16 |              | The node address associated with button 2, long press.                                                   | 3.00           |
| 262               | Button 2 - Short Press - Function | uint16 | see notes    | The function to use when button 2 is short-pressed.                                                      | 3.00           |
| 264               | Button 2 - Short Press - Node     | uint16 |              | The node address associated with button 2, short press.                                                  | 3.00           |