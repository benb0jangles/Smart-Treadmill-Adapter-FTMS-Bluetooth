# Smart Treadmill - FTMS Bridge

Transform any manual treadmill into a smart fitness device compatible with Peloton, Zwift, Strava, Kinomap and other fitness apps using a microcontroller and a simple hall effect sensor.

![treadmill_image1](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/jk02.jpg)

This is my ghetto treadmill, it cost me maybe £49.95 in the returned item sale. It doesn't do any interactivity with any of the latest fitness apps. It just has stop start button, speed adjustment. It doesn't do any auto speed/incline adjustment during classes like the £3499 Peloton Tread Machines do but I figure i can adjust speed with the button. Perhaps I will work on this feature later on.

I Have an old ipad 6th gen and a free peloton 30-day trial, so what better way to improve my ghetto-tread than to implement some treadmill metrics and send them to the ipad app. I saw online there is an adapter called a 'runn' (https://npe.fit/products/runn) which attaches to the treadmill and provides app metrics but it costs £77 (+P&P) and that is more than my whole sub-£50 treadmill cost so no thanks.

I decided to create my own adapter using parts i already have in a box at home, I think the parts are cheap though, coming in at under £10 for the whole lot on Ali. I designed and 3d printed the case.

Here
![treadmill_gif1](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/export%20(5).gif)


![treadmill_gif2](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/export%20(6).gif)



## Features

- ✅ **Real-time Speed & Distance Tracking** using hall effect sensor
- ✅ **OLED Display** showing live metrics (speed, distance, calories, incline, time)
- ✅ **Bluetooth Low Energy (BLE)** broadcasting via Fitness Machine Service (FTMS)
- ✅ **Peloton App Compatible** - Full support for iOS/Android in portrait and landscape modes
- ✅ **Live Metrics During Workout** - Speed, pace, distance, incline, elevation gain, calories
- ✅ **Complete Post-Workout Summary** - Charts and graphs for all metrics
- ✅ **Zwift Compatible** - Works with any FTMS-compatible fitness app
- ✅ **Standalone Operation** - Works without app connection, displays metrics on OLED

## Hardware Requirements

### Components

- **Microcontrller** (any variant with BLE support)
- **IR Module Sensor**
- **Small Piece of Aluminum Tape** (to attach to treadmill belt or roller)
- **OLED Display** (128x64, I2C interface)
- **4.2v Lipo Battery** or **5V USB Power Supply**
- **Case/Enclosure** (to protect the System)

## Software Requirements

### Arduino IDE Setup

1. **Install Arduino IDE** (1.8.x or 2.x)
2. **Add ESP32 Board Support:**
   - Go to `File` → `Preferences`
   - Add to "Additional Board Manager URLs":
     ```
     https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
     ```
   - Go to `Tools` → `Board` → `Boards Manager`
   - Search for "ESP32" and install "esp32 by Espressif Systems"

3. **Install Required Libraries:**
   - Go to `Sketch` → `Include Library` → `Manage Libraries`
   - Install the following:
     - `Adafruit GFX Library`
     - `Adafruit SSD1306`
     - `Wire` (built-in)
     - ESP32 BLE libraries (included with ESP32 board package)

## Installation

1. **Clone or Download** this repository
2. **Open** `smart_treadmill.ino` in Arduino IDE
3. **Configure Your Treadmill** (see Configuration section below)
4. **Select Your Board:**
   - `Tools` → `Board` → `ESP32 Arduino` → `ESP32 Dev Module` (or your specific board)
5. **Select Your Port:**
   - `Tools` → `Port` → Select your ESP32's COM port
6. **Upload** the sketch to your ESP32

## Configuration

Before uploading, you **must** configure these settings in `smart_treadmill.ino`:

### 1. Measure Your Treadmill Belt Circumference

```cpp
#define BELT_CIRCUMFERENCE_CM 216.0  // CHANGE THIS
```

**How to measure:**
- Mark a point on your treadmill belt with tape
- Manually rotate the belt one full revolution
- Measure the distance the belt traveled in centimeters
- Update the value in the code

### 2. Set Your Treadmill Incline

```cpp
#define MANUAL_INCLINE 5.0  // CHANGE THIS (% incline)
```

Set this to your treadmill's current incline percentage (e.g., 0.0 for flat, 5.0 for 5% incline).

## Physical Installation

1. **Mount the Hall Effect Sensor:**
   - Position the sensor near the treadmill belt roller or belt edge
   - Secure it so it doesn't move during use
   - Leave a small gap (2-5mm) between sensor and magnet path

2. **Attach the Magnet:**
   - Attach a small magnet to the treadmill belt or roller
   - The magnet should pass close to the hall effect sensor once per revolution
   - Test by manually rotating the belt - the sensor should trigger each revolution

3. **Mount the ESP32 & Display:**
   - Position the OLED display where you can easily see it while running
   - Secure the ESP32 in a safe location away from moving parts
   - Ensure the USB cable or power supply is safely routed

## Usage

### Standalone Mode (No App)

1. **Power on** the ESP32
2. **Start walking/running** - the display will show:
   - Speed (km/h)
   - Distance (km)
   - Calories burned
   - Incline (%)
   - Elapsed time
   - Bluetooth status

### With Peloton App

1. **Power on** the ESP32 (displays "BT: Advertising")
2. **Open Peloton App** on your phone/tablet
3. **Pair the Device:**
   - Go to Settings → Bluetooth Devices
   - Look for device named **"Runn"**
   - Connect to it
4. **Start a Tread Class:**
   - Select any treadmill class
   - Your live metrics will appear during the workout
   - Post-workout summary will show complete stats with charts

### With Zwift or Other FTMS Apps

1. **Power on** the ESP32
2. **Open your fitness app**
3. **Pair as Treadmill** or **FTMS Device**
4. **Start your workout** - live metrics will sync automatically

## Metrics Provided

### Live Metrics (During Workout)
- **Speed** (km/h)
- **Pace** (min/km) - calculated by app
- **Distance** (km)
- **Incline** (%)
- **Elevation Gain** (m) - calculated by app from distance × incline
- **Calories** - calculated by app

### Post-Workout Summary (Peloton)
- Output
- Total Output
- Avg Output
- Distance
- Pace (with chart)
- Avg Pace
- Speed (with chart)
- Avg Speed
- Incline (with chart)
- Avg Incline
- Elevation (with chart)
- Calories

## Troubleshooting

### Display shows "SSD1306 allocation failed"
- Check OLED wiring (SDA to GPIO 8, SCL to GPIO 9)
- Verify OLED I2C address is 0x3C (some displays use 0x3D)
- Check power connections (3.3V and GND)

### No speed/distance showing
- Verify hall effect sensor is triggering (check Serial Monitor)
- Ensure magnet passes close enough to sensor (2-5mm gap)
- Check sensor wiring and polarity
- Confirm `SENSOR_PIN` is set correctly

### Distance way too high/low
- Verify `BELT_CIRCUMFERENCE_CM` is measured correctly
- Re-measure your belt circumference and update the code
- Check Serial Monitor for revolution count accuracy

### Peloton not showing live metrics in landscape mode
- This is now fixed! Use the latest code version
- Ensure BLE connection is established (check "BT:Y" on display)
- Restart the Peloton app and reconnect

### Post-workout metrics missing
- Make sure you complete the class (don't force-quit the app)
- Ensure the ESP32 stays powered for 60 seconds after class ends
- Check Serial Monitor for "Workout STOPPED" message

### Bluetooth won't connect
- Power cycle the ESP32
- Forget the device in your phone's Bluetooth settings and re-pair
- Make sure you're within BLE range (typically 10m or less)
- Check Serial Monitor for "CLIENT CONNECTED" message

## Technical Details

### FTMS Protocol Implementation

This project implements the Bluetooth **Fitness Machine Service (FTMS)** specification for treadmills.

**BLE Service UUID:** `0x1826`
**Treadmill Data Characteristic UUID:** `0x2ACD`
**Control Point Characteristic UUID:** `0x2AD9`

**Data Packet Structure:**
```
Flags: 0x050C (Heart Rate + Elapsed Time + Distance + Inclination)
- Speed (uint16, km/h × 100)
- Distance (uint24, meters)
- Inclination (sint16, % × 10)
- Ramp Angle (sint16, degrees × 10)
- Heart Rate (uint8, 0 if no sensor)
- Elapsed Time (uint16, seconds)
```

**Supported Control Point Commands:**
- `0x00` - Request Control
- `0x01` - Reset (clears all metrics)
- `0x07` - Start/Resume (begins new workout)
- `0x08` - Stop/Pause (ends workout, preserves data for 60s)

### Update Intervals
- **Display:** 200ms (5 Hz)
- **BLE Notifications:** 200ms (5 Hz) for responsive live metrics
- **Speed Timeout:** 3 seconds (stops showing speed after no movement)

## Serial Monitor Debugging

Connect to the Serial Monitor at **115200 baud** to see debug output:

```
*** CLIENT CONNECTED ***
Control Point: Start/Resume
  -> Workout STARTED (all metrics reset)
BLE Notify - State: ACTIVE | Speed: 8.5 km/h | Dist: 0.12 km | Inc: 5.0% | Elev: 6 m | Time: 45 s
Speed: 8.5 km/h | Distance: 0.12 km | Revs: 56 | BT: Connected
Control Point: Stop/Pause
  -> Workout STOPPED
  -> Final metrics will be available for 60 seconds
```

## Customization

### Adjust Calorie Calculation
The internal calorie estimate (displayed on OLED) uses a simple formula:
```cpp
calories = totalDistance * 0.75 * 70;  // Assumes 70kg user
```
Change `70` to your weight in kg for more accurate estimates on the display.

**Note:** Peloton uses its own proprietary calorie calculation based on speed, incline, duration, and user profile.

### Change Device Name
```cpp
BLEDevice::init("Runn");  // Change "Runn" to your preferred name
```

### Adjust Sensor Debounce
If you get false triggers or missed revolutions:
```cpp
if (now - lastTrigger > 50) {  // Change 50ms to higher/lower value
```

## Credits & Acknowledgments

- **FTMS Specification:** Based on Bluetooth SIG Fitness Machine Service standard
- **QZ App Inspiration:** FTMS implementation referenced from [qdomyos-zwift](https://github.com/cagnulein/qdomyos-zwift) project
- **Libraries Used:**
  - Adafruit GFX & SSD1306 for OLED display
  - ESP32 Arduino Core for BLE functionality

## License

This project is open source. Feel free to modify and improve!

## Future Enhancements

Potential improvements you could add:

- [ ] Auto-detect belt circumference via calibration mode
- [ ] Add real heart rate sensor integration (ANT+ or BLE)
- [ ] Motorized incline control via relay
- [ ] Web interface for configuration
- [ ] Multi-user profiles with different calibrations
- [ ] Integration with Home Assistant or other smart home platforms
- [ ] Data logging to SD card
- [ ] Battery level monitoring for portable operation

## Contributing

Found a bug or have an improvement? Feel free to open an issue or submit a pull request!

---

**Enjoy your smart treadmill! 🏃‍♂️**
