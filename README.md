# 🏭 Multi-PLC Handshake & OPC UA Integration

**Industrial Automation Project | Siemens TIA Portal V17 | PLCSIM**

## 📖 Project Overview
This project demonstrates a distributed control system architecture between two independent S7-1500 PLCs. It implements a robust **handshake interlocking protocol** to synchronize material flow between a Loading Station (PLC1) and a Testing Station (PLC2), while exposing production data via **OPC UA** for Industry 4.0 integration.

Key Engineering Features
1. Robust Handshake Protocol
  Implemented a state-based interlocking system to prevent part collisions:
  PLC1 detects a part and sets Part_Ready = TRUE.
  PLC2 detects the rising edge, starts a 2-second processing timer, and sets Part_Done = TRUE.
  PLC1 acknowledges the completion, resets the flag, and restarts the conveyor.

3. HMI Abstraction Layer (Best Practice)
  Instead of linking HMI tags directly to physical I/O (%I0.0, %Q0.0), I implemented Global Data Blocks (DBs) as an abstraction layer:
  DB_Commands: Handles HMI inputs (Start/Stop).
  DB_Status: Handles machine outputs and counters.
  Benefit: Drastically reduces MTTR (Mean Time To Repair) and allows for easy I/O reassignment without touching HMI screens.

5. Industry 4.0 / OPC UA Integration
Configured the native OPC UA server on the S7-1500 CPU to expose production metrics (Part_Count, Machine_Status) to external MES/SCADA systems securely.
🛠️ Technical Stack
Hardware (Simulated): 2x Siemens S7-1500 (CPU 1214C DC/DC/DC)
HMI: KTP700 Basic PN
Software: TIA Portal V17, PLCSIM, UaExpert
Protocols: PROFINET, S7 Communication (PUT/GET), OPC UA


