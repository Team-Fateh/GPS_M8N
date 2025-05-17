# GPS-Based Lap Tracker

Live GPS lap tracking and visualization system using Neo M8N module + Python.

## Features

- *GPS Data Acquisition*  
  GPS data is received using the [NeoGPS](https://github.com/SlashDevin/NeoGPS) library, known for its high accuracy and low latency.

- *Serial Communication*  
  Data is sent from the microcontroller via the serial monitor and read on the host machine using the *serialpy* library.

- *Data Visualization*  
  GPS coordinates are plotted using *matplotlib*. The first lap's data is used to create the track layout.

- *Lap Counter and Lap Timer*  
  A lap is detected when the live GPS location returns within a *0.00003 threshold (latitude/longitude)* of the original starting point, and the lap time is plotted as well.

- *Live Tracking*  
  From the *second lap onwards*, a live location bubble is shown moving along the plotted track, while the track itself remains based on the first lap's recorded data.
- *RPM Trail Visualisation*
  Creates a coloured RPM trail
## Requirements

- Neo M8N GPS Module  
- Microcontroller
- Python Libraries:  
  - serialpy  
  - matplotlib

## Usage

1. Upload the NeoGPS-based GPS reading code to your microcontroller.
2. Run the Python script that reads serial data using serialpy and plots it using matplotlib.
3. Complete one full lap to initialize the track.
4. From the second lap onward, live tracking and lap counting will be active.

