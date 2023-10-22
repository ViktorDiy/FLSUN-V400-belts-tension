Greetings to all owners of the wonderful FLSUN V400 3D printer!

I would like to share with you my development for measuring the tension of FLSUN V400 3D printer belts and monitoring it using a smart home system, including informing you about the achievement of critical tension values. 

My printer works 24/7, so it is critical for me to constantly monitor the tension of the belts. According to my observations, improper tension of the belts for 3d printers with delta kinematics significantly affects the print quality and can be harmful. 

Insufficient tension is bad because it increases the echo effect, and also, in general, reduces the quality of printing. 
It has also been observed that insufficient belt tension can significantly reduce the quality of the BED MASH. 
Excessive tension leads to rapid wear of the belts, increasing the load on the motors and bearings, which will result in faster wear and breakage. 
A very large and abrupt decrease in tension (for example, if the belt crash) leads to a strong change in the Z0 offset, which (some printer owners have observed) can lead to the breakage of the printer head, especially if it is very close to the table at that moment. It can also lead to deterioration of the surface of the PEI plate coating. 

All the methods of tension measurement known by me at the moment did not satisfy my requests, because, they looks strange from the point of view of metrology. And it is also impossible to implement monitoring, alerting, and integration with a smart home on their basis. 

After my analysis and a number of experiments with tension sensors, up to and including their integration into belt tensioners, I settled on the next most acceptable option from my point of view. 
A ready-made tension sensor from hands scales is used as a tension sensor, which can be easily placed in the printer rack. The donor of this sensor is the cheapest and most common canter scales, which can be easily bought on Aliexpress or Amazon or in local stores in your country. You can find a link to it in the general list of parts that I used in the project. 

Of course, using your imagination, you can use any other details and software that are available and convenient for you. I warn you right away that it is unlikely that you will be able to use the electronic part of the canter scales and the display for constant measurement of tension using my method, because the principle of measuring a canter scales is that first the value on the sensor is measured at zero weight, and then the value of the sensor is measured at the weight that you are measuring (if its value remains unchanged). These electronic canter scales cannot constantly measure weight/tension. 

The second main element of my project is the ESP32 development board, which is integrated with the Home Assistant smart home via ESPHome. Of course, you can develop software and hardware on ESP8266, Arduino, PlatformIO (developed in Ukraine), etc. 

ESP32 CP2102 Type-C 38 pin development board:
https://www.aliexpress.com/item/1005001636295529.html

The very common hx711 board is used as an amplifier/converter of tension measurement:
https://www.aliexpress.com/item/4000089335888.html
https://esphome.io/components/sensor/hx711
For each axis of the 3d printer we need a separate sensor and signal converter.
You should calibrate all 3 tension sensors separately and put calibration volumes in to ESPHome configuration file.

In my project I used 0.96 inch OLED IIC Serial White Display Module 128X64 I2C SSD1306 7 pin:
https://www.aliexpress.com/item/1005005563780197.html

Tension sensor donor - strain-gauge sensor from canter scales:
https://www.aliexpress.com/item/1005005627474221.html


x3 furniture coupler intersection screw M4 thread and 30mm long:
https://www.aliexpress.com/item/1005004446281911.html
https://epicentrk.ua/ua/shop/bolt-styazhnoy-dekorativnyy-mezhsektsionnyy-m4-10-sht-khrom.html


Very usefull Andreas Spiess video - https://youtu.be/iywsJB-T-mU?si=le56kaODWxQH_tsv


The finished device looks like this:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/6b900b95-a41a-49ab-9de1-971654017edd)
![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/a66871ea-0ed5-4b11-b925-bd6affa5c24b)
![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/04eebce9-2494-486e-a39e-1084fabd80ea)

You should print project details is these positions:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/a4815c73-1258-43f0-9593-d847d7233491)

Example of ESP32 pinout:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/ade8105f-7c18-4662-97ed-e6b359eb6bfc)

Sensor assembly:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/f620b8c3-9189-41b8-9741-3797119099e8)
![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/ac63c50f-3bbe-4597-9c55-33b102c43ffe)

Very lazy way for board installation:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/03e7e8b3-a43e-4bed-b33e-b700cdcdcf42)

You can reuse factory tension bolt. Put some spacer (for example x4 M4 nuts) for his length betterment.

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/fc6d47cd-ba77-4311-8b4f-fc0ab41af8c3)

You can reuse factory roller, but I prefer to use standard from Ali:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/65f64d7c-4292-4efa-a903-4714fc55fa0e)

I use separate small 5V power adapter for HX711 + ESP32 power supply (connected to 220V in printer) but you can use DC-DC step down converter (24V->5V) or may be take 5V from V400 MCU.
![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/2bd933eb-8b4a-40fa-9a95-7c752a29960d)
![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/b11de6dd-cffc-4b68-996d-7c5e874f130a)

Sensor pinout... For all my 10 scales Red wire = E+, Black = E-, colors for signal wires can be different, if during calibration you load more weight but get less volume - just swap these two wires. Sometimes they are mixed up at the factory in China.
![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/f3faf8cc-a0c2-4e51-9446-ec5c8acaa35f)

Sensor calibration pocess:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/6bdad82d-f583-4592-9a3b-ec90585bf0c1)








