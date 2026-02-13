# SatTrackRadio

A comprehensive satellite tracking application with integrated dual-radio control, real-time Doppler correction, advanced visualizations, and AI-powered frequency predictions for amateur radio satellite operations.

## Screenshots
![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/SatTrackRadio.gif)

![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/elev_time.jpg)

![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/SatTrackRadio7.jpg)

## Features

### 🛰️ Satellite Tracking
- **Real-time position tracking** with azimuth, elevation, range, and velocity
- **SGP4 propagator** for accurate orbital calculations using official SGP4 library
- **Pass prediction** with configurable minimum elevation (0-90°)
- **Multi-satellite support** with easy selection and management
- **GPS time synchronization** for atomic clock accuracy
- **TLE age warnings** - alerts when orbital data is older than 30 days with visual indicators
- **Altitude and velocity display** for each tracked satellite
- **Range rate tracking** for precise Doppler calculations

### 📡 Dual Radio Control

#### Supported Radios
- **Radio 1 & Radio 2 Support**:
  - Icom IC-705 (CI-V protocol via Bluetooth)
  - Yaesu FT-818 (CAT control via Bluetooth)
  - Kenwood TH-D74 (ASCII commands via Bluetooth)
  - Kenwood TH-D75 (Compatible with D74 protocol)
  - Independent control of two radios simultaneously

#### Radio Assignment
- **Flexible Radio Routing**:
  - Assign uplink to Radio 1 or Radio 2
  - Assign downlink to Radio 1 or Radio 2
  - Full duplex operation with two radios
  - Simplex operation with single radio
  - Mix and match radio types (e.g., IC-705 for uplink, TH-D74 for downlink)

#### Radio Control Features
- **Automatic Doppler correction** for uplink and downlink frequencies
- **Real-time frequency updates** during satellite passes
- **Multiple update modes:**
  - RX Only (Downlink/Simplex)
  - TX Only (Uplink/Simplex)
  - Both (Full Duplex)
- **Manual frequency adjustment** with frequency locking
- **Mode selection** (FM, NFM, WFM, AM, LSB, USB, CW, CWR, RTTY, DV/D-STAR)
- **Sync from radio** to read current frequencies
- **Frequency calibration integration** - uses your learned frequencies automatically
- **Independent connection status** for each radio
- **Auto-reconnect on connection loss**

#### Radio Setup Guide

**Single Radio Setup (Simplex)**:
1. Select your radio type in Radio 1 dropdown
2. Select paired Bluetooth device
3. Leave Radio 2 as "---"
4. Assign Radio 1 to both uplink and downlink selectors
5. Click Connect

**Dual Radio Setup (Full Duplex)**:
1. Select first radio type in Radio 1 dropdown
2. Select first Bluetooth device
3. Select second radio type in Radio 2 dropdown
4. Select second Bluetooth device
5. Assign Radio 2 to uplink, Radio 1 to downlink (or vice versa)
6. Click Connect
7. Both radios connect independently

**IC-705 Satellite Mode Setup**:
1. Select "Icom IC-705" in Radio 1 (or Radio 2) dropdown
2. Select paired Bluetooth device (the IC-705 must be paired as an SPP/serial device)
3. Assign Radio 1 to uplink and/or downlink as needed
4. Click Connect — the app communicates using Icom's CI-V protocol
5. Doppler updates are applied to the active VFO only 

**Connection Status**:
- Each radio shows independent connection status
- Green = Connected and ready
- Red = Disconnected
- Yellow = Connecting

### 🎯 Smart Frequency Calibration System

The app learns from your actual operating experience to predict the best frequencies for future passes using machine learning!

#### What It Does
- **Saves Your Successful Frequencies**: After making a contact, save the frequencies that actually worked
- **Learns Equipment Characteristics**: Accounts for your radio's oscillator drift and characteristics
- **Tracks Satellite Drift**: Monitors how satellite frequencies change over time
- **AI-Powered Predictions**: Uses LSTM machine learning to predict optimal frequencies
- **Historical Analysis**: Maintains complete history of all your syncs with statistics
- **Quality Assessment**: Rates calibration quality (Excellent/Good/Fair/Poor)
- **Per-Transponder Tracking**: Individual calibration for each satellite mode
- **Confidence Scoring**: Shows prediction reliability (0-100%)

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
- Sort by satellite, sync count, or age

