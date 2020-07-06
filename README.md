# DahuaANPRSDK
SDK for Dahua ANPR Cameras to extract Plate Numbers

## Info

ANPR API's are extracted by reverse engineering the JavaScript in Web UI

## Example Snippet

```py
from dahua_rpc import DahuaRpc

dahua = DahuaRpc(host="192.168.1.10", username="admin", password="password")
dahua.login()

# Get the current time on the device
print(dahua.current_time())

# Set display to 4 grids with first view group
dahua.set_split(mode=4, view=1)

# Make a raw RPC request to get serial number
print(dahua.request(method="magicBox.getSerialNo"))

# Get the ANPR Plate Numbers by using the following
object_id = dahua.getTraficInfo() # Get the object id
dahua.startFind(object_id=object_id) # Use the object id to find the Plate Numbers
response = json.dumps(dahua.doFind(object_id=object_id)) # Extract the Plate Numbers
```
