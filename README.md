# SatTrackRadio

A Satellite tracking application with integrated radio control and real-time Doppler correction for amateur radio satellite operations.

## Screenshots
![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/SatTrackRadio.gif)

![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/Xplot.jpg)

![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/SatTrackRadio7.jpg)

## Features

### 🛰️ Satellite Tracking
- **Real-time position tracking** with azimuth, elevation, range, and velocity
- **SGP4 propagator** for accurate orbital calculations
- **Pass prediction** with configurable minimum elevation
- **Multi-satellite support** with easy selection and management
- **GPS time synchronization** for atomic clock accuracy
- **TLE age warnings** - alerts when orbital data is older than 30 days

### 📡 Radio Control
- **Supported Radios:**
  - Yaesu FT-818 (CAT control via Bluetooth)
  - Kenwood TH-D74 (ASCII commands via Bluetooth)
- **Automatic Doppler correction** for uplink and downlink frequencies
- **Real-time frequency updates** during satellite passes
- **Multiple update modes:**
  - RX Only (Downlink/Simplex)
  - TX Only (Uplink/Simplex)
- **Manual frequency adjustment** with frequency locking
- **Mode selection** (FM, NFM, AM, LSB, USB, CW, CWR, DV)
- **Sync from radio** to read current frequencies
- **Frequency calibration integration** - uses your learned frequencies automatically

### 🎯 Smart Frequency Calibration System

The app now learns from your actual operating experience to predict the best frequencies for future passes!

#### What It Does
- **Saves Your Successful Frequencies**: After making a contact, save the frequencies that actually worked
- **Learns Equipment Characteristics**: Accounts for your radio's oscillator drift and characteristics
- **Tracks Satellite Drift**: Monitors how satellite frequencies change over time
- **AI-Powered Predictions**: Uses LSTM machine learning to predict optimal frequencies
- **Historical Analysis**: Maintains complete history of all your syncs with statistics
- **Quality Assessment**: Rates calibration quality (Excellent/Good/Fair/Poor)
- **Per-Transponder Tracking**: Individual calibration for each satellite mode

#### How Frequency Calibration Works

**Step 1: First Contact**
- Start with nominal frequencies from the transponder database
- Make your contact as usual

**Step 2: Save What Worked**
- After a successful contact, go to the Radio Control tab
- Your current frequencies are displayed
- Click "Sync Radio" to save them to the calibration database
- The app records: frequencies, time, elevation, range, and your location

**Step 3: Build Your Database**
- Each sync adds to your calibration history
- The app tracks patterns across multiple passes
- Statistical analysis calculates drift rates and confidence

**Step 4: AI Predictions Activate**
- After 5+ syncs, the LSTM prediction model kicks in
- The app predicts optimal frequencies for your next pass
- Predictions include confidence levels (0-100%)
- Better data = better predictions

**Step 5: Use Predictions**
- Predicted frequencies automatically appear in the Radio Control tab
- The app shows prediction confidence and when it was calculated
- Fine-tune manually as needed during the pass
- Continue syncing to improve accuracy

#### What Gets Learned
The calibration system compensates for:
- Your radio's oscillator drift
- Satellite oscillator drift over time
- Temperature effects on equipment
- Regional propagation conditions
- Your specific antenna and setup characteristics

#### Calibration Quality Ratings

- **⭐ Excellent** (10+ syncs): Very reliable predictions with low frequency variance
- **✅ Good** (5-9 syncs): Solid predictions with moderate confidence
- **⚠️ Fair** (3-4 syncs): Basic predictions, more data needed
- **❌ Poor** (1-2 syncs): Insufficient data for reliable predictions

### 📊 Calibration Management

#### View All Calibrations
- See complete list of all saved calibrations
- Check sync count and age for each satellite/mode
- View quality ratings at a glance
- Monitor which calibrations need updating

#### Import/Export
- **Export**: Backup your calibration database to a file
- **Import**: Restore calibrations from backup
- **Share**: Transfer calibrations between devices
- Data saved in portable JSON format

#### Clear Options
- **Clear Current**: Remove calibration for selected satellite/mode
- **Clear All**: Delete entire calibration database (with confirmation)
- Useful for starting fresh or removing bad data

### 🗄️ Data Management
- **TLE (Two-Line Element) management**
  - Automatic updates from Celestrak
  - Import/export TLE files
  - Multiple TLE sources (Amateur, Weather, CubeSats, Space Stations)
  - **Age warnings** for TLEs older than 30 days
  - Visual indicators showing TLE freshness
- **Transponder database integration**
  - Automatic download from SatNOGS database
  - Support for multiple transponders per satellite
  - Uplink/downlink frequency pairs
  - Cached offline access

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
  - Radio control panel with calibration status
  - Pass predictions table
  - Satellite management
  - Location settings
  - Application settings with calibration management
