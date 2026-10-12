# Geminus — System Architecture

Each system is a line of its own. Under it, each numbered item is a subsystem,
with its inputs (←) and outputs (→) as sub-items. Use "—" when there are none.
External actors: Drone under test (DUT), Operator.

Drone Interface
1. Mounting adapter
   1. ← drone geometry and mass, adapter configuration
   2. → rigid drone attachment, drone-plus-payload COM offset
2. COM alignment
   1. ← drone-plus-payload COM offset, live angle readout
   2. → platform height setting, counterweight positions

Structure
1. Base and column
   1. ← —
   2. → fixed reference frame
2. Gimbal stages (pitch → roll → yaw)
   1. ← rigid drone attachment, drone thrust and torques, axis support, friction torque, platform height setting, counterweight trim, locked axes
   2. → stage rotations, stage loads
3. Counterweights
   1. ← counterweight positions
   2. → counterweight trim

Rotary Joints
1. Bearings (one per axis)
   1. ← fixed reference frame, stage loads
   2. → axis support, friction torque
2. Slip rings (pitch, roll axes)
   1. ← roll and yaw A/B signals, 5 V rig power
   2. → routed roll and yaw A/B signals, roll and yaw encoder power

Sensing
1. Encoders (pitch, roll, yaw)
   1. ← stage rotations, 5 V rig power, roll and yaw encoder power
   2. → pitch A/B signals, roll and yaw A/B signals

Data Acquisition
1. Quadrature decoding
   1. ← pitch A/B signals, routed roll and yaw A/B signals
   2. → encoder counts
2. Zeroing
   1. ← encoder counts, zero command, locked axes
   2. → encoder offsets
3. Angle and rate computation
   1. ← encoder counts, encoder offsets
   2. → gimbal angles, gimbal rates
4. Streaming
   1. ← gimbal angles, gimbal rates
   2. → time-stamped angle stream

Host Software
1. Test control
   1. ← operator commands
   2. → zero command, test markers
2. Attitude kinematics
   1. ← time-stamped angle stream
   2. → drone attitude, body rates
3. Live display
   1. ← drone attitude, body rates, over-speed warning
   2. → live angle readout
4. Logging
   1. ← time-stamped angle stream, drone attitude, body rates, test markers
   2. → time-stamped test logs
5. Analysis and export
   1. ← time-stamped test logs, drone flight log
   2. → response metrics, IMU-vs-encoder error, CSV export

Safety
1. Axis locks
   1. ← lock/unlock
   2. → locked axes
2. Over-speed monitor
   1. ← gimbal rates
   2. → over-speed warning
3. Procedures
   1. ← —
   2. → pre-test checklist, test rules

Power System
1. Rig supply
   1. ← USB 5 V
   2. → 5 V rig power

Electronics
1. DAQ board
   1. ← 5 V rig power
   2. → hosts DAQ firmware
2. Host PC
   1. ← —
   2. → hosts host software, USB 5 V
