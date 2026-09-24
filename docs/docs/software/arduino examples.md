# Arduino Examples

## Example 01 - Basic Readings

The first example demonstrates the simplest way to get data from the SparkFun CO<sub>2</sub> Sensor - STCC4/SHT40 (Qwiic). This example initializes the sensors and starts continuous measurement to read CO<sub>2</sub> concentration, temperature and relative humidity roughly once per second. Open the example by navigating to **File** > **Examples** > **SparkFun STCC4 Arduino Library** > **Example01_BasicReadings**. Select your Board and Port and click the "Upload" button. After the code finishes uploading, open the serial monitor with the baud set to **115200** and you should see readings for CO<sub>2</sub>C in ppm, temperature in &deg;C and relative humidity in %RH.

Note, for the first 20 seconds after first ever power up the STCC4 outputs a fixed bypass value for CO<sub>2</sub> of 390 ppm.

## Example 02 - Low Power Single Shot

Example 2 shows how to use the STCC4 in single shot mode to operate in a low power environment. This example sets up a 10 second sampling interval for the STCC4 to wake up, trigger a single shot measurement and then returns the sensor back to sleep mode:

``` c++
delay(kSamplingIntervalMs);

mySensor.exitSleepMode();
mySensor.measureSingleShot();
mySensor.readMeasurement();
```

You can adjust the sample interval to whatever you'd like by adjusting this line:

``` c++
const unsigned long kSamplingIntervalMs = 10000;
```

We recommend keeping it between 5 and 600 seconds to keep the STCC4's automatic self-calibration algorithm working correctly.

## Example 05 - Forced Recalibration

The fifth example shows how to force the STCC4 to perform a recalibration using a known reference concentration. This is helpful if you need to recalibrate the sensor immediately either during initial installation or if it cannot regularly see fresh air. 

Before running this example, make sure the board is in air with a known CO<sub>2</sub> concentration. Outdoor air works decently, it has an average concentration of 420 ppm. Then, set the `kReferenceCO2` value *below* your reference value. The example runs the STCC4 in continuous measurement mode for 60 seconds to stabilize the readings, then stops measurement. With the measurement stopped it performs the forced recalibration and prints out the correction the sensor applied. After the correction value is stored, the code resumes measurements in continuous mode.

## Example 06 - Pressure Compensation

The sixth example shows how to compensate for atmospheric pressure. The STCC4 assumes sea level air pressure (101,300 Pa) by default so if you're measuring at a different altitude or have a barometric pressure sensor handy to send true ambient air pressure this can improve the CO<sub>2</sub> measurement accuracy.

This example defaults to set the air pressure value for sea level, you can change that by adjusting this line:

``` c++
const uint32_t kAmbientPressurePa = 101325;
```

The code then uses that value to set the pressure compensation value here:

``` c++
mySensor.setPressureCompensation(kAmbientPressurePa);
```

