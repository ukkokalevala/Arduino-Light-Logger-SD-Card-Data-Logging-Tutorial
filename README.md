This tutorial demonstrates how to interface a photoresistor (LDR) and a microSD card module with an Arduino Nano to build a standalone light-level data logger. The LDR and a 10 kΩ resistor form a voltage divider, producing an analog voltage proportional to incident light intensity, which is sampled on analog input A0 and converted to a 10-bit value (0–1023). At a configurable interval, the firmware appends a timestamped record to a CSV file on the microSD card via the SPI bus. The SD card module is wired as follows: VCC→5V, GND→GND, CS→D10, MOSI→D11, MISO→D12, SCK→D13. A 1-second delay is implemented before SD.begin() to allow the card's onboard regulator and level shifter to stabilize — a critical step for reliable initialization on many modules. The resulting light.csv file contains three columns (uptime in seconds, raw ADC value, and percentage), suitable for import into Excel or Google Sheets for graphing. The same firmware framework can be adapted to other analog or digital sensors by changing the sensor input and the conversion math.

Specifications Summary
Parameter	Value
Microcontroller	Arduino Nano (ATmega328P)
Sensor	LDR + 10 kΩ voltage divider
Analog input	A0 (10-bit ADC, 0–1023)
Storage	microSD via SPI (FAT16/FAT32, ≤32 GB)
SD pin mapping	CS→D10, MOSI→D11, MISO→D12, SCK→D13
Log interval	Configurable (default 10 s test / 60 s production)
Output format	CSV (uptime_s, light_raw, light_percent)
Initialization requirement	1 s delay before SD.begin()