#### Import/Export
- **Export**: Backup your calibration database to a file
- **Import**: Restore calibrations from backup
- **Share**: Transfer calibrations between devices
- Data saved in portable JSON format
- Preserves complete history and statistics

#### Clear Options
- **Clear Current**: Remove calibration for selected satellite/mode
- **Clear All**: Delete entire calibration database (with confirmation)
- Useful for starting fresh or removing bad data

### 💾 Frequency Memory System

Quick access to your favorite frequency pairs for instant recall during operations.

#### Features
- **15 Memory Slots** per satellite/transponder combination
- **Store Current Frequencies**: Save uplink/downlink pairs with one click
- **Load Saved Frequencies**: Recall stored frequencies instantly
- **Gen Button**: Automatically generate 15 frequency pairs from a single seed
- **Persistent Storage**: Frequencies saved across app sessions
- **Auto-Advance**: Automatically moves to next available slot
- **Per-Transponder Memory**: Separate memory banks for each satellite mode
- **Visual Indicators**: See which slots are occupied

#### How to Use Memory Slots

**Storing Frequencies**:
1. Set your desired uplink and downlink frequencies
2. Click "Store [#]" button
3. Frequencies are saved to that slot
4. Slot counter automatically advances to next available position

**Loading Frequencies**:
1. Click "Load [#]" button
2. Frequencies are loaded into uplink/downlink fields
3. Doppler correction applies if enabled
4. Slot counter advances to next occupied slot for quick scanning

**Generating Frequency Pairs (Gen Button)**:
1. Store your preferred uplink/downlink pair in slot 1 (the seed)
2. Click "Gen" button
3. App automatically generates 14 additional pairs (slots 2-15):
   - Pairs spaced at 5 kHz intervals
   - Alternating above/below seed frequency to keep it centered
   - Computed via transponder's linear relationship
   - Validated against transponder passband limits
4. Requires linear transponder mode (not FM/repeater)
5. All 15 slots instantly populated for quick scanning during pass

**Gen Button Example**:
- Slot 1 seed: ↑145.950 MHz / ↓435.800 MHz
- Gen creates: 145.940/435.785, 145.960/435.815, 145.945/435.792, etc.
- Maintains correct uplink-to-downlink ratio for the transponder


**Memory Management**:
- Each satellite/transponder has its own 15-slot memory bank
- Switch satellites to access different memory banks
- Overwrite slots by storing to occupied positions
- Use Gen to quickly populate all 15 slots from a seed
- Memory persists when app is closed
- Data is device-specific, not synced to cloud

### 🗺️ Advanced Map & Visualization Features

#### Real-Time Elevation Timeline Graph
- **Scrolling Graph**: Satellite passes scroll right-to-left toward the NOW line in real-time
- **Live Updates**: Graph refreshes every second, continuously showing upcoming passes
- **Multi-Satellite Display**: All upcoming passes shown simultaneously with color-coded labels
- **Interactive Controls**:
  - **Pan**: Drag to view past or future time periods


#### Interactive OpenStreetMap Display
- **Real-time satellite tracking** on world map
- **Zoom and pan** with touch/mouse controls
- **Tile caching** for offline operation
- **Multi-satellite display** - track multiple satellites simultaneously
- **Observer location marker** - shows your position on the map
- **Satellite footprint visualization** - shows coverage area
- **Ground track display** - satellite path across Earth's surface

#### Satellite Footprint Features
- **Real-time footprint calculation** based on satellite altitude
- **Geographic coordinate system** projection
- **Horizon visibility circle** showing coverage area
- **Color-coded footprints** for different satellites
- **Toggle footprint visibility** for each satellite
- **Footprint follows satellite** in real-time
- **Handles date line wrapping** for global tracking

