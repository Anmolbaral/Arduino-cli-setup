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
    Sketch created in: /Users/anmolbaruwal/MyFirstSketch
    
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

      arduino-cli compile -b Seeeduino:samd:seeed_wio_terminal -v
      
 You can get your board's FQBN by running the code:
 
 
     arduino-cli board list
     
     
 To upload the sketch to your board, run the following command, using the serial port your board is connected to:    

    arduino-cli upload -b Seeeduino:samd:seeed_wio_terminal -p /dev/cu.usbmodem13201  -v
    
    
    

