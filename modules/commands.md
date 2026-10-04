# Commands
Commands are received by the HTTP API exposed by the embedded device and are routed to the appropriate module depending on the URL. The device listens on port 80 (or 443 when TLS is enabled) for POST requests carrying command payloads.

## Modules
Each Module supports the expected GET/PUT/POST/DELETE methods.

## API route
device_hostname/module/{module_id}/cmd/{cmd_name}

Path params:
* **module_id** - numeric module instance id.
* **cmd_name** - command identifier from the URL.

The JSON command payload is sent in the HTTP POST body.

## Format
### Field descriptions
* **body** - the full JSON POST body for the command.
* **params** - the URI path params from the route (`module_id`, `cmd_name`), not JSON fields inside the body.
> The entire object must be valid JSON and not exceed the device’s maximum request size (currently ~2 KB).

## Examples

### Simple command with params
```bash
curl -X POST \
  http://device.local/module/3/cmd/setColor \
  -H 'Content-Type: application/json' \
  -d '{"r":255,"g":80,"b":20}'
```

### Complex payload in body
```bash
curl -X POST http://device.local/module/1/cmd/log \
  -H 'Content-Type: application/json' \
  -d '{"level":"warn","message":"Temperature high"}'
```

### HTTP library (Python) example
```python
import requests

def send_command(host, module_id, cmd):
  url = f"http://{host}/module/{module_id}/cmd/log"
    r = requests.post(url, json=cmd)
    r.raise_for_status()
    return r.json()

cmd = {"level": "warn", "message": "Temperature high"}
print(send_command("device.local", 2, cmd))
```

## Routing and dispatch
The API route has the form:

```
device_hostname/module/{module_id}/cmd/{cmd_name}
```

* `module_id` is the numeric instance within that class.
* `cmd_name` is the command name taken from the URL path.

When a request arrives the device:
1. Looks up the `Module` instance matching the type and id.
2. Parses the JSON POST body into a `JsonObject`.
3. Calls `module->handleCommand(cmd)`; the module returns a `ResponseType` indicating success or error.
4. The response object (see below) is serialized and sent back to the caller.

If the module cannot be found, the server responds with **404 Not Found**. Malformed JSON results in **400 Bad Request**.

## Extending the command set
To add a new command:
1. Modify the appropriate module’s `handleCommand` override.
2. Update `docs/modules/module_name.md` with the new command route params (`module_id`, `cmd_name`), expected JSON body, and examples.
3. Rebuild and flash the firmware.

Each `Module` subclass should document its supported names either in comments or a separate README.

## Batching Commands

You can send multiple commands in a single HTTP POST request using the batch endpoint. This is useful for reducing network overhead and ensuring multiple operations are performed together.

### Batch Endpoint
```
device_hostname/modules/cmds
```

### Batch Command Format
The request body should be a JSON object with a `commands` array. Each item in the array must have the following structure:

```json
{
  "moduleId": 1,
  "cmdName": "string",
  "command": { /* command object */ }
}
```
- **moduleId**: The numeric ID of the target module.
- **cmdName**: The command name to invoke (e.g., `setColor`).
- **command**: The command object or parameters, as required by the module and command.

#### Example Batch Request
```bash
curl -X POST http://device.local/modules/cmds \
  -H 'Content-Type: application/json' \
  -d '{
    "commands": [
      { "moduleId": 1, "cmdName": "setColor", "command": {"color": "red"} },
      { "moduleId": 2, "cmdName": "setBrightness", "command": {"level": 80} }
    ]
  }'
```

#### Example Batch Request (Python)
```python
import requests

batch = {
    "commands": [
        {"moduleId": 1, "cmdName": "setColor", "command": {"color": "red"}},
        {"moduleId": 2, "cmdName": "setBrightness", "command": {"level": 80}}
    ]
}
resp = requests.post("http://device.local/modules/cmds", json=batch)
print(resp.json())
```

### Batch Response
The response will be a JSON array with the result for each command, in the same order as sent. Each result will indicate success or error for the corresponding command.

---

*Last updated: March 2026.*