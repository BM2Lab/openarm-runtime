# openarm-runtime contributor instructions

## Ownership and upstream integration

This repository owns physical OpenArm interfaces, kinematics/control adapters,
guards/stopping, single-/bimanual session authority and LeRobot device adapters.
Depend on lightweight `contracts`, not `learning` or Isaac. Package imports must
not require CAN/ROS/vendor libraries, connect to devices or start control threads.
Select optional backends explicitly.

Inspect and pin the relevant upstream vendor/LeRobot/ROS implementation before
rewriting drivers. Document the physical hardware revision and exact chosen
software/firmware versions; do not assume all OpenArm variants share limits or
protocols. Preserve provenance and behavioral parity when extracting code.

## Hardware semantics and safety

Verify per-unit joint order, motor IDs, CAN interface identity, encoder zero
offsets, units/signs, URDF/FK, frames/TCP, grippers, limits and leader/follower
topology before any command path. Bimanual operation requires explicit shared
timing, command ownership and coordinated fault/stop semantics; it is not merely
two independent clients.

Keep final guards, watchdogs and validated stopping local to the runtime.
Record command acceptance/interventions, state validity and timestamps. Python
teleop/policy orchestration is not a substitute for device/runtime protection.
Do not assume a Franka-style torque controller or stop procedure applies here.

Default development/tests are offline/read-only/mock/shadow. Connections, motion,
homing/calibration, recovery and changes to safety behavior need explicit separate
authorization and a reviewed per-unit procedure. CI must never actuate hardware.

## Development, artifacts and current status

Use an isolated pinned environment; no required parent `AGENTS.md`, workstation
path, sibling checkout or shared simulator/ML environment. Configure device
identity and artifact locations externally; never auto-select an available CAN
device as a live default or use a copied venv as qualification evidence.

```bash
python -m pytest tests --import-mode=importlib
```

Test pure imports, serialization, joint/frame conversion and mock backend behavior
without hardware; add source/backend parity and coordinated fault/stop tests as
implementations arrive. Keep large logs, recordings, native builds and binary
artifacts outside Git. Retain lightweight fixtures, per-unit configuration and
provenance/qualification manifests. Check explicit output paths for availability
and capacity; buffer high-rate logs off the control loop.
This scaffold supplies no working driver, calibrated robot or motion approval.
