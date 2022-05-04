#  Recap - Fix production code to pass all tests

Keep test code such as test cases and test stubs separate from production code.

## Bug in Production code using 'for' indexes

The iterator for major index is 'i' and iterator for minor index is 'j'.
In the following code, 'i' is used for both. Such bugs can easily be caught if the test cases are present.

```c
 int pair_number;
    for (i = 0; i < 5; i++)
    {
        for (j = 0; j < 5; j++)
        {
            pair_number = (i * 5 + j)+1;
            std::cout << pair_number << " | " << majorColor[i] << " | " << minorColor[i] << "\n";
            checkPairNumberValidity(pair_number);
        }
    }
```