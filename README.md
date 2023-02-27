[![MCHP](./images/microchip.png)](https://www.microchip.com)

# Curiosity Nano Out-of-the-Box Code using PIC18F56Q71 Microcontroller with MCC Melody

This project comes preloaded on the PIC18F56Q71 Curiosity Nano board when the user first plugs it in. It consists of three programs and a command line that enables choosing between those programs.

- The first program is a simple LED blinking program. The microcontroller starts with this program being activated
- The second program turns on the existing on-board LED by pressing a button on the Curiosity Nano board
- The third program sends an 8-bit counter through UART when the on-board button is pressed. This increases the counter.

The main program is changed by sending one of the numbers 1, 2 or 3 through UART interface. Any other key will return the menu.

## Related Documentation

For more details and code examples on the PIC18F56Q71 click on the following links:

- [PIC18F56Q71 Product Page](https://www.microchip.com/wwwproducts/en/PIC18F56Q71)
- [PIC18F56Q71 Code Examples on GitHub](https://github.com/microchip-pic-avr-examples?q=PIC18F56Q71)

## Software Used

- [MPLAB® X IDE  v6.05 or newer](http://www.microchip.com/mplab/mplab-x-ide)
- [MPLAB® XC8 v2.40 or newer](http://www.microchip.com/mplab/compilers)
- [PIC18F-Q_DFP v1.16.368 or newer Series Device Pack](https://packs.download.microchip.com/)
- [MPLAB® Data Visualizer](https://www.microchip.com/en-us/tools-resources/debug/mplab-data-visualizer)

## Hardware Used

- PIC18F56Q71 Curiosity Nano Development Board is used as a test platform.
<br><img src="images/pic18f56q71_cnano_board.png" width="800">

## Operation

To program the Curiosity Nano board with this MPLAB® X project, follow the steps provided in the [How to Program the Curiosity Nano Board](#how-to-program-the-curiosity-nano-board) chapter.<br>

## 1. Setup

The following peripheral and clock configurations are set up using MCC Melody for the PIC18F56Q71:

- **Clock Control:**
  - Clock Source: HFINTOSC
  - HF Internal Clock: 64_MHz
  - Clock Divider: 1
  <br><img src="images/clock_control_config.png" width="400">

- **Configuration Bits:**
  - CONFIG5:
    - WDT operating mode: WDT Disabled; SWDTEN is ignored
  <br><img src="images/wdt_config.png" width="400">

- **UART2:**
  - UART PLIB Selector: UART2
  - Requested Baudrate: 115200
  - Parity: None
  - Data Size: 8
  - Stop Bits: 1
  - Redirect Printf to UART: Enabled
  <br><img src="images/uart2_config.png" width="400">

- **UART2PLIB:**
  - Enable UART: Enabled
  - Enable Receive: Enabled
  - Enable Transmit: Enabled
  <br><img src="images/uart2_plib_config.png" width="400">

- **Pin Grid View:**
  - UART2 RX2 input: RB5
  - UART2 TX2 output: RB4
  - GPIO input: RA0
  - GPIO output: RC7
  <br><img src="images/pin_grid_view_mcc.png" width="1000">

- **Pins:**
  - RB5:
    - Module: UART2
    - Function: RX2
  - RB4:
    - Module: UART2
    - Function: TX2
  - RA0:
    - Function: GPIO
    - Direction: input
    - Custom Name: Button
    - Weak Pullup: Enabled
  - RC7:
    - Function: GPIO
    - Direction: output
    - Custom Name: LED
  <br><img src="images/pins_mcc.png" width="1000">

**Note:** 
  - Pin RA0 (Button) has weak pull-up enabled.
  - UART2 is routed to CDC pins for more flexibility (TX = RB4, RX = RB5)


The following pin configuration must be made for this project:

|   Pin    | Configuration  | Function    |
| :------: | :------------: | :---------: |
|   RB4    | Digital output | UART2 TX    |
|   RB5    | Digital input  | UART2 RX    |
|   RC7    | Digital output | LED         |
|   RA0    | Digital input  | Button      |

## 2. Demo

### 2.1. LED Blink

The first program is a simple LED blinking program. The program is activated when the microcontroller is plugged in.
To run the first project, send the command `1` through UART using the Data Visualizer. After sending this command, the terminal will receive the following message: `"Program changed to blink LED"`.
<br><img src="images/blinky_demo.gif" width="800">

### 2.2. Push the button to turn on the LED

The second program turns on the on-board LED by pressing the on-board button on the Curiosity Nano board.
To run the second project, send the command `2` through UART using the Data Visualizer. After sending this command, the terminal will receive the following message: `"Program changed to press button to turn on LED"`.
<br><img src="images/button_demo.gif" width="800">

### 2.3. Ramp on Data Visualizer

While the on-board button is pressed, the third program sends an 8-bit counter through UART and increases the counter.
To run the third project, send the command `3` through UART using Data Visualizer. After sending this command, the terminal will receive the following message:`"Program changed to press button to send a ramp through UART"`.

Follow the steps in the **How to use MPLAB® Data Visualizer** section to set up the Data Visualizer so that it can correctly view the ramp through UART2 sent by pressing the button.

<br> **Note:** The next demo is at 8x speed.

<br><img src="images/ramp_demo.gif" width="800">

**Note:** By pressing any other key, the program returns the menu through UART using the software terminal.

## 3. Summary

This project is an out-of-the-box experience for the first-time user. It showcases the basic features of the Curiosity Nano Development platform.


## How to use MPLAB® Data Visualizer

This section illustrates how to use the MPLAB® X Data Visualizer to send commands and receive information, but prior to programming the PIC18F56Q71 Curiosity Nano Board. This can be applied to any other projects.

1. Open the software terminal in MPLAB® X IDE. Left click on the **Data Visualizer** button.

<br><img src="images/data_visualizer_button.png" width="1000">

2. Prepare settings in Data Visualizer.

- Left click on the specific serial port communication **COMx**
- Set the correct **Baud Rate**
- Select the right **Input Source**

<br><img src="images/com_settings_dv.png" width="1000">

3. Start using the programs. Press the **Start** button. Left click on the **Line input**, type any key, send commands.

<br><img src="images/send_input_line.png" width="1000">

**Note:** The next steps must be followed to run the third program.

4. Prepare MPLAB® Data Visualizer. Right click on the **Important files**, click **Add Item to Important Files...** .

<br><img src="images/add_item_important_files.png" width="500">

**Note:** Step 5 will be followed only if there is no existing setup file for Data Visualizer. Otherwise go to Step 6.

5. Prepare MPLAB® Data Visualizer.

- In the **Connections** tab, at the **COMx** option, press **New variable streamer...**
- Type a specific **Variable Streamer Name**
- Choose **Ones' Complement** from the **Framing Mode** dropdown menu
- Type a specific value from the **Start of Frame**, press **Add a variable**
- Type a specific name for the variable name in **Variable Name**
- Press **Next**, after that press **Next** again
- Save these settings using **Save As** button as a DVWS file.

<br><img src="images/plot_streaming_data.png" width="1000">

6. Add the DVWS file to see the ramp using Data Visualizer. Click on the **\*.DVWS file** and **Select**.

<br><img src="images/dvws_file.png" width="700">

7. See the expected result on Data Visualizer.

- Double click on the **\*.dvws file** from **Important Files**, or right click and select **Open with Data Visualizer**, or directly press **Load** button on the **MPLAB Data Visualizer** tab and select the file
- Select **Source** from Time Plot window
- Click **Start Streaming COMx** the communication serial port in the **Variable Streamers** tab
- Click **Scroll axis automatically**.

<br><img src="images/data_visualizer_ramp.png" width="1000">

##  How to Program the Curiosity Nano board

This chapter shows how to use the MPLAB® X IDE to program an PIC® device with an Example_Project.X. This can be applied for any other projects. 

- Connect the board to the PC.

- Open the Example_Project.X project in MPLAB X IDE.

- Set the Example_Project.X project as main project.

  - Right click on the project in the **Projects** tab and click **Set as Main Project**.
    <br><img src="images/program_set_as_main_project.png" width="500">

- Clean and build the Example_Project.X project.

  - Right click on the **Example_Project.X** project and select **Clean and Build**.
    <br><img src="images/program_clean_and_build.png" width="500">

- Select the **PICxxxxx Curiosity Nano** in the Connected Hardware Tool section of the project settings:

  - Right click on the project and click **Properties**
  - Click on the arrow under the Connected Hardware Tool
  - Select the **PICxxxxx Curiosity Nano** (click on the **SN**), click **Apply** and then click **OK**:
    <br><img src="images/program_tool_selection.png" width="500">

- Program the project to the board.
  - Right click on the project and click **Make and Program Device**.
    <br><img src="images/program_make_and_program_device.png" width="500">

<br>

- [Back to Setup](#1-setup)
- [Back to Demo](#2-demo)
- [Back to Summary](#3-summary)
- [Back to Top](#curiosity-nano-out-of-the-box-code-using-pic18f56q71-microcontroller-with-mcc-melody)
