# Arduino-cli-setup

  Download the pre-built binaries for your supported platform
  
  Extract the downloaded file to a directory already in your path or add the Arduino CLI installation path to your PATH environment variable.
 
  
  # Use the install scripts
   The script requires sh. This is always available on Linux and macOS. sh is not available by default on Windows. The script may be run on Windows by installing    Git for Windows, then running it from Git Bash.
   
   This script will install the latest version of Arduino CLI to $PWD/bin:
     
     curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh
     
   If you want to target a different directory, for example ~/local/bin, set the BINDIR environment variable like this:
   
    curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | BINDIR=~/local/bin sh
    
   If you would like to use the arduino-cli command from any location, install Arduino CLI to a directory already in your PATH or add the Arduino CLI installation path to your PATH environment variable.
   
   If you want to download a specific arduino-cli version, for example 0.9.0, pass the version number as a parameter like this:
   
     curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh -s 0.9.0
     
  # To add to the path on a Mac OS:
  
   1. Open your Terminal.
   
   2. Run the command:              
   
    sudo nano /etc/paths
   
   3. Enter your password, when required.
   
   4. Go to the bottom of the file, and enter the path you wish to add.
   
   5. Hit control-x to quit.
   
   6. Enter "Y" to save the modified buffer.
  
  
   Open new window and run the code to see if you have successfully installed the script
   
      arduino-cli help core
     
     
     Arduino core operations.

     Usage:
       arduino-cli core [command]

    Examples:
      arduino-cli core update-index

    Available Commands:
     download     Downloads one or more cores and corresponding tool dependencies.
     install      Installs one or more cores and corresponding tool dependencies.
     list         Shows the list of installed platforms.
     search       Search for a core in Boards Manager.
     uninstall    Uninstalls one or more cores and corresponding tool dependencies if no longer used.
     update-index Updates the index of cores.
     upgrade      Upgrades one or all installed platforms to the latest version.

    Flags:
      -h, --help   help for core

    Global Flags:
      --additional-urls strings   Comma-separated list of additional URLs for the Boards Manager.
      --config-file string        The custom config file (if not specified the default will be used).
      --format string             The output format, can be {text|json}. (default "text")
      --log-file string           Path to the file where logs will be written.
      --log-format string         The output format for the logs, can be {text|json}.
      --log-level string          Messages with this level and above will be logged. Valid levels are: trace, debug, info, warn, error, fatal, panic
     -v, --verbose                   Print the logs on the standard output.

    Use "arduino-cli core [command] --help" for more information about a command.
     
     
   # Connect the board to your PC
    
   After connecting the board to your PC by using the USB cable, you should be able to check whether it's been recognized by running:
   
      arduino-cli board list
    
      Port                  Type                Board Name               FQBN                               Core
     /dev/cu.usbmodem14101  Serial Port(USB)    Seeeduino Wio Terminal   Seeeduino:samd:seeed_wio_terminal  Seeeduino:samd
     
     
   Download the platform indexes by running the command:
   
        arduino-cli core update-index
   
   If you see an Unknown board listed, uploading should still work as long as you identify the platform core and use the correct FQBN string. When a board is not detected for whatever reason,try downloading and installing the board in your PC.
   
   Run the code to download package for your board: Seeeduino Wio Terminal
   
    arduino-cli core update-index --additional-urls https://files.seeedstudio.com/arduino/package_seeeduino_boards_index.json
    
  If you using any other board, change the url with your board's url.
    
   
   Run the code to install the particular board in your PC
   
   Here I am installing Seeeduino Wio board
   
     arduino-cli core install Seeeduino:samd
     
   To check again if you have successfully installed the board, run the following code
     arduino-cli board list
     
        Port                  Type                Board Name               FQBN                               Core
     /dev/cu.usbmodem13201  Serial Port(USB)    Seeeduino Wio Terminal   Seeeduino:samd:seeed_wio_terminal  Seeeduino:samd
  
  
# Create a new sketch

 To create a new sketch named MyFirstSketch in the current directory, run the following command:

    arduino-cli sketch new MyFirstSketch
    Sketch created in: /Users/anmol/MyFirstSketch
    
 A sketch is a folder containing assets like source files and libraries; the new command creates for you a .ino file called MyFirstSketch.ino containing Arduino boilerplate code:
 
Change the directory to your new sketch
  
    cd MyFirstSketch 
    
Run the foollowing code to make an arduino file


    ls
    
Run the command to make the setup for your program.

    cat MyFirstSketch.ino
    
   
      void setup() {
    }

     void loop() {
    }

