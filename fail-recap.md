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

## Keep test code seperate 

Assert is part of production code
```cpp
void checkPairNumberValidity(int pair_no)
 {
    assert(pair_no>=1 && pair_no<=25);
}

void displayPairNumber(int x, int y)
{
    int pair_number = x * 5 + y;
    std::cout<<pair_number+1;   //Pair numbers should start from 1
    checkPairNumberValidity(pair_number);
}
```

# Do not create different paths for test and production in production code

A function pointer that points to the stub or actual production code can be used and injected into production code. Hence production code will be agnostic of which function it is calling.

```c
        celcius = (farenheit - 32) * 5 / 9;
        printf("ALERT: Temperature is %.1f celcius.\n", celcius);
        if (environment == Test)
        {
            returncode = stub(celcius);
        }
        else
        {
            //Integration environment
            returncode = network(celcius);
        }
        if (returncode != 200) 
        {
        // non-ok response is not an error! Issues happen in life!
        // let us keep a count of failures to report
        // However, this code doesn't count failures!
        // Add a test below to catch this bug. Alter the stub above, if needed.
        alertFailureCount += 0;
        }
    ```