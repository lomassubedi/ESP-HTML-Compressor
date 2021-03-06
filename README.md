# ESP HTML Compressor

This Python script, minifies and converts HTML,CSS and Javascript files, to an char array of hex values. Which is to be stored in the ESP progmem.

## Getting Started

Create a folder for you HTML, CSS, Javascript files to go and call it "HTML".
Make sure files only use punctuation, for the file extensions. Eg. "jquery-3.3.1.js" is not allowed, change to something like: "jquery-3_3_1.js".
Next run "Convert.py" a file called "output_dir" would appear in the root directory, with the lines of code you need to copy into you ESP32/ESP8266 project.

the lines would look something like this:
```
const char* data_bootstrap_min_css_path PROGMEM = "/bootstrap/css/bootstrap_min.css";   <- The path of the file
const char data_bootstrap_min_css[] PROGMEM = {0X67,0X63,0X61,0X70,0X74....};           <- The array of minifed code
```

Implement the data
```
#include <WiFi.h>
#include <FS.h>
#include <AsyncTCP.h>
#include <ESPAsyncWebServer.h>


//**************************** Code generated by the Python script ********************************

// /bootstrap/css/bootstrap_min.css
const char* data_bootstrap_min_css_path PROGMEM = "/bootstrap/css/bootstrap_min.css";
const char data_bootstrap_min_css[] PROGMEM = {0X2F,0X2A,0X21,0XA,0X20,0X2A,0X20,0X42,...};

// /index.html
const char* data_index_html_path PROGMEM = "/index.html";
const char data_index_html[] PROGMEM = {0X3C,0X68,0X74,0X6D,0X6C,0X20,0X6C,0X61,.....};

//**************************************************************************************************


AsyncWebServer server(80);

#define AP_SSID "MyWifiSSID"           // SSID of ESP's wifi
#define AP_PASS "********"             // Password for ESP's wifi
 
void setup(){
  Serial.begin(115200);
 
  WiFi.begin(AP_SSID, AP_PASS);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi..");
  }
  
  
  // Serve the webfiles 
  server.on("/", HTTP_GET, [](AsyncWebServerRequest *request){
    Serial.println("Index.html requested");
    request->send_P(200, "text/html", data_index_html);
  });

  server.on(data_bootstrap_min_js_path, HTTP_GET, [](AsyncWebServerRequest *request){
    Serial.println("bootstrap_min.js requested");
    request->send_P(200, "text/javascript", data_bootstrap_min_js);
  });
  server.begin();
}
 
void loop()
{
}
```
### Thanks to

 chilts - @andychilton
 for making those online tools, used in this project.
 - https://javascript-minifier.com
 - http://html-minifier.com
 - http://html-minifier.com

### Prerequisites

Only tested with Python 3.5


## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Authors

* **Gheotic** - *Initial work* - [Gheotic](https://github.com/Gheotic)

See also the list of [contributors](https://github.com/Gheotic/ESP-HTML-Compressor/graphs/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

