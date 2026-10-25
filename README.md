# ma4012_ballCatcher
Files and code for the module MA4012, where we need to make a robot that competes with another robot for catching tennis balls inside an arena.

## Autonomous program

`main_ma4012.c` is the integrated ROBOTC program. It waits for the start button,
searches for balls with a left/right scan, steers toward a detected ball while
running the intake, checks the storage sensor, navigates to the configured box
approach point, and runs the release motor. It repeats this cycle until three
balls have been deposited or a bounded search, navigation, pickup, or release
attempt fails. The opponent-distance sensor and four line sensors are checked
while the robot moves. Drive and turn operations use the wheel encoders and
have timeouts.

### Calibrate before running

Edit the configuration block near the top of `main_ma4012.c` for the actual
robot and arena. The supplied geometry and positions are example values, not
measurements:

- Set the wheel diameter, wheel track (center-to-center spacing), encoder ticks
  per wheel revolution, and encoder polarity. Confirm that positive motor power
  drives both wheels forward and that the encoder signs match the configuration.
- Set arena width/height, robot length/width, starting robot center and heading,
  and the robot stopping point in front of the deposit box. Coordinates are in
  centimeters; heading zero points east (+X), and positive heading turns toward
  north (+Y).
- Calibrate the ball, opponent, storage, and boundary thresholds on the actual
  sensors. The starter code's analog thresholds are only initial estimates.
  `BOUNDARY_ACTIVE_LOW` selects whether a boundary line gives a lower or higher
  reading than the arena floor.
- Confirm that the two rear limit switches and the emergency-stop switch are
  normally-open touch switches. Their ROBOTC sensor types are set to
  `sensorTouch`; change them to match the installed hardware if necessary.
- Confirm the intake/release motor directions and tune the approach, scan,
  obstacle-clearance, and release settings for the mechanism.

The box has no dedicated range sensor in the provided sensor configuration, so
box navigation is encoder odometry to the configured approach point, not visual
box detection. Validate that point and the starting pose on the real field.
Likewise, line-sensor polarity, sensor thresholds, and encoder calibration must
be verified on the robot before an autonomous run. The directional digital
inputs are retained in the sensor configuration but are not used for navigation
because their physical function is not specified in the starter code.
