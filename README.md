# Tank Level Control System (Manual & Automatic)

A PLC-based tank level control system developed in **Siemens TIA Portal** as part of PLC training and extended with features.
The system simulates an industrial tank process with **manual and automatic operating modes**, analog signal processing, and HMI visualization.
A key focus of this project was solving **latency and instability issues** between **Factory I/O** and **TIA Portal** using signal buffering.

## System Overview
- The system controls the filling and discharging of a tank.
- Tank level is visualized on an HMI using an animated level indicator.
- Both **Manual** and **Automatic** operating modes are supported.
- Analog signals are normalized, scaled, and buffered before being used in control logic.

## Operating Modes

### Manual Mode
- The operator directly controls filling and discharging using HMI buttons.
- Valve opening is adjusted incrementally to control flow rate and speed.
- Each button press increases or decreases the valve opening by a fixed step.
- This allows fine control over filling and discharge speed without abrupt changes.

### Automatic Mode
- The system maintains the tank level using threshold-based logic.
- Filling starts when the level drops below a defined limit.
- Discharging starts when the level exceeds the maximum level.
- Pump operation is automatically linked to the filling state.
- Manual and automatic logic are separated into dedicated Function Blocks.

## Analog Signal Processing
- Raw tank level data is read from an analog input.
- The value is **buffered in a data block** for stable processing.
- The buffered value is:
  - Normalized using `NORM_X`
  - Scaled to engineering units using `SCALE_X`
- Buffering eliminates delay caused by communication latency between Factory I/O and TIA Portal.

## Control Logic Highlights

### Automatic Operation Function Block
- Uses the buffered and scaled tank level value.
- Filling valve opens when the level is below the threshold and discharge is inactive.
- Filling valve closes when the target level is reached.
- Discharge valve opens when the level exceeds the maximum limit.
- Discharge valve closes when the tank is nearly empty.
- The pump runs only when the fill valve is active.

### Manual Operation Function Block
- Filling and discharging are controlled via HMI buttons.
- Analog valve outputs range from **0 (closed)** to **27648 (fully open)**.
- Each button press adjusts the valve opening by approximately **1728**.
- This step-based approach enables controlled flow adjustment.

## HMI Visualization
- Real-time tank level visualization using animated graphics.
- Manual control buttons for filling and discharging.
- Adjustable fill and discharge speeds.
- Mode selection between manual and automatic operation.

## Tools & Technologies
- Siemens TIA Portal
- Siemens WinCC Advanced
- Factory I/O

## What I Learned
- Handling and processing analog signals in PLC systems
- Normalizing and scaling raw analog input values
- Using buffering to solve latency between Factory I/O and TIA Portal
- Designing manual and automatic control logic using Function Blocks
- Integrating PLC logic with HMI visualization

## Possible Improvements
- Implement PID-based level control instead of threshold logic
- Add alarms for overflow, low-level, and sensor faults
- Add trend visualization for tank level history
