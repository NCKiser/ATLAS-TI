An World Atlas for your TI-84 Plus CE! (and a stripped-down version for the CSE and monochrome 83+/84+)

NoahK, 2025

------------------------
##  For the CE version, ATLAS_complete.8xp (ATLAS, 53kB):

Starting at the world map, use the F keys to navigate to the desired continent and subregion, and use Clear to go back.
Then, use Arrow keys and Enter to select a country/territory in that subregion by their ISO 3166-1 alpha-2 country code.

The country data page contains the Country Name, Capital, Population, Region, and Country Code.
The country's flag is also loaded and drawn. This can take some time, so to skip or interrupt loading and drawing the flag, press Clear.
Press Enter or Clear to return from the country data page back to the continent map.

This Atlas contains data for 250 countries (sorry Wales, you're lumped in with the rest of GB).

Pressing Clear at the world map brings up a list of all 250 countries in alphabetical order by English name, but displayed by country code. Use Arrows and Enter to select a country from this complete list. (ex: Algeria shows up at the top of the list with the other 'A' countries, but has a country code of DZ).

Pressing Clear again exits the program, which cleanly restores all variables and window settings to their original values except for:
	GDB1
	L1
	L3
	Str8
	Str0

-------------------------
## For the stripped down version, ATLAS_light.8xp (ATLAStheta, 13kB):

A list of all 250 countries in alphabetical order by English name, but displayed by country code. Use Arrows and Enter to select a country from this complete list. (ex: Algeria shows up at the top of the list with the other 'A' countries, but has a country code of DZ).

The country data page contains the Country Name, Capital, Population, Region, and ISO 3166-1 alpha-2 Country Code.
Press Enter to go back to the list, or Clear to exit the program directly.

Uses Variables:
	C, D, G, P, R
	Str1, Str2, Str3, Str4, Str9

-------------------------
## Technical Info

Data is as of mid-2025. Country names, populations, and capitals may have changed since.
Sources:
	https://github.com/dr5hn/countries-states-cities-database/blob/master/csv/countries.csv
	https://flagpedia.net/download

Country Names, ISO codes, Regions, and Capitals are stored in plain text, all caps strings, and indexed using a list of character offsets.
Populations are stored in lists, indexed directly.

The stripped-down ATLAStheta contains all the same data, but not map or flags. If you don't need map or flag data, ATLAStheta is much faster to navigate and load.

Flag data was converted from PNGs, finding the closest of the TI-84 CE's 15 colors to each pixel in the flag.
Flags are 24px high, and a variable width. The colors are encoded is letters A-O, and then run-length encoded, and the entire string is prepended with the width of the flag. So a 36 pixel wide flag consisting of 3 Red, White, and Blue horizontal stripes would be: "36B288K288A288".

The remaining letters, P-Z, are used as keywords to further compress the flag data. Repeated sequences of characters are pulled out of the string, and replaced with one of these characters, and a dictionary of these sequences is added to the beginning of the string. In the previous example, "288" is repeated 3 times, so the dictionary entry would be "P288P", and the string "36BPKPAP", all together: "P288P36BPKPAP", which is a single character shorter than the original "36B288K288A288".

These savings get much more appreciable with flags that have vertical stripes, repeating patterns, or aliased diagonals. All this compression makes it possible to fit 250 flags that average ~850 pixels each (~212,500 pixels) in less than 34kB.