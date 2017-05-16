# blur-doodles

How should we blur sensor values (technically, so that privacy is
protected)? How can we explain what "level of blur" achieves which
"level of privacy"? How can we further express a mapping from one
type of level to the other?

## Things to talk about
* Sensor name
* Physical unit(s), number of dimensions, sampling rate, quantization
* Privacy relevance
* Possible mitigation techniques and their properties (rate, accuracy)


### Accelerometer
Measures acceleration (m/s^2) of device in three spatial dimensions, at up to 200 Hz
(as per Android 7) and around 12 bits of nominal accuracy.

Exposes
* low-frequency audio
* user tapping on the touch screen
* LF motion (car/train/walking).
* Readings include standard gravity, and thus yield a vector indicative
  of the orientation of the device.
* Sensor exhibits device-specific noise pattern.

Rate limiting:
* Low-pass filter as desired.
* Fixed rates may still serve to undersample regular motion patterns.

Accuracy reduction:
* Round to specific precision. **How effective is this?**



### Gyroscope

Measures angular velocity (rad/s) of the device around three spatial
dimensions, at up to 200 Hz (cf. GyroPhone) and **unknown resolution**.

For privacy relevance and mitigations see Accelerometer.



### Magnetometer

Measures the ambient magnetic field (uT) of the device along three spatial
dimensions, at an **unknown rate** and **unknown resolution**.

Exposes
* Orientation of the device in comparison to Earth's magentic field.

For other privacy relevance and mitigations see Accelerometer.



### WiFi

When connected to an access point, it shows its name (SSID),
MAC address (BSSID), frequency, capabilities, RSSI, link speed;
also the device's MAC and IP addresses.

When scanning, it shows every nearby access point's SSID, BSSID,
frequency, capabilities.

Exposes
* Physical device location, as WiFi names and MAC addresses can be mapped.
* See any location-type sensor for further implications.

Rate limiting: See other location-type sensors.

Accuracy reduction:
* Suppress/randomize (B)SSIDs. Still exhibits some info about the spectrum,
  worth investigating for fingerprintability etc.
* Hash and salt (B)SSIDs, keepi the salt constant across vessels
  of one experiment.



### Bluetooth

#### `get_bluetooth_info`

Returns a locally-administered MAC address
("02:..."), device name, interface state (on/off, turning on/off),
and scan mode (none, connectable, connectable and discoverable) of
the device.

Exposes
* The device name which might be unique and/or reference the user by name.

Rate limiting: Likely doesn't help because the Bluetooth name of the
device won't change very often; the scan mode might though.

Accuracy reduction: See WiFi interface.



#### `get_bluetooth_scan_info`

Scans for Bluetooth devices in the vicinity.

Exposes for every scanned device the
* MAC address
* "Device type", i.e. a [broad classification of Bluetooth interface capabilities](https://developer.android.com/reference/android/bluetooth/BluetoothDevice.html#DEVICE_TYPE_CLASSIC)
* "Bond state", i.e. whether this device has been paired (or is currently
  pairing) with the owner's device and can communicate encrypted.

Note: Bluetooth device names are currently [**not** exposed](https://github.com/aaaaalbert/sensibility-testbed/commit/68f0b5b6e708903bbfb728a61d7da082fc526898#diff-33ae59376f054824ee6480e4b9dcc0e9R661)

Rate limiting, accuracy reduction: See WiFi interface.
