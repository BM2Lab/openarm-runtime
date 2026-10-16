# openarm-runtime

Offline-first runtime scaffold. Install with ../robot-learning/packages/contracts,
not the learning package. Importing this package never connects to hardware.

Evaluate upstream OpenArm integration before implementing drivers. Inventory hardware revision, CAN identity, joint order, zero offsets and coordinated bimanual capabilities first.

No backend, controller, stop path or physical deployment is implemented or
approved. The workstation supports pure/offline tests only. Receiving control
hosts maintain separate pinned environments; do not copy this machine's venv.