To edit the setup for your program in terminal.

  Run:
  
    nano MyFirstSketch.ino
  
  And change the code similar to this
  
       void setup() {
        pinMode(LED_BUILTIN, OUTPUT);
    }

       void loop() {
         digitalWrite(LED_BUILTIN, HIGH);
         delay(1000);
         digitalWrite(LED_BUILTIN, LOW);
         delay(1000);
    }
    
    
  Save and exit from the steup
  
  # Compile and upload sketch
  
  To compile the sketch you run the compile command, passing the proper FQBN string:

      arduino-cli compile -b Seeeduino:samd:seeed_wio_terminal MyFirstSketch -v
      
 You can get your board's FQBN by running the code:
 
 
     arduino-cli board list
     
     
 To upload the sketch to your board, run the following command, using the serial port your board is connected to:    

    arduino-cli upload -b Seeeduino:samd:seeed_wio_terminal -p /dev/cu.usbmodem13201 MyFirstSketch -v
     
 You can upload any .ino file by just writing the file name without extension after mentioning the serial port as shown above.
 
 # Add libraries
 
 If you need to add more functionalities to your sketch, chances are some of the libraries available in the Arduino ecosystem already provide what you need. For example, if you need a light sensor, you can try searching for the light sensor keyword:
 
      arduino-cli lib search light sensor
      
      Name: "Adafruit APDS9960 Library"
       Author: Adafruit
       Maintainer: Adafruit <info@adafruit.com>
       Sentence: This is a library for the Adafruit APDS9960 gesture/proximity/color/light sensor.
       Paragraph: This is a library for the Adafruit APDS9960 gesture/proximity/color/light sensor.
       Website: https://github.com/adafruit/Adafruit_APDS9960
       Category: Sensors
       Architecture: *
       Types: Contributed
       Versions: [1.0.0, 1.0.1, 1.0.2, 1.0.3, 1.0.4, 1.0.5, 1.0.6, 1.1.0, 1.1.1, 1.1.2, 1.1.3, 1.1.4, 1.1.5].  
      Name: "Adafruit_VL6180X"
       Author: Adafruit
       Maintainer: adafruit <support@adafruit.com>
       Sentence: Sensor driver for VL6180X Time of Flight sensor
       Paragraph: Sensor driver for VL6180X Time of Flight sensor
       Website: https://github.com/adafruit/Adafruit_VL6180X
       Category: Sensors
       Architecture: *
       Types: Contributed
       Versions: [1.0.0, 1.0.2, 1.0.3, 1.0.4, 1.0.5, 1.0.6, 1.0.7, 1.0.8, 1.1.0, 1.2.0]
       Dependencies: Adafruit SSD1306, Adafruit GFX Library
      Name: "Arduino_MKRENV"
       Author: Arduino
       Maintainer: Arduino <info@arduino.cc>
       Sentence: Allows you to read the temperature, humidity, pressure, light and UV sensors of your MKR ENV shield.
       Paragraph:
       Website: http://github.com/arduino-libraries/Arduino_MKRENV
       Category: Sensors
       Architecture: samd
       Types: Arduino
       Versions: [1.0.0, 1.1.0, 1.2.0]
       Provides includes: Arduino_MKRENV.h
      Name: "BH1730"
       Author: Janco Kock
       Maintainer: Janco Kock
       Sentence: An easy to use library for reading light values from the BH1730 light sensor
       Paragraph: An easy to use library for reading light values from the BH1730 light sensor
       Website: https://github.com/jancoow/BH1730-Library
       Category: Sensors
       Architecture: *
       Types: Contributed
       Versions: [1.0.0]
      Name: "BH1750"
       Author: Christopher Laws
       Maintainer: Christopher Laws
       Sentence: Arduino library for the digital light sensor breakout boards containing the BH1750FVI IC
       Paragraph: Pretty simple and robust BH1750 library. Arduino, ESP8266 & ESP32 compatible.
       Website: https://github.com/claws/BH1750
       Category: Sensors
       Architecture: avr, sam, esp8266, esp32, stm32
       Types: Contributed
       Versions: [1.1.4, 1.2.0]
       Provides includes: BH1750.h
     
       
 Let's install one of the libraries,
 
       arduino-cli lib install BH1750
       
       Downloading BH1730@1.0.0...
       BH1730@1.0.0 downloaded
       Installing BH1730@1.0.0...
       Installed BH1730@1.0.0
       
 Similarly, if you want to install particular library using Git hub link, you can following these steps.
 
  At first, you will need to enable the unsafe install of the library which is set as false by default.
  
        arduino-cli config init --overwrite
        
        Config file written to: /Users/anmol/Library/Arduino15/arduino-cli.yaml
        
  You will get the location of config file.
  
 Now, we need to edit the config file.
 
         nano /Users/anmol/Library/Arduino15/arduino-cli.yaml
         
         board_manager:
         additional_urls: []
         daemon:
         port: "50051"
         directories:
         data: /Users/anmol/Library/Arduino15
         downloads: /Users/anmol/Library/Arduino15/staging
         user: /Users/anmol/Documents/Arduino
         library:
         enable_unsafe_install: false
         logging:
         file: ""
         format: text
         level: info
         metrics:
         addr: :9090
         enabled: true
         sketch:
         always_export_binaries: false
         
         
Edit the enable_unsafe_install by setting it as true
 
Hit control-x to quit.
   
Enter "Y" to save the modified buffer.

Let's install our servo library using Github link by running following command

       arduino-cli lib install --git-url https://github.com/PaintYourDragon/Servo.git

       Enumerating objects: 83, done.
       Counting objects: 100% (83/83), done.
       Compressing objects: 100% (57/57), done.
       Total 83 (delta 31), reused 60 (delta 20), pack-reused 0
       Installed Library from Git URL


 
 
 
 
 
    
    

