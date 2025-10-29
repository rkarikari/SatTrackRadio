![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/calib2.jpg)
![Alt text](https://raw.githubusercontent.com/rkarikari/SatTrackRadio/main/images/calib1.jpg)

# How Calibration Data is Used

## Automatic Loading

When you select a satellite in the **Tracking** tab, the app
automatically:

-   Looks for a saved calibration for that **satellite + transponder +
    mode** combination
-   If found, loads the calibrated center frequencies into the frequency
    fields
-   Enables manual mode to use these frequencies as the base for Doppler
    correction

## The Flow on Subsequent Passes

### Without Calibration:

    Nominal Transponder Freq → Apply Doppler → Send to Radio
       (e.g., 145.900 MHz)

### With Calibration:

    Calibrated Center Freq → Apply Doppler → Send to Radio
       (e.g., 145.902 MHz - learned from previous pass)

The calibrated frequency accounts for: - Crystal oscillator offset in
the satellite - Transponder drift over time - Your radio's frequency
offset

------------------------------------------------------------------------

## Required Settings in Radio Control Tab

### To USE calibration data automatically:

1.  **Manual Mode**: Should be **ENABLED** (checked)
    -   This tells the app to use the stored calibrated frequencies
    -   The app enables this automatically when loading a calibration
2.  **Lock ↑Tx/Rx↓**: Can be ON or OFF depending on transponder
    -   **ON** for simplex/FM satellites (same uplink/downlink)\
    -   **OFF** for linear transponders (separate uplink/downlink)
3.  **Doppler Correction**: Should be **ENABLED** (checked)
    -   This applies real-time Doppler shifts to the calibrated base
        frequencies
4.  **Auto Update Radio**: Should be **ENABLED** (checked) for automatic
    tracking
    -   **Update Mode**: Choose RX Only, TX Only, or Both depending on
        your operation

### ✅ Complete Setup for Automatic Calibrated Tracking:

    ✓ Manual [checked]                 ← Uses calibrated frequencies
    ✓ Lock ↑Tx/Rx↓ [checked/unchecked] ← Depends on satellite type
    ✓ Enable Doppler Correction        ← Applies real-time Doppler
    ✓ Auto Update Radio                ← Sends to radio automatically
      Update Mode: Both RX/TX          ← Or RX/TX Only as needed

------------------------------------------------------------------------

## The Calibration Workflow

### First Pass (Learning):

1.  Track satellite with nominal frequencies\
2.  When you hear the signal, tune radio manually to center it\
3.  Click **"🎯 Sync Radio"** button\
4.  App reads your tuned frequency and calculates true center\
5.  Calibration is saved automatically

### Subsequent Passes (Automatic):

1.  Select the same satellite\
2.  App auto-loads calibration (you'll see a green message)\
3.  Frequencies are already set to calibrated values\
4.  Enable "Auto Update Radio"\
5.  Radio tracks automatically with Doppler correction applied to
    calibrated frequencies

------------------------------------------------------------------------

## Verification

You can verify calibration is loaded by checking:

### In Radio Control Tab -- "📡 Calibration Status" section shows:

    ✅ Calibrated: X days ago (synced Xx)
    TX offset: X.XX kHz | RX offset: X.XX kHz

### In Satellites Tab

-   Shows calibration info for current satellite

### In Analysis Tab

-   Shows detailed statistics if you want to review quality

------------------------------------------------------------------------

## Why This Matters

### Without calibration:

You need to manually tune every pass because: - Satellite oscillators
drift (temperature changes in orbit) - Different transponders have
different offsets - Your radio may have a frequency offset

### With calibration:

Zero-maintenance tracking because: - App remembers the exact center
frequency - Doppler is applied to the correct base frequency - No manual
tuning needed on future passes

------------------------------------------------------------------------

## Example Scenario

### RS-44 Beacon 

**First Pass (Learning):** - Nominal: 435.605 MHz downlink\
- You tune to **435.603 MHz** to center/hear beacon\
- Click **"Sync Radio"** → Saves **435.603 MHz** as calibrated center

**Second Pass (Automatic):** - App loads **435.603 MHz** automatically\
- Applies Doppler: **-6.2 kHz** at AOS\
- Radio set to **435.6092 MHz**\
- As satellite moves, Doppler changes continuously\
- Radio tracks perfectly without manual intervention

> The calibration essentially *learns* the satellite's true frequency
> once, then reuses it ( until the satellite's oscillator
> drifts significantly, which is tracked in the Analysis tab).
