# Automated Bottling & Packaging Line Control System

A complete Programmable Logic Controller (PLC) architecture designed to manage a continuous beverage manufacturing line. The system oversees four core operational stations—Quality Inspection, Bottle Capping, Batch Counting, and Packaging—while managing real-time safety interlocks and fault recovery protocols. 

This project was developed in **LS Electric XG5000** using standard Ladder Logic.

## System Architecture & Features

The control logic operates on a single master run interlock, ensuring that emergency stops and fault states safely isolate all downstream machine actuators within a single PLC scan cycle.

* **Automated Sequence Control:** Manages continuous conveyor operation synchronized with a fixed-duration capping cycle (21.0s) and a volumetric batch packaging cycle (16 bottles/batch).
* **Quality Control Interlocks:** Integrates a through-beam photoelectric sensor logic block to detect underfilled bottles. Triggers an immediate system halt and visual alarm for manual operator intervention, preventing mechanical jams or downstream contamination.
* **Supervisory Watchdog Timers:** Includes a custom timeout fault sequence (30.0s) at the packaging station to detect and safely arrest actuator jams or sensor failures.
* **Fail-Safe Safety Architecture:** Start, Stop, and E-Stop loops are hard-interlocked at the master control level. Clearing a fault requires a dedicated reset authorization before the system can be restarted.

## Hardware Allocation

| I/O Address | Device | Description |
| :--- | :--- | :--- |
| `P00000` - `P00002` | Operator Inputs | Start (NO), Stop (NC), Emergency Stop (NC) |
| `P00003` - `P00007` | Field Sensors | Bottle presence, Underfill inspection, High-speed counting, Pack-complete limit switch |
| `P00040` - `P00043` | Actuators | Conveyor Motor, Alarm Beacon, Capping Machine, Packaging Machine |

## Repository Contents

* `220021116_CEP_XG5000.xgw`: The complete, executable XG5000 project file.
* `220021116_CEP_Report.pdf`: Comprehensive engineering documentation including sensor selection rationale, alternative fault-recovery analyses, and simulated waveform verifications.

## Simulation & Verification
The logic has been fully verified using the XG5000 integrated simulator under normal continuous operation, fault interruption/recovery sequences, and mid-cycle emergency stops. See the attached engineering report for execution screenshots.
