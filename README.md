[**js-aruco**](https://github.com/jcmellado/js-aruco) is a JavaScript port by jcmellado of the ArUco library. This module adapts that browser library slightly to work in Node.js.

[ArUco](http://www.uco.es/investiga/grupos/ava/node/26) is a minimal library for Augmented Reality applications based on OpenCV.

### Usage ###
Create an `AR.Detector` object:

```
var AR = require('js-aruco').AR;
var detector = new AR.Detector();
```

Call `detect` function:

```
var markers = detector.detect(imageData);
```

`markers` result will be an array of `AR.Marker` objects with detected markers.

`AR.Marker` objects have two properties:

 * `id`: Marker id.
 * `corners`: 2D marker corners.

`imageData` argument must be a valid `ImageData` canvas object. The [pixel](https://www.npmjs.com/package/pixel) suite of modules may be helpful for constructing these in Node.

### 3D Pose Estimation ###
Create an `POS.Posit` object:

```
var POS = require('js-aruco').POS1;
var posit = new POS.Posit(modelSize, canvas.width);
```

`modelSize` argument must be the real marker size (millimeters).

Call `pose` function:

```
var pose = posit.pose(corners);
```

`corners` must be centered on canvas:

```
var corners = marker.corners;

for (var i = 0; i < corners.length; ++ i){
  var corner = corners[i];

  corner.x = corner.x - (canvas.width / 2);
  corner.y = (canvas.height / 2) - corner.y;
}
```

`pose` result will be a `POS.Pose` object with two estimated pose (if any):

 * `bestError`: Error of the best estimated pose.
 * `bestRotation`: 3x3 rotation matrix of the best estimated pose.
 * `bestTranslation`: Translation vector of the best estimated pose.
 * `alternativeError`: Error of the alternative estimated pose.
 * `alternativeRotation`: 3x3 rotation matrix of the alternative estimated pose.
 * `alternativeTranslation`: Translation vector of the alternative estimated pose.

Note: POS namespace can be taken from `require('js-aruco').POS1` or `.POS2`.
