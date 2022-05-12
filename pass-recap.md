#  Recap - Fix production code to pass all tests

## Keep test code separate from production code.

> Test code = test cases + stubs

Production code should be agnostic of test environment or production environment. 

```cs
int returnCode = 0;
          float celsius = ConvertFarenheitToCelsius(farenheit);
          switch (environment)
          {
            case "Test":
              returnCode = NetworkAlert.AlertNetwork(celsius);
            break;
           case "Production":
             returnCode = NetworkAlertStub.AlertNetwork(celsius);
           break;
          }
```

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

## Test the functionality

The assert is on colorpair...

```c
  strcpy(colorpair[localPairNumber].MajorColor , majorColor[i]);
  strcpy(colorpair[localPairNumber].MinorColor , minorColor[j]);
  ...
  assert(strcmp(colorpair[23].MajorColor, "Violet") == 0);
  assert(strcmp(colorpair[23].MinorColor, "Green") == 0);
```

... while the actual-functionality to print on console isn't related to the asserts.

```c
  printf("%d | %s | %s\n", i * 5 + j, majorColor[i], minorColor[j]);
```