- **Visual Lookahead Dial** - Scrollable circular dial to set prediction period (1-30 days)
- **Calibration Status Indicators** - See sync count and quality on Radio and Satellites tabs
- **Status indicators** and countdown timers
- **Color-coded pass predictions** based on elevation
- **Enhanced information display** with emoji indicators for quick recognition

## Installation

Install on your Android phone. 

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
   - Select update mode (RX or TX)
   - Radio will automatically adjust frequency during passes

### Using Smart Frequency Calibration

#### Your First Contact (No Calibration Yet)

1. Select your satellite and transponder
2. The app shows nominal frequencies from the database
3. Enable Doppler correction
4. Make your contact

#### Saving Your First Calibration

1. After a successful contact, stay on the Radio Control tab
2. Your current frequencies are shown in the frequency displays
3. Click the **"Sync Radio"** button
4. A confirmation appears showing what was saved
5. The calibration status updates to show "1 sync"

#### Building Your Calibration Database

**For Best Results:**
- Sync after each successful contact
- Try to sync at different elevations (low, medium, high passes)
- Sync at different times of day
- The more variety in conditions, the better the predictions

**What Happens:**
- Each sync is added to the history
- The app calculates average frequencies
- Standard deviation shows frequency consistency
- Drift rate tracks changes over time

#### Using AI Predictions (After 5+ Syncs)

1. **Look for the LSTM Prediction Indicator**
   - Appears in Radio Control tab calibration status
   - Shows "LSTM Model: Active" with confidence percentage
   - Displays predicted uplink and downlink frequencies

2. **Automatic Frequency Loading**
   - When you select a satellite with LSTM predictions
   - Predicted frequencies automatically load
   - Doppler correction applies on top of predictions
   - Manual adjustment still available

3. **Interpreting Confidence Levels**
   - 80-100%: Very reliable, trust the predictions
   - 60-79%: Good, but watch for drift
   - 40-59%: Use as starting point, expect to adjust
   - Below 40%: More data needed, predictions less reliable

#### Managing Your Calibrations

**View All Calibrations:**
1. Go to Settings tab
2. Scroll to "📡 Frequency Calibration Database" section
3. Click "📊 View All"
4. See table with all satellites, sync counts, ages, quality ratings

**Export Your Data:**
1. Settings tab → Calibration section
2. Click "💾 Export"
3. Choose location to save file
4. File contains all calibrations in JSON format

**Import Calibrations:**
1. Settings tab → Calibration section
2. Click "📥 Import"
3. Select your backup file
4. Calibrations are merged with existing data

**Clear Calibrations:**
- **Clear Current**: Removes calibration for currently selected satellite/mode only
- **Clear All**: Deletes entire database (requires confirmation)

### Radio Control Modes

#### RX Only Mode
Updates only the receive frequency (downlink). Ideal for monitoring satellites.

#### TX Only Mode
Updates only the transmit frequency (uplink). For simplex operations.

### Pass Predictions

1. Navigate to Passes tab
2. Select satellite (or "All Satellites")
3. **Adjust lookahead using the visual dial**
   - Scroll on the circular dial
   - Range: 1 to 30 days
   - Current value shown in center
4. Click "Predict Passes"
5. View upcoming passes sorted by AOS time
6. Passes with high elevation are highlighted
7. **Calibration status shown for each satellite**

### GPS Time Synchronization

For maximum accuracy in Doppler calculations:

1. Go to Location tab
2. Click "Get GPS Location & Time"
3. Wait for GPS fix
4. Check "Use GPS Time"
5. GPS provides atomic clock accuracy for time-sensitive operations

## Configuration

### Settings Options

#### General Settings
- **Minimum Elevation**: Set minimum angle for pass predictions (0-90°)
- **Prediction Period**: Use visual lookahead dial (1-30 days)
- **Update Interval**: Position update frequency (1-60 seconds)
- **Auto-update TLEs**: Automatically refresh TLEs on startup
- **TLE Source**: Choose Celestrak category
- **Auto-connect Radio**: Connect to last used radio on startup

#### Frequency Calibration Settings
- **View All Calibrations**: See complete calibration database
- **Export Calibrations**: Backup your frequency data
- **Import Calibrations**: Restore from backup
- **Clear Current**: Remove calibration for selected satellite
- **Clear All**: Delete entire calibration database

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
- **Integrates with frequency calibration** for improved accuracy

### AI Prediction System

#### LSTM-Like Recursive Model
- **Machine Learning Approach**: Similar to Long Short-Term Memory (LSTM) neural networks
- **Pattern Recognition**: Learns from your historical sync data
- **Multi-Factor Analysis**: Considers elevation, range, time, temperature drift
- **Recursive Predictions**: Each prediction improves based on previous accuracy
- **Confidence Scoring**: Provides reliability estimate (0-100%)

