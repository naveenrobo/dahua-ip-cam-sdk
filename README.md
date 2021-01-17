# Dahua SDK
SDK for Dahua IP Cameras to extract Plate Numbers and listening of events like Video Motion, Camera Tampering which are support by camera.

## Info

API's are extracted by reverse engineering the JavaScript in Web UI. 

## Example Snippet

Login to camera
```py
from dahua_rpc import DahuaRpc

# Initialize the object
dahua = DahuaRpc(host="192.168.1.10", username="admin", password="password")

# Login to create session
dahua.login()
```

Some basic functions
```py
# Get the current time on the device
print(dahua.current_time())

# Set display to 4 grids with first view group
dahua.set_split(mode=4, view=1)

# Make a raw RPC request to get serial number
print(dahua.request(method="magicBox.getSerialNo"))
```

Get ANPR details
```py
# Get the ANPR Plate Numbers by using the following
# Get the object id
object_id = dahua.get_traffic_info() 

# Use the object id to find the Plate Numbers
dahua.start_find(object_id=object_id) 

# Find and dump the Plate Numbers
response = json.dumps(dahua.do_find(object_id=object_id)) 
```


Listening for event's like video motion, tamper detection
```py
# Attach an event. 
# NOTE : Check your camera model for possible events.
# Detaching an event is not yet supported.
print(dahua.attach_event(["VideoMotion"]))


# Create a callback to receive the data
def callback(data):
    print("Data = {}".format(data))

print(dahua.listen_events(callback))

# NOTE: Currently everything happens in a main thread. Will be moved to a thread in later update
```

## Credits

Forked from [this gist](https://gist.github.com/gxfxyz/48072a72be3a169bc43549e676713201). Thanks [G.X.F.](https://gist.github.com/gxfxyz) for your contribution.