#### Ground Track Display
- **Future path prediction** - see where satellite will travel
- **Historical track** - where satellite has been
- **Configurable track length** - adjust how much path to display
- **Color-coded by elevation** - shows when satellite is visible
- **Smoothly updated** as satellite moves
- **Works in both real-time and visualization modes**

#### Visualization Timeline Mode
- **Predict future pass geometry** - see satellite path at any future time
- **Set custom time** - jump to specific date/time to preview pass
- **TCA (Time of Closest Approach) viewing** - center on best contact time
- **Coverage area preview** - see footprint at selected time
- **Multi-satellite comparison** - view overlapping coverage zones
- **Reset to real-time** - return to live tracking instantly

#### Polar Plot (Sky View)
- **Azimuth/Elevation display** in polar coordinates
- **Real-time satellite position** on sky plot
- **Pass prediction overlay** - see entire pass trajectory
- **Horizon markers** for 0° elevation
- **Cardinal direction indicators** (N, E, S, W)
- **Elevation rings** at 30° and 60°
- **Visual pass quality assessment** - high elevation = better passes

#### Using Visualizations

**Real-Time Tracking**:
1. Go to Visualizations tab
2. Map shows your location and tracked satellite
3. Satellite footprint and ground track update automatically
4. Polar plot shows satellite position in sky
5. All views synchronized with current time

**Future Pass Visualization**:
1. Go to Visualizations tab
2. Select target date/time
3. Click "Show at Selected Time"
4. Map displays satellite position at that time
5. Footprint shows coverage at selected moment
6. Click "Clear Viz" to return to real-time

**Multi-Satellite Tracking**:
1. Add multiple satellites to tracking list
2. All satellites appear on map with different colors
3. Toggle individual footprints on/off
4. Each satellite has distinct marker and footprint
5. Track up to 10 satellites simultaneously

### 🗄️ Data Management
- **TLE (Two-Line Element) management**
  - Automatic updates from Celestrak
  - Import/export TLE files
  - Multiple TLE sources (Amateur, Weather, CubeSats, Space Stations, Starlink)
  - **Age warnings** for TLEs older than 30 days
  - Visual indicators showing TLE freshness
  - Last update timestamp display
- **Transponder database integration**
  - Automatic download from SatNOGS database
  - Support for multiple transponders per satellite
  - Uplink/downlink frequency pairs
  - Mode information (FM, SSB, CW, etc.)
  - Cached offline access
  - Per-transponder calibration support

### 📍 Location Services
- **GPS integration** (Android)
  - Automatic location acquisition
  - GPS time synchronization for sub-second accuracy
  - Altitude detection
  - Fix quality indicators
  - Horizontal and vertical accuracy display
  - Auto-update location on first fix
- **Manual location entry** with validation
- **Observer location caching** - saves across sessions
- **Named locations** - assign custom names to positions
- **Geodetic coordinate support** with WGS-84 ellipsoid

### 🎨 User Interface
- **Modern dark theme** optimized for night operations
- **Tabbed interface** for easy navigation:
  - **Tracking** - Real-time satellite position and velocity
  - **Visualizations** - Map, footprint, ground track, and sky view
  - **Radio Control** - Dual radio management with calibration status
  - **Passes** - Upcoming pass predictions table
  - **Satellites** - Satellite list with TLE management
  - **Location** - GPS and manual position entry
  - **Settings** - Calibration management and app configuration
- **Visual Lookahead Dial** - Scrollable circular dial to set prediction period (1-30 days)
- **Calibration Status Indicators** - See sync count and quality on Radio and Satellites tabs
- **Status indicators** and countdown timers
- **Color-coded pass predictions** based on elevation
- **Enhanced information display** with emoji indicators for quick recognition
- **Connection status for each radio** with color coding
- **Screen always-on during tracking** - prevents timeout during passes

## Installation

Install on your Android phone (APK available in releases).

### System Requirements
- Android 7.0 (Nougat) or higher
- Bluetooth capability for radio control
- GPS for location services (optional)
- Internet connection for TLE/transponder updates
- ~50MB storage space

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
   - Click "Get GPS Location & Time" for automatic setup
   - Optionally name your location
   - Save your location

