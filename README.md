# laser-m01-esp32
[Leer en Español](README_ESP.md)

Integration of a high-precision laser distance measurement module into an ESP32 Wemos Lolin32 development board.

Laser Range Module (M01, 6 pins) with ESP32 (LOLIN32)

Integration of a high-precision laser distance measurement module into an ESP32 Wemos Lolin32 development board.

Materials: 50m Laser ranging sensor module from Liancheng Electronics (AliExpress).

Minimal and functional example to read distances via UART from an M01 laser module (6-pin board) using an ESP32 (Wemos LOLIN32).
Keys: Q (measure), L (laser ON), K (laser OFF), R (module reset).

Hardware
•	M01 laser module (6-pin board). Liancheng Electronics (Shenzhen) Co., Ltd. Store) AliExpress
•	ESP32 Wemos LOLIN32 (any ESP32 will work).
•	3.3 V Power supply (min. ~150 mA recommended).
•	Dupont cables / soldering.

Module Pinout (top → bottom)
1.	MIN (3V3) – 3.3 V power supply
2.	ENA – enable (active high)
4.	GND – ground
5.	RXD – module UART input
6.	TXD – module UART output
7.	NC

Wiring Colors (according to manufacturer)
•	Red = MIN (3V3)
•	Black = GND
•	Green = RXD (module)
•	Yellow = TXD (module)

Note: Module TX → ESP32 RX, Module RX ← ESP32 TX (crossed).

Recommended Connection (ESP32 LOLIN32)
•	Red (MIN) → 3V3
•	Black (GND) → GND
•	Yellow (module TXD) → GPIO33 (ESP32 RX)
•	Green (module RXD) ← GPIO32 (ESP32 TX)
•	ENA (if accessible) → GPIO5 set to HIGH (or direct to 3V3)
If your harness only has 4 wires (red/black/green/yellow), ENA is usually integrated high or must be connected.

________________________________________
Usage
1.	Upload the sketch and open Serial Monitor at 115200 baud.
2.	Point the laser at a matte wall (2–4 m) with a dark background.
3.	Press:
o	L → turn on laser.
o	Q → quick reading (shows X.XXX).
o	K → turn off laser.
o	R → restart the module (cuts and restores ENA).
Note: The emitter is usually infrared; the "dot" is not visible to the naked eye. It can be seen using a phone camera.

________________________________________
Quick Troubleshooting (if no data on RX)
•	Crossed wires: Yellow (module TXD) → ESP32 RX; Green (module RXD) ← ESP32 TX.
•	Common GND between module and ESP32.
•	ENA high (GPIO5 HIGH or 3V3).
•	Cable loopback (express test): Bridge green ↔ yellow on the module connector; whatever the ESP32 sends should return identical via RX. If there's no echo → check soldering/continuity on GPIO33/GPIO32 ↔ connector.
•	If your unit is set to 115200, change LZR.begin(9600, ...) to 115200.

________________________________________
Safety
•	It is IR (≈905–940 nm). Do not point at eyes or nearby reflective surfaces.

________________________________________
Acknowledgements
We especially appreciate the collaboration and support of Liancheng Electronics (Shenzhen) Co., Ltd. Store, which provided the harness color scheme and helped resolve RX/TX connection issues.
Store link: https://www.aliexpress.com/store/1104805174?spm=a2g0o.order_list.order_list_main.8.21ef194dfoSHNu