#### Statistical Analysis
For each calibration, the system calculates:
- **Mean Frequencies**: Average uplink and downlink from all syncs
- **Standard Deviation**: Frequency consistency measure
- **95% Confidence Interval**: Range where true frequency likely falls
- **Drift Rate**: Frequency change over time (MHz/day)
- **Prediction Accuracy**: R² score showing model fit quality

#### Data Tracked Per Sync
- Timestamp (UTC)
- Uplink frequency used
- Downlink frequency used
- Satellite elevation at time of sync
- Range to satellite
- Observer location
- Transponder mode
- Sync method (manual/auto)

### CAT Protocol

#### FT-818
- Binary CAT commands
- BCD frequency encoding
- Frequency resolution: Hardware Specs
- 9600 baud rate

#### TH-D74
- ASCII command protocol
- Dual-band operation (Band A/B)
- Frequency resolution: Hardware Specs
- Extended receive coverage on Band B

## Default Satellites

Includes sample pre-configured TLEs and transponders for:
- AO-92 (FOX-1D) - Fox-1D
- Always download the Latest

## Data Sources

- **TLEs**: Celestrak (https://celestrak.org)
- **Transponders**: SatNOGS Database (https://db.satnogs.org)
- **Calibration Data**: Locally stored on device

## Troubleshooting

### TLE Updates Fail
- Check internet connection
- Verify HTTPS connectivity
- Look for TLE age warnings (>30 days indicator)

### Radio Connection Issues
- Verify Bluetooth pairing
- The app only lists devices from bluetooth "paired" in android settings
- Check radio is in CAT control mode
- For FT-818: Ensure correct baud rate (9600)

### GPS Not Working (Android)
- Grant location permissions
- Enable location services
- Ensure clear sky view
- Wait 30-60 seconds for initial fix

### Doppler Correction Inaccurate
- Update TLEs (older than 7 days may be inaccurate)
- Use GPS time synchronization
- Verify observer location is correct
- **Build frequency calibration database** for personalized accuracy

### Frequency Calibration Issues

#### "Sync Radio" Button Doesn't Work
- Ensure a satellite is selected
- Select a transponder mode first
- Check that frequencies are displayed
- Verify you're on the Radio Control tab

#### No LSTM Predictions Appearing
- Need at least 5 syncs before LSTM activates
- Check calibration age (expires after 30 days)
- Verify same transponder mode is selected
- Look at calibration status indicator for details

#### Low Prediction Confidence
- More syncs needed (aim for 10+ for best results)
- Try syncing at different elevations
- Ensure GPS time is accurate during syncs
- Check for consistency in your synced frequencies

#### Predictions Seem Wrong
- Verify TLEs are current (update if old)
- Check that you're using the correct transponder
- Ensure location is accurate
- Consider clearing and rebuilding calibration

#### Calibrations Lost
- Uninstalling app removes all local data
- Export calibrations regularly as backup
- Import to restore from backup file
- Data is device-specific, not cloud-synced

## Tips for Best Results

### Frequency Calibration Best Practices

1. **Start Simple**: Make contacts using nominal frequencies first
2. **Sync Every Contact**: More data = better predictions
3. **Vary Your Conditions**: Sync at different elevations and times
4. **Use GPS Time**: Accurate timestamps improve predictions
5. **Keep TLEs Fresh**: Update regularly for best accuracy
6. **Export Regularly**: Backup your calibrations weekly
7. **Monitor Quality**: Check calibration ratings in Settings
8. **Be Patient**: LSTM needs 5+ syncs to activate
9. **Trust High Confidence**: 80%+ predictions are very reliable
10. **Fine-Tune as Needed**: Predictions are starting points, adjust during pass

### Operating Tips

1. **Pre-Pass Setup**
   - Start tracking 5-10 minutes before AOS
   - Check calibration status for selected satellite
   - Verify TLE age is recent
   - Enable Doppler correction and auto-tracking

2. **During the Pass**
   - Let auto-tracking update your radio
   - Watch for signal strength
   - Fine-tune manually if needed
   - Note actual frequencies that work best

3. **Post-Pass**
   - Sync frequencies after successful contacts
   - Check prediction confidence levels
   - Monitor calibration quality rating
   - Export calibrations if many updates made

4. **Maintenance**
   - Update TLEs weekly
   - Export calibrations monthly
   - Review calibration database quarterly
   - Clear old/bad calibrations as needed

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
- Special thanks to Travis Goodspeed (KK4VCZ), LA3QMA, WM8S, M1HOG, AG6IE, and DG6OBE for their pioneering work in reverse-engineering the Kenwood TH-D74 CAT protocol
- Amateur radio satellite community

## Support

For issues, questions:
- Open an issue on GitHub
- Contact: 9G5AR 

## Disclaimer

This software is provided "as is" without warranty. Use at your own risk. Always verify satellite pass times and frequencies before operations. The developer is not responsible for any damage to equipment or regulatory violations.

---

**73 de 9G5AR** 🛰️📡
