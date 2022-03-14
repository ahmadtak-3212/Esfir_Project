# Design
- There are 3 components to this design server, database and esp client:
  ![C++ Extension](https://github.com/ahmadtak-3212/Smart_Lamp/blob/main/writeup_resources/smart_lamp.png?raw=true)
## Server Side
### WEB UI
- From the server side their are 2 endpoints the server.py (http://608dev-2.net/sandbox/sc/ahmadtak/server/home.py) endpoint and home.py (http://608dev-2.net/sandbox/sc/ahmadtak/server/home.py) endpoint.
- Navigating to the home.py enpoint will open the web-ui for changing the color of the led. The HTML is hard coded as a global variable in the home.py sript. It references exterenal CSS and JS Files from CDN (bootstrap and jquary)
- Once the user clicks the submit button they are making a post request (see picture below) to the home.py endpoint. This request parses the form data, extracting the rgb values, and placing them on the database under the colors table (see section on database)
![image](https://user-images.githubusercontent.com/78754327/158101948-c3f650f5-e215-4354-93bb-d7a914dad59b.png)

### ESP32 CLIENT
- Once the database has updated values, a get request from the esp32 client is made to the server.py endpoint. 
- Server.py then processes this get request by finding the latest posted rgb value (Makes a sql query and orders by timestamp). Once the request is made it then returns the value as a string to esp32 ("{r},{g},{b}"). 
## Database
- Our database table contains 4 columns (red, green, blue, and timestamp).
- Everytime a post request is made it populates a row in this table

![image](https://user-images.githubusercontent.com/78754327/158104619-4153eaf0-bdc8-4362-9322-34b816ffd12f.png)

## Esp32 Client
- The esp32 makes periodic get requests to the every RESPONSE_INTERVAL (line 19 of RESPONSE INTERVAL) milliseconds 
- Once a get request is made it returns a response from server.py in the format mentioned above this is then processed into three integers representing red green and blue values. Each value is then written to one of the 3 pwm channels tied to the pins of the led.
- Since it is active low we are actually writing 255 minus the value from the database. 
- Another caveat green overpowers other colors when all values are the same. To compensate for this I multipled the green value written to the pwm channel by 0.9 effectively reducing greens brightness by 10% to even it out with the other colors. 
# Final Notes
I had a lot of fun doing this excersise it was really cool seing it work!
link to video: https://youtu.be/NfWi4lIguIc

