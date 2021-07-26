# Arduino-cli-setup

  Download the pre-built binary for your supported platform
  
  Extract the downloaded file to a directory already in your path or add the Arduino CLI installation path to your PATH environment variable.
  
  # To add to the path on a Mac OS:
  
   Open your Terminal.
   
   Run the command:              
   
    sudo nano /etc/paths
   
   Enter your password, when required.
   
   Go to the bottom of the file, and enter the path you wish to add.
   
   Hit control-x to quit.
   
   Enter "Y" to save the modified buffer.
  
  # Use the install scripts
   The script requires sh. This is always available on Linux and macOS. sh is not available by default on Windows. The script may be run on Windows by installing    Git for Windows, then running it from Git Bash.
   
   This script will install the latest version of Arduino CLI to $PWD/bin:
     
     curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh
     
   If you want to target a different directory, for example ~/local/bin, set the BINDIR environment variable like this:
   
    curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | BINDIR=~/local/bin sh
    
   If you would like to use the arduino-cli command from any location, install Arduino CLI to a directory already in your PATH or add the Arduino CLI installation path to your PATH environment variable.
   
   If you want to download a specific arduino-cli version, for example 0.9.0, pass the version number as a parameter like this:
   
     curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh -s 0.9.0
     
   Run the code to see if you have successfully installed the script
   
     arduino-cli help core
     
   # Connect the board to your PC
   
   The first thing to do upon a fresh install is to update the local cache of available platforms and libraries by running:
   
     $ arduino-cli core update-index
   Updating index: package_index.json downloaded
   
   After connecting the board to your PC by using the USB cable, you should be able to check whether it's been recognized by running:
   
     $ arduino-cli board list
    
      Port                  Type                Board Name               FQBN                               Core
     /dev/cu.usbmodem14101  Serial Port(USB)    Seeeduino Wio Terminal   Seeeduino:samd:seeed_wio_terminal  Seeeduino:samd
   
   If you see an Unknown board listed, uploading should still work as long as you identify the platform core and use the correct FQBN string. When a board is not detected for whatever reason,try downloading and installing the board in your PC.
   
   Run the code to download package for your board: Seeeduino Wio Terminal
   
    arduino-cli core update-index --additional-urls https://files.seeedstudio.com/arduino/package_seeeduino_boards_index.json
    
   
   Run the code to install the particular board in your PC
   
     arduino-cli core install Seeeduino:samd
     
   To see if you have successfully downloaded the board, run the following code and see if you can get details about your board
   
     arduino-cli board list
     
 
  
  
