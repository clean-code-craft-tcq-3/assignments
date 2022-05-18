# Recap of Extension

[Abstracting the comparison prevents repeating changes](https://github.com/clean-code-craft-tcq-3/simple-monitor-in-py-bipin-raju-007/blob/d8e91d020b1bc760fd993aa55f6b27090ed14af0/battery_vitals.py)

[Data-driven approach with dependency injection](https://github.com/clean-code-craft-tcq-3/simple-monitor-in-cpp-YogeshGovindaraju/blob/b6a8a9fd1eccd7844abf7724b71f30e117cb6aaf/ChargeRateManager.h)

## Test individual functions, then sample the integration

    assert(get_unit_from_feature('30F')=='F')
    assert(get_value_from_feature('20C') == 20)
    assert(temperature_is_ok('1F') is True)
    assert(temperature_is_ok('-2C')is False)
    assert(soc_is_ok(20)is True)
    assert(soc_is_ok(15)is False)
    assert(charge_rate_is_ok(0.9)is False)
    assert(charge_rate_is_ok(0.8)is True)
    assert(battery_is_ok('25F', 70, 0.7) is True)
    assert(battery_is_ok('50C', 85, 0) is False)

... however, warnings are not tested here. Isolate the warning checks to easily test those conditions.
