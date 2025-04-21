# GPS Lap Tracker

This project uses GPS data from a Neo M8N module to track laps and visualize the path using live plotting.

## Features

- *GPS Data Acquisition*  
  GPS data is received using the [NeoGPS](https://github.com/SlashDevin/NeoGPS) library, known for its efficiency in parsing NMEA sentences from the Neo M8N GPS module.

- *Serial Communication*  
  Data is sent from the microcontroller via the serial monitor and read on the host machine using the serialpy library.

- *Data Visualization*  
  GPS coordinates are plotted using matplotlib. The first lap's data is used to create the track layout.

- *Lap Counter*  
  A lap is detected when the live GPS location returns within a *0.00002 threshold (latitude/longitude)* of the original starting point.

- *Live Tracking*  
  From the *second lap onwards*, a live location bubble is shown moving along the plotted track, while the track itself remains based on the first lap's recorded data.

## Requirements

- Neo M8N GPS Module  
- Microcontroller (e.g., Arduino, ESP32)  
- Python Libraries:  
  - serialpy  
  - matplotlib

## Usage

1. Upload the NeoGPS-based GPS reading code to your microcontroller.
2. Run the Python script that reads serial data using serialpy and plots it using matplotlib.
3. Complete one full lap to initialize the track.
4. From the second lap onward, live tracking and lap counting will be active.

