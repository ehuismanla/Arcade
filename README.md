# Arcade
Arcade script for use in ArcGIS Pro and ArcGIS Online

This script can be used to edit street names in an attribute table to ensure that they are properly formatted. This means that the first letter of street names will be capitalized.
In addition, directional components (N, E, S, W, etc.) as well as street type abbreviations (St., Rd., Ave., etc.) are also properly capitalized.
However, ordinal text following numbers (44th, 3rd, 21st, etc.) are always lowercase.
At present, the script can manage any road name with up to 7 words/sections, however most streets only contain 2 words/sections, or 3 if they have a directional letter at the start.
It is applied by right-clicking on the field name, selecting “calculate field”, selecting “Arcade” as expression type, and pasting the code into the box at the bottom; just make sure to correctly input the “FIELDNAME” in the first line.

Explanation:
Variable “s” calls in the feature of which you are trying to edit the streets field of. Simply replace the text “FIELDNAME” with the name of the field you are trying to reformat.

Variable “a” is an array which contains string-formatted numbers. It contains all possible digits and is referred to later in the code in order to identify streets with numbers in their name and ensure proper ordinal formatting.

Variable “b” is an array which contains all of the two-directional abbreviations, in all possible formatting styles.

Variable “x” splits the street name at each space, creating an array where each segment of the street name is its own entity.
The next block of code, beginning with variable “y” , analyzes the first item in the array contained by variable “x”. Variable “y” is first set to proper text format, meaning that it will be a string with the first letter capitalized. It then goes through a for statement where for each item in the variable “a” array, the find function will check if that number is in variable “y”. If there is a number, variable “y” becomes lowercase. This is because if there is a number, the ordinals will need to be lowercase (21St → 21st). Variable “y” then is tested for all of the items in variable “b” because if there is a two-directional abbreviation, both letters will need to be capitalized, which would not be the case using the proper function. This test is only in the first block of code because directional abbreviations will only be in the first segment of a street name.

The next six blocks contain the following variables: “z”, “q”, “w”, “e”, “t”, and “u”. These blocks function the same as the variable “y” block and properly format each segment of the road name, but provide lowercase ordinals in the event of a number. Each of these variables is responsible for a specific item in the variable “x” array. This is evident by the if (count(x) > NUMBER and proper(text(x[2]). For example, if the road name is 21st St., only variables “y” and “z” will be used because there are only two items in the road name. But if the road name was SW De La Salle Blvd, variables “y”, “z”, “q”, “w”, and “e” would be used because there are five items in the road name.

The final block of code concatenates each properly formatted segment of the road name back into one singular, unified string value, contained by variable “r”. This is dependent on the number of segments and ensures that there will be no extra spaces after the name.