2. **Add Satellites**
   - Go to Satellites tab
   - Click "Update TLEs" to download latest orbital data
   - Select TLE source (Amateur, Weather, etc.)
   - Satellites and their transponders are automatically downloaded
   - Check TLE age indicators for data freshness

3. **Track a Satellite**
   - Select a satellite from the list
   - Click "Start Tracking"
   - View real-time position, velocity, and Doppler data
   - Azimuth, elevation, range, and range rate update every second

4. **Connect Radio(s)**
   - Go to Radio Control tab
   - **For Single Radio**:
     - Select radio type in Radio 1 dropdown
     - Choose Bluetooth device
     - Leave Radio 2 as "---"
     - Click "Connect"
   - **For Dual Radio**:
     - Select first radio type in Radio 1
     - Choose first Bluetooth device
     - Select second radio type in Radio 2
     - Choose second Bluetooth device
     - Assign radios to uplink/downlink
     - Click "Connect"

5. **Enable Auto-Tracking**
   - Check "Enable Doppler Correction"
   - Check "Auto Update Radio"
   - Select update mode (RX Only, TX Only, or Both)
   - Choose which radio handles uplink and downlink
   - Radio(s) will automatically adjust frequency during passes

### Using Dual Radio Mode

#### Full Duplex Operation
For linear transponder satellites (e.g., AO-91, AO-92):

1. **Connect Two Radios**:
   - Radio 1: Receive radio (e.g., IC-705 or TH-D74 for 145.880 MHz downlink)
   - Radio 2: Transmit radio (e.g., FT-818 or IC-705 for 435.190 MHz uplink)

2. **Assign Radio Functions**:
   - Uplink Radio Selector: Choose "Radio2"
   - Downlink Radio Selector: Choose "Radio1"

3. **Enable Auto-Tracking**:
   - Check "Enable Doppler Correction"
   - Check "Auto Update Radio"
   - Both radios update independently with correct Doppler

4. **During Pass**:
   - Radio 1 tracks downlink frequency
   - Radio 2 tracks uplink frequency
   - Full duplex communication maintained
   - Monitor both connection status indicators

#### Simplex Operation
For FM satellites (e.g., ISS, SO-50):

1. **Use Single Radio**:
   - Set Radio 1 to your transceiver
   - Leave Radio 2 as "---"

2. **Assign to Both Functions**:
   - Uplink Radio Selector: "Radio1"
   - Downlink Radio Selector: "Radio1"

3. **Auto-Tracking**:
   - Select "RX Only" for receive
   - Or "TX Only" for transmit
   - Radio switches between as needed

### Using Map Visualizations

#### Real-Time Tracking
1. Go to Visualizations tab
2. Your location appears as a marker
3. Tracked satellite shows with footprint
4. Ground track displays satellite path
5. Footprint shows coverage area
6. Polar plot shows satellite in sky

#### Predicting Future Passes
1. In Visualizations tab, use date/time picker
2. Select target date and time
3. Click "Show at Selected Time"
4. Map displays satellite position at that moment
5. See footprint coverage for planning
6. Click "Clear Viz" to return to real-time

#### Multi-Satellite Display
1. Track multiple satellites simultaneously
2. Each has unique color marker
3. Toggle individual footprints on/off
4. View overlapping coverage areas
5. Compare pass geometries
6. Plan coordination windows

### Using Smart Frequency Calibration

#### Your First Contact (No Calibration Yet)

1. Select your satellite and transponder
2. The app shows nominal frequencies from the database
3. Enable Doppler correction
4. Make your contact
5. Note actual working frequencies

#### Saving Your First Calibration

1. After a successful contact, stay on Radio Control tab
2. Your current frequencies are shown in the frequency displays
3. Click the **"Sync Radio"** button
4. A confirmation appears showing what was saved
5. The calibration status updates to show "1 sync"
6. Frequency memory automatically stores successful frequencies

#### Building Your Calibration Database

