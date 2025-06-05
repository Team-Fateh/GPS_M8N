#  GPS-Based Lap Tracker

Live GPS lap tracking and visualization system using a **Neo M8N GPS module** + **Python**.

---

##  Features

- **GPS Data Acquisition**  
  High-accuracy GPS data is received using the [NeoGPS](https://github.com/SlashDevin/NeoGPS) library.

- **Serial Communication**  
  Data is transmitted from the microcontroller and read via `serialpy` on the host PC.

- **Real-Time Data Visualization**  
  GPS coordinates are plotted using `matplotlib`. The first lap defines the base track layout.

- **Lap Detection and Timing**  
  A lap is considered complete when the current GPS location returns within a **0.00003°** threshold of the start point.

- **Live Tracking (Lap 2+)**  
  From the second lap onward, a moving location marker is shown. The base track remains constant.

- **RPM Trail Visualization**  
  RPM is simulated and shown as a color-coded trail:
  - 🟢 Green: < 2000 RPM  
  - 🟡 Yellow: 2000–4000 RPM  
  - 🔴 Red: > 4000 RPM

---

##  Core Functions

### `save_first_lap_trajectory()`
- Saves latitude/longitude of the first lap into a `.npy` file.
- Returns the array for use in offset boundary drawing.
  ![save_first_lap](https://github.com/user-attachments/assets/4736b8c9-c956-4ac8-aefa-8d5875f3a477)


### `draw_virtual_start_line(lat, lon)`
- Creates a vertical **lime green** start/finish line using the first GPS coordinate.
- Only drawn once at initialization.
  ![virtual_start_line](https://github.com/user-attachments/assets/ce2e1304-75b0-4731-b7b7-46abfbe7f9a4)


### `update_lap_one()`
- Called during lap 1.
- Simulates RPM and assigns a trail color.
- Plots GPS path in real-time.
- Updates blue current-location marker.
- Displays point count.
  ![lap one ](https://github.com/user-attachments/assets/5e455d84-14df-495c-957c-a29266bd69c3)


### `update_plot_lap_two_onwards()`
- Called from lap 2 onwards.
- Applies RPM color logic.
- Loads saved first lap and draws offset track boundaries.
- Updates GPS trail and live position.
- Refreshes lap counter and timer.
  ![lap two onwards](https://github.com/user-attachments/assets/5202e6c8-846d-4b3d-b6a6-9140149e5417)


### `check_lap_completion(lat, lon)`
- Continuously checks proximity to the start line.
- Triggers when:
  - Enough points are recorded.
  - Start point is reached again.
- Actions:
  - Increments lap count.
  - Updates lap time.
  - Saves first lap (if applicable).
  - Clears old data to prep for the next lap.
    ![check lap completion ](https://github.com/user-attachments/assets/79b09cfb-9074-44a1-a42e-407534d821f9)


### **Main Loop Logic**
Continuously:
- Reads GPS data via Arduino serial (e.g., `COM3`).
- Parses GPS (lat, lon).
- Initializes start line.
- Appends valid coordinates.
- Calls:
  - `update_lap_one()` during lap 1.
  - `update_plot_lap_two_onwards()` for lap 2+.
- Handles cleanup on keyboard interrupt.
  ![main loop ](https://github.com/user-attachments/assets/7d8f5234-61c4-4647-a15a-52b531ce62df)


---

##  Requirements

- **Hardware**
  - Neo M8N GPS Module  
  - Microcontroller (e.g., Arduino)

- **Python Libraries**
  - `serialpy`  
  - `matplotlib`  
  - `numpy`

---

##  Usage

** Hardware Setup**

- Connect your **Neo M8N GPS module** to your **microcontroller** (e.g., Arduino).
- Ensure the GPS module has a clear view of the sky for optimal signal.
- Upload your Arduino sketch that outputs GPS NMEA sentences via serial.
