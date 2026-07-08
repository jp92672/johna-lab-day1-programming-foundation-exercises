# LAB PROOF | Day 1 | Programming Foundation Exercises
## John Adams

**Program path:** 
See homeguard_system.ipynb file

**Run command and output:** 
See homeguard_system.ipynb file

**Program function:**
The simulator defines a `Sensor` class for individual devices (temperature, motion, smoke detector, door, window, light) and a `Room` class that can have a list of devices, and a mode (home/away). Each cycle, every sensor generates a random variable, and the room's `alerts()` checks each reading against the abnormal condition definitations and the room's mode to decide whether to print an ALERT, ALARM, or NOTICE.

**Edge case:**
The `light` sensor's abnormal check originally used `self.value not in ["On"]`, which incorrectly flagged the light as abnormal when it was `"Off"`. It was fixed with `self.value == "On"`, so the alert only fires when the light is actually left on while away.