**For Best Results:**
- Sync after each successful contact
- Try to sync at different elevations (low, medium, high passes)
- Sync at different times of day
- The more variety in conditions, the better the predictions
- Use GPS time for accurate timestamps

**What Happens:**
- Each sync is added to the history
- The app calculates average frequencies
- Standard deviation shows frequency consistency
- Drift rate tracks changes over time
- Quality rating improves with more syncs

#### Using AI Predictions (After 5+ Syncs)

1. **Look for the LSTM Prediction Indicator**
   - Appears in Radio Control tab calibration status
   - Shows "LSTM Model: Active" with confidence percentage
   - Displays predicted uplink and downlink frequencies
   - Shows when prediction was calculated

2. **Automatic Frequency Loading**
   - When you select a satellite with LSTM predictions
   - Predicted frequencies automatically load
   - Doppler correction applies on top of predictions
   - No manual adjustment needed for start

3. **Monitor Confidence**
   - 80%+ confidence = Very reliable, use as-is
   - 60-80% confidence = Good starting point, minor tuning may be needed
   - Below 60% = Use with caution, manual adjustment likely needed

4. **Fine-Tune During Pass**
   - If signal is weak, adjust manually
   - Note the working frequency
   - Sync again after pass to improve model
   - Each sync refines predictions

### Using Frequency Memory Slots

#### Quick Store for Later Use

1. **During a Pass**:
   - Dial in your working frequencies
   - Note which slot number is shown (0-14)
   - Click "Store" button
   - Frequencies saved to that slot
   - Display advances to next empty slot

2. **Recalling Frequencies**:
   - Click "Load" button
   - Frequencies from selected slot load
   - Load button cycles through occupied slots
   - Instant frequency recall for repeated satellites

3. **Memory Organization**:
   - Each satellite/transponder has separate memory bank
   - 15 slots per configuration
   - Switch satellites to access different banks
   - Store multiple working frequency pairs
   - Great for different pass elevations or modes

#### Memory Best Practices

- **Store successful frequencies** immediately after contact
- **Label your approach**: low slot numbers for low passes, high for high passes
- **Overwrite old data** when conditions change
- **Use with calibration**: Memory complements, doesn't replace calibration
- **Quick recall**: Perfect for rapid frequency changes during crowded passes

### Predicting Passes

1. Go to Passes tab
2. Set minimum elevation (default 5°)
3. Set prediction period using lookahead dial (1-30 days)
4. Click "Predict Passes"
5. View upcoming passes sorted by AOS time
6. Passes with high elevation are highlighted
7. **Calibration status shown for each satellite**
8. Click on a pass to see detailed information

### GPS Time Synchronization

For maximum accuracy in Doppler calculations:

1. Go to Location tab
2. Click "Get GPS Location & Time"
3. Wait for GPS fix (indicated by status)
4. Fix quality shown (Excellent/Good/Fair/Poor)
5. Check "Use GPS Time"
6. GPS provides atomic clock accuracy for time-sensitive operations
7. Time source indicator shows "GPS (Atomic Clock Accuracy)"
8. System offset displayed for reference

## Configuration

### Settings Options

#### General Settings
- **Minimum Elevation**: Set minimum angle for pass predictions (0-90°)
- **Prediction Period**: Use visual lookahead dial (1-30 days)
- **Update Interval**: Position update frequency (1-60 seconds)
- **Auto-update TLEs**: Automatically refresh TLEs on startup
- **TLE Source**: Choose Celestrak category (Amateur, Weather, CubeSats, etc.)
- **Auto-connect Radio**: Connect to last used radio on startup
- **Use GPS Time**: Enable GPS-based time synchronization

#### Radio Settings
- **Radio 1 Type**: Select Yaesu FT-818, Kenwood TH-D74/D75, or ---
- **Radio 2 Type**: Select second radio type or ---
- **Radio 1 Device**: Choose paired Bluetooth device
- **Radio 2 Device**: Choose second Bluetooth device
- **Uplink Assignment**: Assign uplink to Radio 1 or Radio 2
- **Downlink Assignment**: Assign downlink to Radio 1 or Radio 2
- **Update Mode**: RX Only, TX Only, or Both
- **Auto Doppler**: Enable/disable automatic Doppler correction

