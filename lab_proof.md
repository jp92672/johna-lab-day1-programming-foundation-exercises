# LAB PROOF | Day 1 | Programming Foundation Exercises
## John Adams

**Program path:** 
See homeguard_system.ipynb file

**Run command:** 
# Room 1 set in away mode with all sensor types
room1_room = Room("Living Room", "away")
room1_room.sensors.append(Sensor("temperature", "Living Room"))
room1_room.sensors.append(Sensor("motion", "Living Room"))
room1_room.sensors.append(Sensor("smoke detector", "Living Room"))
room1_room.sensors.append(Sensor("door", "Living Room"))
room1_room.sensors.append(Sensor("window", "Living Room"))
room1_room.sensors.append(Sensor("light", "Living Room"))

# Room 2 set in home mode with all sensor types
room2_room = Room("Bedroom", "home")
room2_room.sensors.append(Sensor("temperature", "Bedroom"))
room2_room.sensors.append(Sensor("motion", "Bedroom"))
room2_room.sensors.append(Sensor("smoke detector", "Bedroom"))
room2_room.sensors.append(Sensor("door", "Bedroom"))
room2_room.sensors.append(Sensor("window", "Bedroom"))
room2_room.sensors.append(Sensor("light", "Bedroom"))

# Run 3 times to simulate variable readings and alerts, for every room
all_rooms = [room1_room, room2_room]
for i in range(3):
    print("=== HomeGuard Security System ===")
    print(f"Time: {datetime.datetime.now().strftime('%H:%M:%S')}")
    print()
    for room in all_rooms:
        print(f"Zone: {room.name} | Mode: {room.mode.upper()}")
        for sensor in room.sensors:
            sensor.read()
            print(f"[READING] {sensor.location} {sensor.sensor_type}: {sensor.value}")
        room.alerts()
        print()

**Output:**
```
=== HomeGuard Security System ===
Time: 12:46:10

Zone: Living Room | Mode: AWAY
[READING] Living Room temperature: 10.75742348189127
[READING] Living Room motion: Motion detected
[READING] Living Room smoke detector: Smoke detected
[READING] Living Room door: Closed
[READING] Living Room window: Closed
[READING] Living Room light: Off
⚠️ ALERT: Motion detected in Living Room while in away mode!
‼️ ALARM: Smoke detected in Living Room!

Zone: Bedroom | Mode: HOME
[READING] Bedroom temperature: 17.9177724349033
[READING] Bedroom motion: No activity
[READING] Bedroom smoke detector: No activity
[READING] Bedroom door: Closed
[READING] Bedroom window: Closed
[READING] Bedroom light: On
ℹ️ NOTICE: Temperature outside comfort zone in Bedroom!

=== HomeGuard Security System ===
Time: 12:46:10

Zone: Living Room | Mode: AWAY
[READING] Living Room temperature: -0.4506772815113482
[READING] Living Room motion: Motion detected
[READING] Living Room smoke detector: No activity
[READING] Living Room door: Closed
[READING] Living Room window: Closed
[READING] Living Room light: Off
⚠️ ALERT: Temperature abnormal in Living Room!
⚠️ ALERT: Motion detected in Living Room while in away mode!

Zone: Bedroom | Mode: HOME
[READING] Bedroom temperature: 6.360309407336361
[READING] Bedroom motion: No activity
[READING] Bedroom smoke detector: Smoke detected
[READING] Bedroom door: Closed
[READING] Bedroom window: Window open
[READING] Bedroom light: Off
ℹ️ NOTICE: Temperature outside comfort zone in Bedroom!
‼️ ALARM: Smoke detected in Bedroom!

=== HomeGuard Security System ===
Time: 12:46:10

Zone: Living Room | Mode: AWAY
[READING] Living Room temperature: 1.6348266391994093
[READING] Living Room motion: No activity
[READING] Living Room smoke detector: Smoke detected
[READING] Living Room door: Closed
[READING] Living Room window: Closed
[READING] Living Room light: On
‼️ ALARM: Smoke detected in Living Room!
⚠️ ALERT: Light is on in Living Room while in away mode!

Zone: Bedroom | Mode: HOME
[READING] Bedroom temperature: -1.7281562287354846
[READING] Bedroom motion: Motion detected
[READING] Bedroom smoke detector: Smoke detected
[READING] Bedroom door: Closed
[READING] Bedroom window: Closed
[READING] Bedroom light: Off
⚠️ ALERT: Temperature abnormal in Bedroom!
‼️ ALARM: Smoke detected in Bedroom!
```

**Program function:**
The simulator defines a `Sensor` class for individual devices (temperature, motion, smoke detector, door, window, light) and a `Room` class that can have a list of devices, and a mode (home/away). Each cycle, every sensor generates a random variable, and the room's `alerts()` checks each reading against the abnormal condition definitations and the room's mode to decide whether to print an ALERT, ALARM, or NOTICE.

**Edge case:**
The `light` sensor's abnormal check originally used `self.value not in ["On"]`, which incorrectly flagged the light as abnormal when it was `"Off"`. It was fixed with `self.value == "On"`, so the alert only fires when the light is actually left on while away.