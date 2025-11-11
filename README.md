![treadmill_image2](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/ghetto-tread.jpg)

Youtube Demo>>>>>

[![Smart Treadmill - FTMS Bridge - Youtube Demo](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fshorts%2FBZ-bItdW56I)](https://www.youtube.com/shorts/BZ-bItdW56I)

# Smart Treadmill - FTMS Bridge

Transform any manual treadmill into a smart fitness device compatible with Peloton, Zwift, Strava, Kinomap and other fitness apps using a microcontroller and a simple ir sensor.

![treadmill_image1](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/jk02.jpg)

This is my ghetto treadmill, it cost me maybe £49.95 in the returned item sale. It doesn't do any interactivity with any of the latest fitness apps. It just has stop start button, speed adjustment. It doesn't do any auto speed/incline adjustment during classes like the £3499 Peloton Tread Machines (https://www.onepeloton.com/en-GB/shop/tread) do but I figure i can adjust speed with the button. Perhaps I will work on this feature later on. For heartrate monitoring I use a cheap £10 bluetooth heart monitor chest strap from ebay/ali.

![treadmill_image3](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/1%20(Small).jpg)

I Have an old ipad 6th gen and a free peloton 30-day trial, so what better way to improve my ghetto-tread than to implement some treadmill metrics and send them to the ipad app. I saw online there is an adapter called a 'runn' (https://npe.fit/products/runn) which attaches to the treadmill and provides app metrics but it costs £77 (+P&P) and that is more than my whole sub-£50 treadmill cost so no thanks.

I decided to create my own adapter using parts i already have in a box at home, I think the parts are cheap though, coming in at under £10 for the whole lot on Ali. I designed and 3d printed the case.


Here is a gif of the peloton app on ios/ipad and the metrics data is displayed at the lower half of the screen. Interestingly, the peloton app does not display metric data if in landscape mode which is unfortunate as most people balance their tablets in that orientation, perhaps it is peloton's cheeky dig at you to buy a whole peloton tread yo.

![treadmill_gif1](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/export%20(5).gif)

Here is a gif of how the wireless sensor functions. there is a small piece of aluminium foil tape (or anything moderately reflective for the ir led to bounce off) on the treadmill which registers everytime it passes the sensor, with this it is possible to calculate speed, and from this we can calculate other metrics too with some simple maths. At present, I am using static incline measurement but in future there is no reason why I cannot implement active incline using an imu, it's very simple to do.

![treadmill_gif2](https://github.com/benb0jangles/Smart-Treadmill-Adapter-FTMS-Bluetooth/blob/main/images/export%20(6).gif)

## Features

- ✅ **Real-time Speed & Distance Tracking** using ir sensor
- ✅ **OLED Display** showing live metrics (speed, distance, calories, incline, time)
- ✅ **Bluetooth Low Energy (BLE)** broadcasting via Fitness Machine Service (FTMS)
- ✅ **Peloton App Compatible** - Full support for iOS/Android in portrait and landscape modes
- ✅ **Live Metrics During Workout** - Speed, pace, distance, incline, elevation gain, calories
- ✅ **Complete Post-Workout Summary** - Charts and graphs for all metrics
- ✅ **Zwift Compatible** - Works with any FTMS-compatible fitness app
- ✅ **Standalone Operation** - Works without app connection, displays metrics on OLED
- ✅ **Battery monitoring** showing remaining charge percentage

### App Compatibility
Works seamlessly with:
- Peloton Digital
- Zwift
- Kinomap
- Strava
- TrainerRoad
- Any app supporting Fitness Machine Service (FTMS)

## Hardware Requirements

### Components
- **Microcontroller** (any variant with BLE support)
- **IR Module Sensor**
- **Small Piece of Aluminum Tape** (to attach to treadmill belt or roller)
- **OLED Display** (128x64, I2C interface)
- **4.2v Lipo Battery** or **5V USB Power Supply**
- **Case/Enclosure** (to protect the System)

### Smart Configuration
- **Web interface** for easy setup (no code editing required!)
- Configure belt circumference, incline, device name
- Set your weight and height for accurate calorie calculations
- Automatic BMI calculation
- Settings saved permanently to device memory

## Software Installation
### upload the .bin file:
The easiest way to upload the firmware is using **ESP Web Flasher** (no software installation needed!):

1. **Download** the latest `.bin` file from the releases page
2. **Connect** your microcontroller to your computer via USB
3. **Open** [ESP Web Flasher](https://esp.huhn.me/) in Chrome or Edge browser
4. **Click** "Connect" and select your device's COM port
5. **Select** the downloaded `.bin` file
6. **Click** "Program" and wait for completion
7. **Done!** Your device will restart automatically

> **Alternative:** You can also use [esptool.py](https://github.com/espressif/esptool) or Arduino IDE if you prefer traditional methods.

### 1. Measure your treadmill belt circumference
### 2. Set Your Treadmill Incline
### 3. attach your shiny tape

### 4. Configure via Web Interface

On first boot, the device creates a WiFi Access Point:

1. **Connect** to WiFi network: `Runn-Config`
2. **Password:** `runn1234`
3. **Open browser** and navigate to: `http://192.168.4.1`
4. **Configure settings:**
   - **Device Name**: Customize Bluetooth name (shows in apps)
   - **Belt Circumference**: Measure your treadmill belt (in cm)
   - **Incline**: Set your treadmill's incline percentage
   - **Weight**: Enter your weight (kg) for accurate calories
   - **Height**: Enter your height (cm) for BMI calculation
5. **Save** settings - they're stored permanently!

**OLED Display shows WiFi info on startup:**
```
=== READY ===

WiFi: Runn-Config
Pass: runn1234

IP: 192.168.4.1

BLE: Advertising
```

---

### Standalone Mode (No App)

1. **Power on** the device
2. **Start walking/running** - the display will show:
   - Speed (km/h)
   - Distance (km)
   - Calories burned
   - Incline (%)
   - Elapsed time
   - Bluetooth status

### With Peloton App

1. **Power on** the device (displays "BT: Advertising")
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

1. **Power on** the device
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

## Technical Details

### FTMS Protocol Implementation

This project implements the Bluetooth **Fitness Machine Service (FTMS)** specification for treadmills.

## Credits & Acknowledgments

- **FTMS Specification:** Based on Bluetooth SIG Fitness Machine Service standard

### Battery Management

The -C3 XIAO includes built-in LiPo battery charging:
- Displays battery percentage on OLED (top right)
- Monitors voltage via ADC
- Calculates remaining charge (4.2V = 100%, 3.0V = 0%)
- Updates every 5 seconds

## Future Enhancements

Potential improvements to add:

- [ ] Auto-detect belt circumference via calibration mode
- [ ] Motorized incline control via relay
- [ ] Integration with Home Assistant or other smart home platforms
- [ ] Data logging to SD card

## Contributing

Found a bug or have an improvement? Feel free to open an issue or submit a pull request!

---

**Enjoy your smart treadmill! 🏃‍♂️**
