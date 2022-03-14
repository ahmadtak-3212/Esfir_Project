# Design
- There are 3 components to this design server, database and esp client:
  ![C++ Extension](https://github.com/ahmadtak-3212/Smart_Lamp/blob/main/writeup_resources/smart_lamp.png?raw=true)
## Server Side
- From the server side their are 2 endpoints the server.py (http://608dev-2.net/sandbox/sc/ahmadtak/server/home.py) endpoint and home.py (http://608dev-2.net/sandbox/sc/ahmadtak/server/home.py) endpoint.
- Navidgating to the home.py enpoint will open the web-ui for chaing the color of the led this US is hard coded as a global variable in the home.py sript.  It references exterenal CSS and JS Files from CDN (bootstrap and jquary)
- Once the user clicks the submit button they are making a post request (see picture below) to the home.py endpoint. This request is processed by posting the rgb values to the database. 
- ![image](https://user-images.githubusercontent.com/78754327/158101948-c3f650f5-e215-4354-93bb-d7a914dad59b.png)

