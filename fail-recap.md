# Recap - avoiding false positives

[Separation of stub](https://github.com/clean-code-craft-tcq-3/test-failer-in-cpp-YogeshGovindaraju) from real code

## Making behavior 'observable' by writing logs

In the [snippet](https://github.com/clean-code-craft-tcq-3/test-failer-in-cpp-YogeshGovindaraju/blob/824adba4576e416139cea214afd7cc537327aa92/misaligned.cpp) below, observability is achieved by setting the globals `number`, `majorColorList` and `minorColorList`. In production projects, it would be logging.
```cpp
    for(i = 0; i < 5; i++) {
        for(j = 0; j < 5; j++) {
            std::cout << i * 5 + j << " | " << majorColor[i] << " | " << minorColor[i] << "\n";
            number.push_back(i * 5 + j);
            majorColorList.push_back(majorColor[i]);
            minorColorList.push_back(minorColor[i]);
        }
    }
...
    assert(number.at(0) == 1);
    assert(majorColorList.at(0) == "White");    
...
```

## Asserts to state functionality

Make choices and express them, not just fail the build. These asserts will fail even after we fix the code.

```cpp
    assert(size(38) == 'S');
    assert(size(38) == 'M');
```
