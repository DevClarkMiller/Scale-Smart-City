# Intersection Controller Module

## Overview
The Intersection Controller coordinates traffic light behavior for a single intersection in the embedded system. It owns the directional light controllers, routes module commands to those lights, and reports vehicle detections upstream.

At a high level, this module acts as the "traffic orchestration" layer between:
- hardware-facing light/sensor components, and
- command/event flows coming from the rest of the system.

## Core Responsibilities
- Manage up to four directional light controllers (one per cardinal direction).
- Load/save intersection light configuration through JSON serialization.
- Apply light-state changes by orientation axis (for example, north/south vs east/west).
- Process traffic-control commands such as color changes, emergency mode, and sensor calibration.
- Forward car detection events to the backend command pipeline.

## Command Handling (High Level)
The controller accepts command messages and maps them to intersection actions. Supported command categories include:
- Set axis lights to a traffic state (red, yellow, green).
- Enter emergency mode.
- Calibrate a light's detection sensor.

Unknown or invalid commands are rejected with an error response.

## Emergency Behavior
When emergency mode is enabled, normal per-light updates are paused and all lights are driven through a flashing emergency pattern. This pattern toggles at a fixed interval until emergency mode is cleared by a normal light-state command.

## Car Detection
Each directional light may include a downward-facing ultrasonic sensor near the stop line. When a valid object height is detected, the controller sends a car-detection command event that includes:
- the direction where detection occurred, and
- the measured height value.

This allows the backend/simulation layer to react to real-time vehicle presence.

## Command Structure and Expected Returns

### Endpoint
Intersection Controller commands use the shared module command route:

```text
POST /module/{moduleId}/cmd/{cmdName}
Content-Type: application/json
```

Where:
- `moduleId` is the numeric id of the `IntersectionController` module instance.
- `cmdName` is one of: `red`, `yellow`, `green`, `emergency`, `calibrateLight`.

### Request Body by Command

#### Axis light control (`red`, `yellow`, `green`)
```json
{
	"orientation": "Vertical"
}
```
Notes:
- `orientation` is passed to the orthogonal-axis parser used by the controller.

#### Emergency mode (`emergency`)
```json
{}
```

#### Sensor calibration (`calibrateLight`)
```json
{
	"direction": "North"
}
```

### Expected Return Values
Single-command responses are plain text messages with HTTP status code + content type from `ResponseType`.

#### `red` / `yellow` / `green`
- `200 OK` with message like: `Made red`.
- `400 Bad Request` with message like: `No lights made red`.

#### `emergency`
- `200 OK` with message: `Emergency mode activated`.

#### `calibrateLight`
- `200 OK` with message: `Calibrated`.
- `400 Bad Request` with message: `Invalid direction`.
- `404 Not Found` with message: `No light with that direction`.
- `404 Not Found` with message: `No sensor on this light`.

#### Unknown command
- `404 Not Found` with message: `Unknown Command`.

## Test Requests

### 1) Set north/south axis to green
```bash
curl -i -X POST "http://device.local/module/0/cmd/green" \
	-H "Content-Type: application/json" \
	-d '{"orientation":"Vertical"}'
```

Expected outcome:
- `HTTP/1.1 200` and body similar to `Made green` when matching lights exist.
- `HTTP/1.1 400` and body similar to `No lights made green` when none match.

### 2) Enable emergency mode
```bash
curl -i -X POST "http://device.local/module/0/cmd/emergency" \
	-H "Content-Type: application/json" \
	-d '{}'
```

Expected outcome:
- `HTTP/1.1 200` with body `Emergency mode activated`.

### 3) Calibrate north light sensor
```bash
curl -i -X POST "http://device.local/module/0/cmd/calibrateLight" \
	-H "Content-Type: application/json" \
	-d '{"direction":"North"}'
```

Expected outcome:
- `HTTP/1.1 200` with `Calibrated`, or
- `HTTP/1.1 404` with `No light with that direction` / `No sensor on this light`.

## Optional Batch Test
You can also test through the batch endpoint:

```bash
curl -i -X POST "http://device.local/modules/cmds" \
	-H "Content-Type: application/json" \
	-d '{
		"commands": [
			{"moduleId":0,"cmdName":"green","command":{"orientation":"Vertical"}},
			{"moduleId":0,"cmdName":"emergency","command":{}}
		]
	}'
```

Expected batch response body is JSON with one result per command:

```json
[
	{"moduleId":0,"cmdName":"green","code":200,"message":"Made green"},
	{"moduleId":0,"cmdName":"emergency","code":200,"message":"Emergency mode activated"}
]
```