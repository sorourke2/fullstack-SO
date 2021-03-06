# Fullstack Technical Assessment


Implemented as a command line program, the program allows the user to input criteria to find the "best-matched restaurants". The "Function" can be tested against using the command line by passing in arguments, therefore most argument validation occurs at the point of reading argument input (In regards to requirement #2 "If parameter values are invalid, return an error message.")

Data is returned from the main() function run in index.py as well as displayed on the command line in a table format for easy readability.

## How to Run

1. cd into /src
2. run `python index.py ...` to start the program
3. Available arguments for the function can be found by running `python index.py -h`.
4. `python -m unittest tests.test_name` to run specific unit_tests all of which can be found in `src/tests`
 
 
 Here are some fun commands to try:
 - `python index.py -p 10 --customer-rating 4`
 - `python index.py -n grill`
 - `python index.py -n grill -c korean`
 - `python index.py -n grill -c korean -p 15`
 - `python index.py -d 12 --customer-rating 5 -n delic`
 - `python index.py`
 - `python index.py -f boston_restaurants.csv -d 6`

## Assumptions Made
When looking at the criteria:
#### Restaurant Name
Partial name matching on the restaurant name only searches for prefixes/the full name. The search is case-insensitive. If a restaurant name is more than one word, the matching will check every word for prefixes. For example, if we are searching for "Gri", the two restaurants "Grill House" and "Steak Grill" will be included in the result. I believe this is better than just searching the first word for the prefix and better than looking for if the word is include ANYWHERE in the word (for example: searching "eak" and getting "Steak Grill").

#### Customer Rating(1 star ~ 5 stars)
This will be an integer with a set range of 1-5

#### Distance(1 mile ~ 10 miles)
This will be a positive float. As there can be restaurants that are 1.5 miles away. There is no upper limit to the value to allow more flexibility.

#### Price(how much one person will spend on average, $10 ~ $50)
This will be a positive float. As there can be averages of $11.5. There is no upper limit to the value to allow more flexibility.

#### Cuisine(Chinese, American, Thai, etc.).
Exactly the same as Restaurant name, since cuisines.csv does not include every cuisine in the world, the search must have flexibility.

#### Uniqueness
I went with the assumption that all Restaurants are unique. As in when we are filtering the CSV, if all the data is the same between two restaurants, only one restaurant is considered. Therefore the output cannot contain two exact same restaurants.

## Specifiying your own data
Users can search through their own data by creating a csv in src/csv to parse and filter. The CSV must follow the same format as the given CSVs. Users can then specify the CSV to use by using the command line args. If no CSV is specified on the command line, the given CSVs are used. If a CSV has invalid format, an error is thrown.

## Display Table Size
Went with the assumption that there would not be a restaurant name or other data points large enough to mess with the formatting of the table. Determing the max string length of each of the data fields to dynamically expand column width seemed overkill.

## Specifications Pattern
I included the ability to filter the recipes by chaining the criteria into more complex booleans by implementing the OrSpecification class and NotSpecification class. Although this ability is not functionally present in the program, I left it in to show that the pattern can be used in the future for more complex querying.
(This pattern/implementation heavily inspired by http://sd.blackball.lv/library/Domain-Driven_Design_-_Tackling_Complexity_in_the_Heart_of_Software.pdf p.246, altered to fit into the context of this program)

#
Let me know if there are any questions! Would love to talk about my thought process while completing this program.
