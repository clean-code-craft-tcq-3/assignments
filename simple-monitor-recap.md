# Recap - Simple monitor

## Test value range 
Test values should cover out of range values, boundary values and in range values

An example of test coverage -

- [range tests](https://github.com/clean-code-craft-tcq-3/simple-monitor-in-cpp-arpit091429/pull/1/files)
- [testing whole and parts](https://github.com/clean-code-craft-tcq-3/simple-monitor-in-cpp-YogeshGovindaraju/blob/c08a64d7f41789554d4302267a55ae66d1c8a496/checkerTest.h)

## Reduce duplication, increase re-use

[Re-usable `BatteryVital` to reduce duplicated checks](https://github.com/clean-code-craft-tcq-3/simple-monitor-in-py-bipin-raju-007/blob/8997b3be0d7abbca42ff1018efa2ee5f02a2a129/check_limits.py)

## Test the parts, then test the whole

```c
  assert(isBatteryTemperatureOk(25));
  assert(!isBatteryTemperatureOk(50));
  assert(!isBatteryTemperatureOk(-1));

  assert(isBatteryChargeStateOk(25));
  assert(!isBatteryChargeStateOk(90));
  assert(!isBatteryChargeStateOk(10));
  
  assert(!isBatteryChargeRateOk(1.0));
  assert(!isBatteryChargeRateOk(0.8));
  assert(isBatteryChargeRateOk(0.7));
  
  assert(batteryIsOk(25.0, 70.0, 0.7));
```

Would be even better if the range comparison was separated into a function, e.g., `isReadingInRange`

## Un-intended shared state and incomplete tests

Avoid use of globals...

```c
int flag = 0;
```

...to accumulate errors

```c
if(chargeRate > MAX_CHARGERATE) {
    flag+=1;
    ...
}
```

...and then conclude

```c
if (flag > 0) {
    return 0;
} else {
    return 1;
}
```

...with incomplete tests

```c
  assert(batteryIsOk(35.0, 20.0, 0.5));
  assert(!batteryIsOk(46.0, 82.0, 0.8));
  // after this point, any call will find flag > 0 and return false
  // (even if all parameters are in range)
  // But it passes because no such tests are there...
  // Moral: Avoid use of globals
```
