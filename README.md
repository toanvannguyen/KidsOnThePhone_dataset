# KidsOnThePhone_dataset
A data set contains touch and sensors data of children and adults interactions on mobile devices.

This is the data set collected and used in the `Kid on The Phone` paper

```
Toan Nguyen, Aditi Roy and Nasir Memon, "Kid on The Phone! Toward Automatic Detection of Children on Mobile Devices", Computers & Security, Volume 84, July 2019, Pages 334–348.
```

### Overview
This data set was collected in a study with a goal to develop algorithms for automatic detection of children on mobile devices. In our work, we devised several methods to distinguish children from adults based on behavioral differences while operating a touch-enabled modern computing device. Behavioral differences are extracted from data recorded by the touchscreen and built-in sensors. Our results showed that it is possible to achieve 99% accuracy and less than 0.5% error rate after 8 consecutive touch gestures using only touch information or 5s of sensor reading. If information is used from multiple sensors, then only after 3 gestures, similar performance could be achieved.

The data set had been created from 50 children and adults who interacted with off-the-shelf applications on smartphones. The data set includes touch and sensor data of 25 kids (age range 3.5--12, average 6.6) and 25 adults (age range 24--66, average 36), mostly parents of kid subjects. The data set in this repo is stored in two directories: `Kids` contains data of children subjects and `Parents` contains data of adult subjects. The data of each subject is stored in a subdirectory within these two directories has following structure.
- SubjectID dir, i.e., `Kid1`
------`Touch`: subdirectory contains __touch__ data of the subject. Under this directory, there are subdirs, i.e, `1499123735344_kid`, where each subdir contains the data of a session. Most subjects only have one session.
------`Sensors`: subdirectory contains __sensors__ data of the subject. Under this directory, there are subdirs, i.e, `1499123735344_kid`, where each subdir contains the data of a session. Most subjects only have one session.
------`listApps.json`: This is a file that maps all the apps on the device to app IDs. The app IDs were used in sensor data (the last column).

### Touch data format

In each session directory, the touch data is stored in a JSON file with format `session_timestamp.json`, i.e., `1499123737171.json`. The touch data includes following fields.
        + _dimX_, _dimY_: the screen size of the phone used in the data collection. In our study, we used a __Nexus 6__ phone to collect data from all subjects.
        + _gestures_: a list of touch gestures captured in the session. Each touch gesture has following data:
          ```
	          {
		      "12": "Swipe",  --> Gesture ID and gesture type
		      "app": "com.google.android.apps.photos",  --> The name of the app on which the gesture was performed and captured
		      "points": [
		        {"o":true,"Ts":[{"p":56,"t":1499123762947,"s":6,"x":1146,"y":1478},{"p":56,"t":1499123762969,"s":6,"x":1117,"y":1481},{"p":56,"t":1499123762977,"s":6,"x":1099,"y":1482},{"p":56,"t":1499123762986,"s":7,"x":1074,"y":1483},{"p":56,"t":1499123762993,"s":6,"x":1038,"y":1483},{"p":56,"t":1499123763001,"s":7,"x":988,"y":1485},{"p":56,"t":1499123763014,"s":6,"x":937,"y":1487},{"p":56,"t":1499123763020,"s":6,"x":886,"y":1494},{"p":56,"t":1499123763027,"s":5,"x":835,"y":1503},{"p":56,"t":1499123763036,"s":4,"x":784,"y":1519},{"p":32,"t":1499123763045,"s":2,"x":735,"y":1536}]}
		      	] --> A list of touch points
		       },
    	```
  
where
    	
    	    + `o`: orientation of the phone. `true`: vertical, `false`: horizontal
    	    + `Ts`: touch sequence. Contains a list of touch points where each touch point has:
    	      + `p`: pressure
    	      + `s`: size of touch finger
    	      + `x`: x-coordinate, the _x_ location of a touch point on the screen
    	      + `y`: y-coordinate, the _y_ location of the touch point on the screen
    	      + `t`: timestamp in UTC
    	      
__Note__: To normalize pressure and size value to _[0, 1]_, use pressure normalization scale provided by the device used in the data collection process. See details: https://source.android.com/devices/input/touch-devices#pressure-field. For our device, this pressure_scale is __0.013__.

Please note that gesture ID may not start from 1 because initial gestures,  which belonged to the experimenter who helped carry out a data collection session, were removed from the data of a subject.

### Sensor data format

In each session directory, there are subdirs of sensor types. Each subdir contains data of a sensor type during the data collection session, including, acelerometer, gyroscope, gravity, linear acceleration, magnetic, orientation, and rotation.

In each sensor subdir, there are `*.txt` files that contain captured data of the sensor. Each filename is a timestamp when the file was created. Each file has 5 columns:
          + `timestamp` in UTC: this timestamp should be used when combining with touch data
          + `sensor_timestamp`: sensor internal timestamp
          + The next three columns are sensor measurements along three axes `x,y,z`
          + The last column is the `app ID` (which app the subject was using when the data was captured). The app ID can be mapped to an app name using the file `listApps.json` described above.

### Kid subject age details
| Subject ID | Age |
|------------|-----|
| Kid1       | 9   |
| Kid2       | 11  |
| Kid3       | 9   |
| Kid4       | 7   |
| Kid5       | 9   |
| Kid6       | 5   |
| Kid7       | 7   |
| Kid8       | 7   |
| Kid9       | 4   |
| Kid10      | 4   |
| Kid11      | 7   |
| Kid12      | 5   |
| Kid13      | 6   |
| Kid14      | 7   |
| Kid15      | 8   |
| Kid16      | 7   |
| Kid17      | 7   |
| Kid18      | 10  |
| Kid19      | 12  |
| Kid20      | 3.5 |
| Kid21      | 5   |
| Kid22      | 3.5 |
| Kid23      | 5   |
| Kid24      | 4   |
| Kid25      | 4   |


### Reference

Kindly cite following article in any of your publication that benefits from the this data set:

__Toan Nguyen__, Aditi Roy and Nasir Memon, ``Kid on The Phone! Toward Automatic Detection of Children on Mobile Devices'', Computers & Security, Volume 84, July 2019, Pages 334–348.

__bibtex__:
```
@article{nguyen2019kid,
  title={Kid on the phone! Toward automatic detection of children on mobile devices},
  author={Nguyen, Toan and Roy, Aditi and Memon, Nasir},
  journal={Computers \& Security},
  volume={84},
  pages={334--348},
  year={2019},
  publisher={Elsevier}
}
```

__PDF__: [Kid on the phone paper](https://arxiv.org/abs/1808.01680)