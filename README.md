Greetings to all owners of the wonderful FLSUN V400 3D printer!

I would like to share with you my development for measuring the tension of FLSUN V400 3D printer belts and monitoring it using a smart home system, including informing you about the achievement of critical tension values. 

My printer works 24/7, so it is critical for me to constantly monitor the tension of the belts. According to my observations, improper tension of the belts for 3d printers with delta kinematics significantly affects the print quality and can be harmful. 

Insufficient tension is bad because it increases the echo effect, and also, in general, reduces the quality of printing. 
It has also been observed that insufficient belt tension can significantly reduce the quality of the BED MASH. 
Excessive tension leads to rapid wear of the belts, increasing the load on the motors and bearings, which will result in faster wear and breakage. 
A very large and abrupt decrease in tension (for example, if the belt crash) leads to a strong change in the Z0 offset, which (some printer owners have observed) can lead to the breakage of the printer head, especially if it is very close to the table at that moment. It can also lead to deterioration of the surface of the PEI plate coating. 

All the methods of tension measurement known by me at the moment did not satisfy my requests, because, they looks strange from the point of view of metrology. And it is also impossible to implement monitoring, alerting, and integration with a smart home on their basis. 

After my analysis and a number of experiments with tension sencors, up to and including their integration into belt tensioners, I settled on the next most acceptable option from my point of view. 
A ready-made tension sensor from hands scales is used as a tension sensor, which can be easily placed in the printer rack. The donor of this sensor is the cheapest and most common canter scales, which can be easily bought on Aliexpress or Amazon or in local stores in your country. You can find a link to it in the general list of parts that I used in the project. 

Of course, using your imagination, you can use any other details and software that are available and convenient for you. I warn you right away that it is unlikely that you will be able to use the electronic part of the canter scales and the display for constant measurement of tension using my method, because the principle of measuring a canter scales is that first the value on the sensor is measured at zero weight, and then the value of the sensor is measured at the weight that you are measuring (if its value remains unchanged). These electronic canter scales cannot constantly measure weight/tension. 

The second main element of my project is the ESP32 development board, which is integrated with the Home Assistant smart home via ESPHome. Of course, you can develop software and hardware on ESP8266, Arduino, PlatformIO (developed in Ukraine), etc. 

The very common hx711 board is used as an amplifier/converter of tension measurement.

For each axis of the 3d printer we need a separate sensor and signal converter.

The finished device looks like this:

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/12dd6dcd-d8ab-4eff-b0ed-8e984e096084)

![image](https://github.com/ViktorDiy/FLSUN-V400-belts-tension/assets/147925158/d0b93d50-dc21-419d-960d-e5a96a806bfb)


