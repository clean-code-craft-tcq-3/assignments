# Recap of naming

- File names as function names - need to use nouns such that it denotes the purpose of the file. For example- get_color_and_pair_number.py , here the file name used is like a function name. A name like color_pair_translation.py would express its purpose.
- A function name needs to indicate its action. Example- ColorCatalogue() could be named as PrintColorCatalogue()
- Function name MapColornamestoPairnumber() gives a first impression that the names and pair number are mapped and could be used in the program somewhere. But in fact all it was doing was just print the manual. Hence renaming to a suitable name is necessary
- Usage of magic numbers - for now the number of minor colors and major colors combination add to 25. However, the number 25 in a corner of the code would be forgotten when we add more colors.

```c
void MapColornamestoPairnumber() {
  for (int i=1; i<=25 ; i++) {
      ...
  }
}
```

## Test and production code

Don't mix them

```c
    printf("PRINTING MANUAL\n");
    for(int i =1 ;i<26;i++)
    {
        colorPair = GetColorFromPairNumber(i);
        printf("majorcolor-%s,minorcolor-%s,%d-pairNumber\n",MajorColorNames[colorPair.majorColor],MajorColorNames[colorPair.minorColor],i);
    }
    printf("DO TEST VERIFICATION\n");
    testNumberToPair(4, WHITE, BROWN);
    testNumberToPair(5, WHITE, SLATE);
```

## Add functionality

[Use a new file for new functionality](https://github.com/clean-code-craft-tcq-3/well-named-in-c-SagarBHiranna/blob/c1742dc6c7d3d50a6a45d205dee2feccd157b930/ReferenceManual.c)
