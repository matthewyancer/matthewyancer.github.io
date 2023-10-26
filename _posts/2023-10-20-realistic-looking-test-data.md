## Realistic-Looking Test Data

There are often times when programmers need to produce test data for a system under development. They may generate some strings of random characters. Or they may pull in some text from a [lorem](https://loremipsum.io/) [ipsum](https://www.lipsum.com/) [generator](https://pirateipsum.me/). Both of these options are undesirable in that they do not look real. Non-developer testers of the system may look at a user interface populated with random characters or gibberish and feel that something is broken. This post explores using random number generators and data look-up tables to produce realistic-looking test data.

### Background

When playing a tabletop, pen-and-paper role-playing game, such as Dungeons & Dragons, sometimes a game master needs help coming up with ideas for the world they are creating and describing to the other players. A common practice is to use tables of data covering various topics that can be randomly selected from using a [set of dice](https://www.amazon.com/Polyhedral-7-Die-Opaque-Chessex-Dice/dp/B0011607GO/). For example, if you need to figure out what is hidden inside a treasure chest, you could consult [a treasures table](https://koboldpress.com/dungeon-tables-trinkets-and-treasures/). Or if you need to come up with the name for a character, you could consult [a character name table](https://koboldpress.com/the-random-dm-npc-names/). There are [all sorts of tables](https://www.reddit.com/r/BehindTheTables/wiki/index/) covering a tremendous number of topic areas that can be used in this way. There are even [role-playing games](http://www.onesevendesign.com/laserfeelings/) that create the majority of their play scenarios using this type of approach. Now, on to the dice used to make these tables work.

The types of dice used for role-playing games are special. Yes, you can use traditional six-sided dice that you may be used to from a game such as Monopoly or Yahtzee. But there are many other shapes and types of dice, known as polyhedral dice, that are useful in role-playing games. Here are some common polyhedral dice types used:

| Name | Description | Link to Roll |
|---|---|---|
| d4 | A four-sided die which gives results from 1 to 4. | [Roll!](https://rolladie.net/roll-a-d4-die) |
| d6 | A traditional six-sided die which gives results from 1 to 6. | [Roll!](https://rolladie.net/) |
| d8 | An eight-sided die which gives results from 1 to 8. | [Roll!](https://rolladie.net/roll-a-d8-die) |
| d10 | A ten-sided die which gives results from 1 to 10. The numbering can also be from 0 to 9. In that case, the 0 is treated as the 10. | [Roll!](https://rolladie.net/roll-a-d10-die) |
| d12 | A twelve-sided die which gives results from 1 to 12. | [Roll!](https://rolladie.net/roll-a-d12-die) |
| d20 | A twenty-sided die which gives results from 1 to 20. | [Roll!](https://rolladie.net/roll-a-d20-die) |
| d100 | A 100-sided die (or two d10s can also be used) which gives results from 1 to 100. | [Roll!](https://rolladie.net/roll-a-d100-die) |

*(Table #1: Types of Dice)*

Equipped with this information, let's look at some real-world scenarios.

### Generating Names

Let's say you need to create a list of real-looking names. Using this handy [list of first names from the Social Security Administration](https://www.ssa.gov/oact/babynames/decades/names1990s.html), you could create a table of 100 first names (first fifty are male, second fifty are female) like this:

| First<br />Name<br />—roll [d100](https://rolladie.net/roll-a-d100-die) | <!-- --> | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|---|
| 1. Michael | 2. Christopher | 3. Matthew | 4. Joshua | 5. Jacob |
| 6. Nicholas | 7. Andrew | 8. Daniel | 9. Tyler | 10. Joseph |
| 11. Brandon | 12. David | 13. James | 14. Ryan | 15. John |
| 16. Zachary | 17. Justin | 18. William | 19. Anthony | 20. Robert |
| 21. Jonathan | 22. Austin | 23. Alexander | 24. Kyle | 25. Kevin |
| 26. Thomas | 27. Cody | 28. Jordan | 29. Eric | 30. Benjamin |
| 31. Aaron | 32. Christian | 33. Samuel | 34. Dylan | 35. Steven |
| 36. Brian | 37. Jose | 38. Timothy | 39. Nathan | 40. Adam |
| 41. Richard | 42. Patrick | 43. Charles | 44. Sean | 45. Jason |
| 46. Cameron | 47. Jeremy | 48. Mark | 49. Stephen | 50. Jesse |
| 51. Jessica | 52. Ashley | 53. Emily | 54. Sarah | 55. Samantha |
| 56. Amanda | 57. Brittany | 58. Elizabeth | 59. Taylor | 60. Megan |
| 61. Hannah | 62. Kayla | 63. Lauren | 64. Stephanie | 65. Rachel |
| 66. Jennifer | 67. Nicole | 68. Alexis | 69. Victoria | 70. Amber |
| 71. Alyssa | 72. Courtney | 73. Rebecca | 74. Danielle | 75. Jasmine |
| 76. Brianna | 77. Katherine | 78. Alexandra | 79. Madison | 80. Morgan |
| 81. Melissa | 82. Michelle | 83. Kelsey | 84. Chelsea | 85. Anna |
| 86. Kimberly | 87. Tiffany | 88. Olivia | 89. Mary | 90. Christina |
| 91. Allison | 92. Abigail | 93. Sara | 94. Shelby | 95. Heather |
| 96. Haley | 97. Maria | 98. Kaitlyn | 99. Laura | 100. Erin |

*(Table #2: First Names)*

And then, using this [list of most common last names from ThoughtCo](https://www.thoughtco.com/most-common-us-surnames-1422656), you could create a table of 100 last names like this:

| Last<br />Name<br />—roll [d100](https://rolladie.net/roll-a-d100-die) | <!-- --> | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|---|
| 1. Smith | 2. Johnson | 3. Williams | 4. Brown | 5. Jones |
| 6. Garcia | 7. Miller | 8. Davis | 9. Rodriguez | 10. Martinez |
| 11. Hernandez | 12. Lopez | 13. Gonzales | 14. Wilson | 15. Anderson |
| 16. Thomas | 17. Taylor | 18. Moore | 19. Jackson | 20. Martin |
| 21. Lee | 22. Perez | 23. Thompson | 24. White | 25. Harris |
| 26. Sanchez | 27. Clark | 28. Ramirez | 29. Lewis | 30. Robinson |
| 31. Walker | 32. Young | 33. Allen | 34. King | 35. Wright |
| 36. Scott | 37. Torres | 38. Nguyen | 39. Hill | 40. Flores |
| 41. Green | 42. Adams | 43. Nelson | 44. Baker | 45. Hall |
| 46. Rivera | 47. Campbell | 48. Mitchell | 49. Carter | 50. Roberts |
| 51. Gomez | 52. Phillips | 53. Evans | 54. Turner | 55. Diaz |
| 56. Parker | 57. Cruz | 58. Edwards | 59. Collins | 60. Reyes |
| 61. Stewart | 62. Morris | 63. Morales | 64. Murphy | 65. Cook |
| 66. Rogers | 67. Gutierrez | 68. Ortiz | 69. Morgan | 70. Cooper |
| 71. Peterson | 72. Bailey | 73. Reed | 74. Kelly | 75. Howard |
| 76. Ramos | 77. Kim | 78. Cox | 79. Ward | 80. Richardson |
| 81. Watson | 82. Brooks | 83. Chavez | 84. Wood | 85. James |
| 86. Bennet | 87. Gray | 88. Mendoza | 89. Ruiz | 90. Hughes |
| 91. Price | 92. Alvarez | 93. Castillo | 94. Sanders | 95. Patel |
| 96. Myers | 97. Long | 98. Ross | 99. Foster | 100. Jimenez |

*(Table #3: Last Names)*

To use these tables, you would role a d100 three times. The first number gives you a first name from table #2, the second number gives you a middle initial from table #2 (just use the first letter of the name), and the third number gives you a last name from table #3. Let's try that. (If you don't have a d100, use the Roll [link](https://rolladie.net/roll-a-d100-die) above in Table #1.)

- Roll #1 (d100) for first name (Table #2): 57
- Roll #2 (d100) for middle initial (Table #2): 2
- Roll #3 (d100) for last name (Table #3): 84

Ok, let's map those numbers to the tables. "57" in table #2 gives: "Brittany". "2" in table #2 gives: "C.". And "84" in table #3 gives: "Wood". For a full name of: "Brittany C. Wood". Let's try another.

- Roll #1 (d100) for first name (Table #2): 29
- Roll #2 (d100) for middle initial (Table #2): 83
- Roll #3 (d100) for last name (Table #3): 48

"29" in table #2 gives: "Eric". "83" in table #2 gives: "K.". And "48" in table #3 gives: "Mitchell". "Eric K. Mitchell".

Here are another five names using this approach:

| Roll #1 | Roll #2 | Roll #3 | Resulting Name |
|---|---|---|---|
| 22 | 26 | 57 | Austin T. Cruz |
| 64 | 92 | 46 | Stephanie A. Rivera |
| 25 | 74 | 68 | Kevin D. Ortiz |
| 53 | 99 | 78 | Emily L. Cox |
| 33 | 21 | 14 | Samuel J. Wilson |

*(Table #4: Generated Names)*

Now, let's try something more advanced.

### Generating Addresses

Let's say you need to create a list of real-looking, but fake, street addresses. There are several parts that will need to be generated here. There's a house or building number, a street name (which has several parts), there may be an apartment number, and finally a city, state, and zipcode. Let's look at the tables that will help with this:

*NOTE: Keep in mind that these are fictitious locations.*

**House or Building Number:**  
For the house number or building number, we'll just directly use die rolls for that. We'll roll a d20 and a d100 and concatenate the results. So, if you roll a "12" on the d20, and a "42" on the d100, the resulting house number will be "1242".

**Street Name:**  
Wikipedia has a helpful description of what components make up a [street name](https://en.wikipedia.org/wiki/Street_name):

> Names are often given in a two-part form: an individual name known as the specific, and an indicator of the type of street, known as the generic. Examples are "Main Road", "Fleet Street" and "Park Avenue".
>  
> A street name can also include a direction (the cardinal points east, west, north, south, or the quadrants NW, NE, SW, SE), especially in cities with a grid-numbering system. Examples include "E Roosevelt Boulevard" and "14th Street NW".
>  
> In the United States, most streets are named after numbers, landscapes, trees (a combination of trees and landscapes such as "Oakhill" is used often in residential areas), or the surname of an important individual (in some instances, it is just a commonly held surname such as Smith).

Based on the above, we'll use the following tables to create a street name:

| Include<br />Direction?<br />—roll [d4](https://rolladie.net/roll-a-d4-die) | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|
| 1. None | 2. None | 3. Prefix | 4. Suffix |

*(Table #5: Street Name: Include Direction in Street Name?)*

| Direction<br />—roll [d8](https://rolladie.net/roll-a-d8-die) | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|
| 1. N | 2. NE | 3. E | 4. SE |
| 5. S | 6. SW | 7. W | 8. NW |

*(Table #6: Street Name: Direction)*

| Specific<br />Name<br />Type<br />—roll [d6](https://rolladie.net/) | <!-- --> | <!-- --> | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|---|---|
| 1. Cardinal<br />Directions | 2. Landmarks | 3. Landscapes | 4. Numbers | 5. Presidents | 6. Trees |

*(Table #7: Street Name: Identify Specific Name Type)*

Once you identify the type of specific name, use the below table to pick the actual specific name:

| Cardinal<br />Directions<br />—roll [d4](https://rolladie.net/roll-a-d4-die) | Landmarks<br />—roll [d6](https://rolladie.net/) | Landscapes<br />—roll [d12](https://rolladie.net/roll-a-d12-die) | Numbers<br />—roll [d12](https://rolladie.net/roll-a-d12-die) | Presidents<br />—roll [d8](https://rolladie.net/roll-a-d8-die) | Trees<br />—roll [d12](https://rolladie.net/roll-a-d12-die) |
|---|---|---|---|---|---|
| 1. North | 1. Broad | 1. Creek | 1. 1st | 1. Adams | 1. Cedar |
| 2. East | 2. Center | 2. Forest | 2. 2nd | 2. Jackson | 2. Cherry |
| 3. South | 3. Church | 3. Highland | 3. 3rd | 3. Jefferson | 3. Chestnut |
| 4. West | 4. High | 4. Hill | 4. 4th | 4. Johnson | 4. Dogwood |
|  | 5. Main | 5. Lake | 5. 5th | 5. Lincoln | 5. Elm |
|  | 6. Market | 6. Lakeview | 6. 6th | 6. Madison | 6. Hickory |
|  |  | 7. Meadow | 7. 7th | 7. Washington | 7. Maple |
|  |  | 8. Orchard | 8. 8th | 8. Wilson | 8. Oak |
|  |  | 9. Park | 9. 9th |  | 9. Pine |
|  |  | 10. Ridge | 10. 10th |  | 10. Spruce |
|  |  | 11. River | 11. 11th |  | 11. Walnut |
|  |  | 12. Sunset | 12. 12th |  | 12. Willow |

*(Table #8: Street Name: Select Actual Specific Name)*

| Generic<br />Name<br />—roll [d12](https://rolladie.net/roll-a-d12-die) | <!-- --> | <!-- --> | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|---|---|
| 1. Ave | 2. Blvd | 3. Cir | 4. Ct | 5. Dr | 6. Ln |
| 7. Pkwy | 8. Pl | 9. Rd | 10. St | 11. Ter | 12. Way |

*(Table #9: Street Name: Generic Name)*

Let's look at an example street name using these tables:

- Roll #1 (d4) for Including Direction (Table #5): 3
- Roll #2 (d8) for Direction (Table #6): 6
- Roll #3 (d6) for Type of Specific Name (Table #7): 5
- Roll #4 (d8) for Specific Name (Table #8): 1
- Roll #5 (d12) for Generic Name (Table #9): 9

Which gives: "SW Adams Rd".

And another example street name:

- Roll #1 (d4) for Including Direction (Table #5): 2
- Roll #2 (d8) for Direction (Table #6): 0 (skipping)
- Roll #3 (d6) for Type of Specific Name (Table #7): 6
- Roll #4 (d12) for Specific Name (Table #8): 3
- Roll #5 (d12) for Generic Name (Table #9): 5

Which gives: "Chestnut Dr".

**Apartment Number:**  
Roughly [1 in 8 people](https://www.naahq.org/united-states-needs-46-million-new-apartments-2030-or-it-will-face-serious-shortage-0#:~:text=States%20%E2%80%94%20that%20is-,almost%201%20in%208,-%E2%80%94%20call%20apartments%20home) in the US live in apartments. We'll use this ratio to decide if our address should include an apartment number.

| Add<br />Apartment<br />Number?<br />—roll [d8](https://rolladie.net/roll-a-d8-die) | <!-- --> | <!-- --> | <!-- --> |
|---|---|---|---|
| 1. No | 2. No | 3. No | 4. No |
| 5. No | 6. No | 7. No | 8. Yes |

*(Table #10: Add Apartment Number?)*

If we roll an "8" on a d8, then we'll use a direct dice roll for the apartment number itself. A d100 will work here. So a roll of "72" would be "Apt 72" for address line 2.

**City, State, Zip:**  
In the next three tables, you'll need an unusual dice type, a d50, or 50-sided die. While such a die does [exist](https://www.amazon.com/Bescon-Fifty-Sided-Sided-50-Sided-Gaming/dp/B06XFGGTCB/), most people wouldn't have one. They would either use a d100 and cut the result in half, or they would roll a d50 online, which you can do [here](https://rolladie.net/roll-a-d50-die).

For the city, we'll use the following table of common [city](https://en.wikipedia.org/wiki/List_of_the_most_common_U.S._place_names) [names](https://geotargit.com/citiespercountry.php?qcountry_code=US&qcity=Riverside):

| City<br />—roll [d50](https://rolladie.net/roll-a-d50-die) | <!-- --> | <!-- --> | <!-- --> | <!-- -->|
|---|---|---|---|---|
| 1. Arlington | 2. Ashland | 3. Auburn | 4. Bethel | 5. Bloomington |
| 6. Bristol | 7. Brookview | 8. Burlington | 9. Centerville | 10. Chester |
| 11. Clayton | 12. Cleveland | 13. Clifton | 14. Clinton | 15. Dayton |
| 16. Dover | 17. Eden | 18. Fairview | 19. Farmington | 20. Florence |
| 21. Franklin | 22. Georgetown | 23. Glendale | 24. Greenville | 25. Greenwood |
| 26. Hamilton | 27. Hudson | 28. Jackson | 29. Kingston | 30. Lebanon |
| 31. Lexington | 32. Liberty | 33. Lincoln | 34. Madison | 35. Manchester |
| 36. Marion | 37. Midway | 38. Milford | 39. Milton | 40. Mount Vernon |
| 41. Newport | 42. Oakland | 43. Oxford | 44. Pleasant Valley | 45. Riverside |
| 46. Salem | 47. Springfield | 48. Union | 49. Washington | 50. Winchester |

*(Table #11: City)*

For the [state](https://www.50states.com/abbreviations.htm), we'll use the following table (leaving out territories for this example):

| State<br />—roll [d50](https://rolladie.net/roll-a-d50-die) | <!-- --> | <!-- --> | <!-- --> | <!-- -->|
|---|---|---|---|---|
| 1. AL | 2. AK | 3. AZ | 4. AR | 5. CA |
| 6. CO | 7. CT | 8. DE | 9. FL | 10. GA |
| 11. HI | 12. ID | 13. IL | 14. IN | 15. IA |
| 16. KS | 17. KY | 18. LA | 19. ME | 20. MD |
| 21. MA | 22. MI | 23. MN | 24. MS | 25. MO |
| 26. MT | 27. NE | 28. NV | 29. NH | 30. NJ |
| 31. NM | 32. NY | 33. NC | 34. ND | 35. OH |
| 36. OK | 37. OR | 38. PA | 39. RI | 40. SC |
| 41. SD | 42. TN | 43. TX | 44. UT | 45. VT |
| 46. VA | 47. WA | 48. WV | 49. WI | 50. WY |

*(Table #12: State)*

And for zipcode, we'll pull the [first 3 digits](https://en.wikipedia.org/wiki/List_of_ZIP_Code_prefixes) of the zipcode from the following table using the same die roll as was used for the state. Then we'll get the last 2 digits from another die roll (d100 to the rescue again) directly and pad with zero if necessary.

|Zipcode<br />Prefix<br />—roll [d50](https://rolladie.net/roll-a-d50-die) | <!-- --> | <!-- --> | <!-- --> | <!-- -->|
|---|---|---|---|---|
| 1. 361 | 2. 998 | 3. 850 | 4. 722 | 5. 958 |
| 6. 802 | 7. 061 | 8. 199 | 9. 323 | 10. 303 |
| 11. 968 | 12. 837 | 13. 627 | 14. 462 | 15. 503 |
| 16. 666 | 17. 406 | 18. 708 | 19. 043 | 20. 214 |
| 21. 022 | 22. 489 | 23. 551 | 24. 830 | 25. 651 |
| 26. 596 | 27. 685 | 28. 897 | 29. 033 | 30. 086 |
| 31. 875 | 32. 122 | 33. 276 | 34. 585 | 35. 319 |
| 36. 731 | 37. 973 | 38. 171 | 39. 029 | 40. 292 |
| 41. 575 | 42. 372 | 43. 787 | 44. 841 | 45. 056 |
| 46. 232 | 47. 985 | 48. 253 | 49. 537 | 50. 820 |

*(Table #13: Zipcode Prefixes)*

Let's look at an example city, state, zipcode using these tables:

- Roll #1 (d50) for City (Table #11): 33
- Roll #2 (d50) for State (Table #12): 29
- Reuse Roll #2 (d50) for Zipcode Prefix (Table #13): 29
- Roll #3 (d100) for remaining Zipcode digits: 7

Which gives: "Lincoln, NH 03307".

And another example city, state, zipcode:

- Roll #1 (d50) for City (Table #11): 42
- Roll #2 (d50) for State (Table #12): 1
- Reuse Roll #2 (d50) for Zipcode Prefix (Table #13): 1
- Roll #3 (d100) for remaining Zipcode digits: 39

Which gives: "Oakland, AL 36139".

**Adding it all together:**  
Here are five full addresses using this approach:

| House # | Street Name | Apt # | City, State, Zip | Generated Address |
|---|---|---|---|---|
| 7, 41 | 1, 0, 2, 3, 11 | 3, 0 | 4, 32, 32, 36 | 741 Church Ter<br />Bethel, NY 12236 |
| 18, 89 | 3, 5, 6, 7, 9 | 6, 0 | 47, 2, 2, 54 | 1889 S Maple Rd<br />Springfield, AK 99854 |
| 11, 16 | 4, 3, 3, 5, 8 | 8, 26 | 19, 27, 27, 90 | 1116 Lake Pl E<br />Apt 26<br />Farmington, NE 68590 |
| 4, 13 | 2, 0, 5, 7, 2 | 8, 51 | 30, 13, 13, 05 | 413 Washington Blvd<br />Apt 51<br />Lebanon, IL 62705 |
| 5, 97 | 1, 0, 4, 3, 4 | 2, 0 | 44, 48, 48, 34 | 597 3rd Ct<br />Pleasant Valley, WV 25334 |

*(Table #14: Generated Addresses)*

### Automating

Now, what if you needed to generate thousands or millions of these data points? Manually rolling dice won't be convenient or practical. Some automation of the process will be needed. Luckily, computers do a pretty good job at producing random numbers and looking up data. Here's what that process might look like:

1. Write a script that produces a list of random numbers. For example, to produce a list of people's names using tables 2 and 3, you would need three numbers between 1 and 100 for each name. Generate as many as are required for your purposes in a loop.

2. Export the list of random numbers created in step 1.

3. Load the needed lookup tables into a database, with a column holding the number you're rolling for as the identifier of the row and another column holding the descriptive text.

4. Import the list of random numbers from step 2 into your database.

5. Write a query that joins the generated numbers with your lookup tables.

Keep in mind that you can extend or change your data tables however you see fit for your purposes. You can also come up with new data tables for scenarios we haven't covered. And your random number generator can use values from any desired range; you're not limited to just the values of physical dice. Just make sure that the range of the random number generated matches the number of records in your lookup table.

Enjoy!
