# Recap of naming
- File names named as function names - need to use nouns such that it gives an indication of the concepts or content. For ex. get_color_and_pair_number.py , here the file name used is like a function name.
- Funtion names should be indicating an action or what it does. ex. ColorCatalogue() could be named as PrintColorCatalogue()
- Good attempt to write segregated API vs implementation , and well named functions/files - [example](https://github.com/clean-code-craft-tcq-3/well-named-in-cpp-Veeresh-Ranjan/pull/1/files
)
-Choose right funtion name - function name MapColornamestoPairnumber() gives a first impression that the names and pair number are mapped and cached that could be used in the program somewhere. But in fact all it was doing was just print the manual. hence renaming to a suitable name is necessary
- Usage of magic numbers - for now the number of minor colors and major colors combination add to 25 if thisnumber is used, this poses a problem when the color codes are extended in future
```
void MapColornamestoPairnumber()
{
  for (int i=1; i<=25 ; i++)
  {
   const int MAX_COLORPAIR_NAME_CHARS = 16;
   ColorPair colorPair = GetColorFromPairNumber(i);
   char colorPairNames[MAX_COLORPAIR_NAME_CHARS];
   ColorPairToString(&colorPair, colorPairNames);
   printf("Pair number:%d:%s\n", i,colorPairNames);
  }
}
```