#### Frequency Calibration Settings
- **View All Calibrations**: See complete calibration database
- **Export Calibrations**: Backup your frequency data
- **Import Calibrations**: Restore from backup
- **Clear Current**: Remove calibration for selected satellite
- **Clear All**: Delete entire calibration database

#### Display Settings
- **Show All Footprints**: Toggle footprint display for all satellites
- **Ground Track Length**: Adjust how much satellite path to display
- **Map Zoom Level**: Default zoom for map view
- **Theme**: Dark mode (optimized for night use)

## Technical Details

### Orbital Mechanics
- **Official SGP4 propagator** with full perturbation theory
- **Geodetic coordinate conversion** with WGS-84 ellipsoid
- **Look angle calculations** in SEZ (South-East-Zenith) frame
- **Greenwich Sidereal Time** calculations for ECI to ECEF conversion
- **Range rate computation** for accurate Doppler prediction
- **Footprint calculation** using geometric horizon formula
- **Ground track projection** on geodetic coordinates

### Doppler Correction
- **Relativistic Doppler formula** for satellite velocities
- Corrects for satellite velocity along line of sight
- Separate calculations for uplink and downlink
- Real-time updates based on range rate
- **Integrates with frequency calibration** for improved accuracy
- Pre-compensation for uplink transmission
- Direct correction for downlink reception

### AI Prediction System

#### LSTM-Like Recursive Model
- **Machine Learning Approach**: Similar to Long Short-Term Memory (LSTM) neural networks
- **Pattern Recognition**: Learns from your historical sync data
- **Multi-Factor Analysis**: Considers elevation, range, time, temperature drift
- **Recursive Predictions**: Each prediction improves based on previous accuracy
- **Confidence Scoring**: Provides reliability estimate (0-100%)
- **Adaptive Learning**: Model updates with each new sync

#### Statistical Analysis
For each calibration, the system calculates:
- **Mean Frequencies**: Average uplink and downlink from all syncs
- **Standard Deviation**: Frequency consistency measure
- **95% Confidence Interval**: Range where true frequency likely falls
- **Drift Rate**: Frequency change over time (MHz/day)
- **Prediction Accuracy**: R² score showing model fit quality

#### Data Tracked Per Sync
- Timestamp (UTC with GPS accuracy)
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
- Frequency resolution: 10 Hz
- 9600 baud rate
- Mode selection support
- Read/Write frequency operations

#### TH-D74/D75
- ASCII command protocol
- Dual-band operation (Band A/B)
- Frequency resolution: 5 kHz (VHF), 6.25 kHz (UHF)
- Extended receive coverage on Band B
- Mode and power level control
- Status query support

### Map Technology
- **OpenStreetMap** tile integration
- **Tile caching** for offline use
- **Mercator projection** for world display
- **Geodetic to screen coordinate** conversion
- **Multi-satellite rendering** with color coding
- **Footprint calculation** using spherical geometry
- **Ground track smoothing** for visual clarity

## Default Satellites

Includes sample pre-configured TLEs and transponders for:
- AO-92 (FOX-1D) - FM transponder
- ISS (ZARYA) - Voice and APRS
- Always download the latest TLEs for best accuracy

## Data Sources

