# SatTrackRadio

A Satellite tracking application with integrated radio control and real-time Doppler correction for amateur radio satellite operations.

## Screenshots
![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/SatTrackRadio9.jpg)

![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/SatTrackRadio8.jpg)


## Features

### 🛰️ Satellite Tracking
- **Real-time position tracking** with azimuth, elevation, range, and velocity
- **SGP4 propagator** for accurate orbital calculations
- **Pass prediction** with configurable minimum elevation
- **Multi-satellite support** with easy selection and management
- **GPS time synchronization** for atomic clock accuracy

### 📡 Radio Control
- **Supported Radios:**
  - Yaesu FT-818 (CAT control via Bluetooth)
  - Kenwood TH-D74 (ASCII commands via Bluetooth)
- **Automatic Doppler correction** for uplink and downlink frequencies
- **Real-time frequency updates** during satellite passes
- **Multiple update modes:**
  - RX Only (Downlink/Simplex)
  - TX Only (Uplink/Simplex)
  - Both RX/TX (Full Duplex/Split)
- **Manual frequency adjustment** with frequency locking
- **Mode selection** (FM, NFM, AM, LSB, USB, CW, CWR, DV)
- **Sync from radio** to read current frequencies

### 🗄️ Data Management
- **TLE (Two-Line Element) management**
  - Automatic updates from Celestrak
  - Import/export TLE files
  - Multiple TLE sources (Amateur, Weather, CubeSats, Space Stations)
- **Transponder database integration**
  - Automatic download from SatNOGS database
  - Support for multiple transponders per satellite
  - Uplink/downlink frequency pairs

### 📍 Location Services
- **GPS integration** (Android)
  - Automatic location acquisition
  - GPS time synchronization for sub-second accuracy
  - Altitude detection
- **Manual location entry** with validation
- **Observer location caching**

### 🎨 User Interface
- **Modern dark theme** optimized for night operations
- **Tabbed interface** for easy navigation:
  - Tracking view with real-time data
  - Radio control panel
  - Pass predictions table
  - Satellite management
  - Location settings
  - Application settings
- **Status indicators** and countdown timers
- **Color-coded pass predictions** based on elevation


### Main Tracking Interface
Real-time satellite position, Doppler shift calculations, and countdown to next pass.

### Radio Control Panel
Integrated CAT control with automatic Doppler correction and frequency management.

### Pass Predictions
Comprehensive pass table with AOS/LOS times, duration, and maximum elevation.

## Installation

Install on your android phone. 

#### Permissions Required
- `BLUETOOTH` - For radio control
- `BLUETOOTH_CONNECT` - For Bluetooth device pairing
- `ACCESS_FINE_LOCATION` - For GPS functionality
- `INTERNET` - For TLE and transponder updates

## Usage

### Getting Started

1. **Set Your Location**
   - Navigate to the Location tab
   - Enter coordinates manually or use GPS (Android)
   - Save your location

2. **Add Satellites**
   - Go to Satellites tab
   - Click "Add" to download from catalog
   - Select satellites you want to track
   - TLEs and transponders are automatically downloaded

3. **Track a Satellite**
   - Select a satellite from the list
   - Click "Start Tracking"
   - View real-time position and Doppler data

4. **Connect Radio** (Optional)
   - Go to Radio Control tab
   - Select radio type (FT-818 or TH-D74)
   - Choose Bluetooth device (Previously paired devices)
   - Click "Connect"

5. **Enable Auto-Tracking**
   - Check "Enable Doppler Correction"
   - Check "Auto Update Radio"
   - Select update mode (RX/TX/Both)
   - Radio will automatically adjust frequencies during passes

### Radio Control Modes

#### RX Only Mode
Updates only the receive frequency (downlink). Ideal for monitoring satellites.

#### TX Only Mode
Updates only the transmit frequency (uplink). For simplex operations.

#### Both RX/TX Mode
Full duplex operation with split frequencies. Automatically manages both uplink and downlink with Doppler correction.

### Pass Predictions

1. Navigate to Passes tab
2. Select satellite (or "All Satellites")
3. Click "Predict Passes"
4. View upcoming passes sorted by AOS time
5. Passes with high elevation are highlighted

### GPS Time Synchronization

For maximum accuracy in Doppler calculations:

1. Go to Location tab
2. Click "Get GPS Location & Time"
3. Wait for GPS fix
4. Check "Use GPS Time"
5. GPS provides atomic clock accuracy for time-sensitive operations

## Configuration

### Settings Options

- **Minimum Elevation**: Set minimum angle for pass predictions (0-90°)
- **Prediction Period**: Hours to predict ahead (1-168 hours)
- **Update Interval**: Position update frequency (1-60 seconds)
- **Auto-update TLEs**: Automatically refresh TLEs on startup
- **TLE Source**: Choose Celestrak category
- **Auto-connect Radio**: Connect to last used radio on startup

## Technical Details

### Orbital Mechanics
- **SGP4 propagator** with full perturbation theory
- **Geodetic coordinate conversion** with WGS-84 ellipsoid
- **Look angle calculations** in SEZ (South-East-Zenith) frame
- **Greenwich Sidereal Time** calculations for ECI to ECEF conversion

### Doppler Correction

- Corrects for satellite velocity along line of sight
- Separate calculations for uplink and downlink
- Real-time updates based on range rate

### CAT Protocol

#### FT-818
- Binary CAT commands
- BCD frequency encoding
-
- Frequency resolution: Hardware Specs

#### TH-D74
- ASCII command protocol
- Dual-band operation (Band A/B)
- 
- Frequency resolution: Hardware Specs
- Extended receive coverage on Band B

## Default Satellites

Includes sample pre-configured TLEs and transponders for:
- AO-92 (FOX-1D) - Fox-1D
- Always download the Latest


## Data Sources

- **TLEs**: Celestrak (https://celestrak.org)
- **Transponders**: SatNOGS Database (https://db.satnogs.org)

## Troubleshooting

### TLE Updates Fail
- Check internet connection
- Verify HTTPS connectivity

### Radio Connection Issues
- Verify Bluetooth pairing
- The app only lists devices from bluetooth "paired" in android settings.
- Check radio is in CAT control mode
- For FT-818: Ensure correct baud rate (9600 )
  

### GPS Not Working (Android)
- Grant location permissions
- Enable location services
- Ensure clear sky view
- Wait 30-60 seconds for initial fix

### Doppler Correction Inaccurate
- Update TLEs (older than 7 days may be inaccurate)
- Use GPS time synchronization
- Verify observer location is correct

## Contributing

Contributions are welcome! 

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Credits

**Developer**: 9G5AR  
**Copyright**: RNK, RadioSport 2025

### Acknowledgments
- Celestrak for TLE data
- SatNOGS for transponder database
- Qt framework
- Special thanks to Travis Goodspeed (KK4VCZ), LA3QMA, WM8S, M1HOG, AG6IE, and DG6OBE for their pioneering work in reverse-engineering the Kenwood TH-D74 CAT protocol.
- Amateur radio satellite community : 

## Support

For issues, questions:
- Open an issue on GitHub
- Contact: 9G5AR 

## Disclaimer

This software is provided "as is" without warranty. Use at your own risk. Always verify satellite pass times and frequencies before operations. The developer is not responsible for any damage to equipment or regulatory violations.

---

**73 de 9G5AR** 🛰️📡