- **TLEs**: Celestrak (https://celestrak.org)
  - Amateur Radio satellites
  - Weather satellites
  - CubeSats
  - Space Stations
  - Starlink constellation
- **Transponders**: SatNOGS Database (https://db.satnogs.org)
- **Calibration Data**: Locally stored on device in JSON format
- **Frequency Memory**: Device-local persistent storage
- **Map Tiles**: OpenStreetMap contributors

## Troubleshooting

### TLE Updates Fail
- Check internet connection
- Verify HTTPS connectivity
- Try different TLE source
- Look for TLE age warnings (>30 days indicator)
- Manual import option available

### Radio Connection Issues
- Verify Bluetooth pairing in Android settings
- The app only lists devices from Bluetooth "paired" list
- Check radio is in CAT control mode
- For FT-818: Ensure correct baud rate (9600)
- For TH-D74/D75: Verify data band selection
- For IC-705: Ensure the radio's Bluetooth SPP (Serial Port Profile) is enabled and the device is paired before launching the app
- Ensure radio is powered on
- Check battery levels on both radio and phone
- Try forgetting and re-pairing Bluetooth device

### IC-705 Specific Issues
- **Split or Dual Watch not activating**: The app sets these automatically on connection — if they don't engage, try disconnecting and reconnecting
- **CI-V errors or no response**: Confirm the IC-705 Bluetooth is set to SPP mode (not just audio); check the CI-V address in the radio's menu matches the default (0xA4)
- **Frequency not updating during pass**: Verify the IC-705 is the selected radio for the uplink/downlink you want to update
- **Wrong VFO being updated**: The app uses VFO-A for the main frequency and VFO-B for split — do not manually switch VFOs during a tracked pass
- **Mode not changing**: All IC-705 modes are supported (LSB, USB, AM, FM, NFM, WFM, CW, CWR, RTTY, DV/D-STAR); if a mode from the transponder database isn't recognized, the radio defaults to USB

### Dual Radio Issues
- **Both radios not connecting**: Check each is paired separately
- **Wrong radio responding**: Verify radio assignments in selectors
- **Interference between radios**: Ensure adequate separation
- **One radio disconnects**: Check battery, Bluetooth range
- **Frequency not updating**: Verify update mode includes that radio
- **Connection status unclear**: Each radio has independent status indicator

### GPS Not Working (Android)
- Grant location permissions in Android settings
- Enable location services system-wide
- Ensure clear sky view
- Wait 30-60 seconds for initial fix
- Check GPS status indicator for fix quality
- Move away from buildings/obstacles
- Restart app if GPS fix stalls

### Doppler Correction Inaccurate
- Update TLEs (older than 7 days may be inaccurate)
- Use GPS time synchronization for precise timing
- Verify observer location is correct
- **Build frequency calibration database** for personalized accuracy
- Check satellite is in view (elevation > 0°)
- Ensure tracking is active
- Verify radio is connected and responding

### Map/Visualization Issues
- **Map not loading**: Check internet connection for tile download
- **Ground track missing**: Verify tracking is active
- **Satellite not on map**: Check satellite elevation > 0°
- **Visualization stuck**: Click "Clear" to reset to real-time


### Frequency Calibration Issues

#### "Sync Radio" Button Doesn't Work
- Ensure a satellite is selected
- Select a transponder mode first
- Check that frequencies are displayed
- Verify you're on the Radio Control tab
- Confirm radio is connected

#### No LSTM Predictions Appearing
- Need at least 5 syncs before LSTM activates
- Check calibration age (expires after 30 days)
- Verify same transponder mode is selected
- Look at calibration status indicator for details
- Ensure syncs have varied elevation/conditions

#### Low Prediction Confidence
- More syncs needed (aim for 10+ for best results)
- Try syncing at different elevations
- Ensure GPS time is accurate during syncs
- Check for consistency in your synced frequencies
- Verify TLEs are current
- Review and clear any bad sync data

#### Predictions Seem Wrong
- Verify TLEs are current (update if old)
- Check that you're using the correct transponder
- Ensure location is accurate
- Consider clearing and rebuilding calibration
- Compare with nominal frequencies
- Check if satellite frequencies have changed

#### Calibrations Lost
- Uninstalling app removes all local data
- Export calibrations regularly as backup
- Import to restore from backup file
- Data is device-specific, not cloud-synced
- Use file manager to locate backup files

### Frequency Memory Issues
- **Slot shows wrong frequency**: Verify correct satellite/transponder selected
- **Can't overwrite slot**: Simply store to same slot number
- **Memory cleared**: Each satellite/transponder has separate bank
- **Load not working**: Ensure slot is occupied (check slot counter)
- **Gen button disabled**: Requires linear transponder and slot 1 stored first
- **Gen creates invalid pairs**: Check transponder passband limits - some combinations may be invalid
- **Lost memory**: Uninstalling app clears memory, export calibrations includes memory

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
11. **Use Memory Slots**: Store successful frequencies for quick recall
12. **Review Statistics**: Check calibration details to identify patterns

### Dual Radio Operating Tips

1. **Pre-Pass Checklist**:
   - Verify both radios are fully charged
   - Check both Bluetooth connections are stable
   - Confirm radio assignments match your setup
   - Test frequency updates on both radios
   - Verify correct antennas connected
   - **IC-705 users**: Confirm the IC-705 is in Bluetooth SPP mode before connecting

2. **During Full Duplex Pass**:
   - Monitor both connection status indicators
   - Watch for frequency updates on both radios
   - Listen to downlink while transmitting on uplink
   - Note any connection drops for troubleshooting
   - Use memory slots to store working frequencies

3. **Simplex Operation**:
   - Set single radio for both uplink and downlink
   - Use RX Only mode for listening
   - Switch to TX Only when transmitting
   - Let Doppler adjust frequency for you
   - Store successful frequencies to memory

### Operating Tips

1. **Pre-Pass Setup**
   - Start tracking 5-10 minutes before AOS
   - Check calibration status for selected satellite
   - Verify TLE age is recent (< 7 days ideal)
   - Enable Doppler correction and auto-tracking
   - Load frequency memory or use calibration predictions
   - Check both radios connected (if using dual radio)
   - Verify GPS time sync is active
   - Set correct transponder mode

2. **During the Pass**
   - Let auto-tracking update your radio(s)
   - Watch for signal strength and clarity
   - Fine-tune manually if needed
   - Note actual frequencies that work best
   - Monitor elevation and range indicators
   - Check footprint on map for coverage
   - Use polar plot to track satellite position in sky

3. **Post-Pass**
   - Sync frequencies after successful contacts
   - Store working frequencies to memory slots
   - Use Gen button to create full memory bank from best frequency
   - Check prediction confidence levels
   - Monitor calibration quality rating
   - Export calibrations if many updates made
   - Review pass on map visualization
   - Note any issues for troubleshooting

4. **Maintenance**
   - Update TLEs weekly (or when age indicator warns)
   - Export calibrations monthly
   - Review calibration database quarterly
   - Clear old/bad calibrations as needed
   - Clean up unused frequency memory slots
   - Check Bluetooth pairing status periodically
   - Update transponder database monthly

### Map and Visualization Tips

1. **Learning the Footprint**:
   - Zoom in to see your local coverage
   - Note how footprint size changes with altitude
   - Higher satellites = larger footprints
   - Plan operations when footprint covers your area

2. **Ground Track Planning**:
   - View future track to predict visibility
   - Look for passes that cross your region
   - Note direction of travel (ascending/descending)
   - Compare tracks for multiple satellites

3. **Using Timeline Mode**:
   - Set time to peak elevation for best view
   - Check footprint coverage at TCA
   - Preview overlapping satellite coverage
   - Plan coordinated multi-satellite operations

4. **Multi-Satellite Coordination**:
   - Track multiple satellites simultaneously
   - Compare footprints for overlap
   - Plan relay operations
   - Identify mutual visibility windows

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
- OpenStreetMap contributors for map tiles
- Qt framework and community
- Official SGP4 library developers
- Icom for their published CI-V protocol documentation enabling IC-705 integration
- Special thanks to Travis Goodspeed (KK4VCZ), LA3QMA, WM8S, M1HOG, AG6IE, and DG6OBE for their pioneering work in reverse-engineering the Kenwood TH-D74 CAT protocol
- Amateur radio satellite community for feedback and testing

## Support

For issues, questions, or feature requests:
- Open an issue on GitHub
- Contact: 9G5AR
- Amateur radio forums and satellite communities

## Disclaimer

This software is provided "as is" without warranty. Use at your own risk. Always verify satellite pass times and frequencies before operations. The developer is not responsible for any damage to equipment or regulatory violations. Ensure compliance with local amateur radio regulations when operating.

---

**73 de 9G5AR** 🛰️📡

