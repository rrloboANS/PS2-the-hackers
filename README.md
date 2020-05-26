# Problem Set 2

## Group project
This is a group project.
You should work in groups of 2 to 4 (not alone and not more than 4). If this is a problem, please let me know ahead of time.

### Please enter the names of the group members here:
1. Mireya Smith
1. Richard Lobo
1. Norman Andino
All of us worked together to figure out how to create the commands and solve the questions.

## Due date
**It is my hope that is can be turned in on Friday, May 22nd**, but I will take it until May 26th at the latest.

## The dataset
I have provided a dataset that you will use for this. The dataset and it's description are on the cluster as well as in github.
 * The dataset is at: `/ufrc/bsc4452/share/Class_Files/data/flights.May2017-Apr2018.csv`
 * The metadata (description of the data) is at: `/ufrc/bsc4452/share/Class_Files/data/flights_metadata.md`
     * It is also [nicely rendered on github](https://github.com/CompTools/Class_Files/blob/master/data/flights_metadata.md).

## Instructions

The goal of this project is to write a Bash script that does the following:
1. Counts the number of flights that were delayed more than 15 minutes into or out of Gainesville, FL (airport code GNV) during the timeframe covered by the dataset. (*2 points*)
##
    grep GNV /ufrc/bsc4452/share/Class_Files/data/flights.May2017-Apr2018.csv >> ./GNV.flights
    grep -E '\s\w\w\"\,\"\w{2}\",\"[[:digit:]]*\",[[:digit:]]*\.[[:digit:]]*,1' GNV.flights | wc -l
Result: 803 delayed flights

2. Produce a table (text is fine) with the data to fill in this table (*13 points*):


GNV to: | Total flights | Total flights delayed (>15min) | Total flights delayed due to Weather
--------|---------------|------------------------|-------------------------------
ATL |1476|262|15
CLT |476|107|3
MIA |205|30|0

## 
    #GNV to ATL
    #Total
    grep -E 'GNV\"\,\"Gainesville, FL\"\,\"FL\"\,\"ATL' GNV.flights >> GNVtoATL 
    wc –l GNVtoATL
    #1476 flight
    #Delayed 15 min
    grep -E 'GNV\"\,\"Gainesville, FL\"\,\"FL\"\,\"ATL\"\,\"Atlanta\, GA\"\,\"GA\"\,\"[[:digit:]]*\",[[:digit:]]*\.[[:digit:]]*\,1'         GNV.flights | wc –l
    #262 flight
    #Delayed by wether
    awk -F, '{print $24}' GNVtoATL | sort
    #15 flights

## 
    #GNV to CLT
    #Total
    grep -E 'GNV\"\,\"Gainesville, FL\"\,\"FL\"\,\"CLT' GNV.flights >> GNVtoCLT 
    wc –l GNVtoCLT
    #476 flight
    #Delayed 15 min
    grep -E 'GNV\"\,\"Gainesville, FL\"\,\"FL\"\,\"CLT\"\,\"Charlotte\, NC\"\,\"NC\"\,\"[[:digit:]]*\",[[:digit:]]*\.[[:digit:]]*\,1' GNV.flights | wc –l
    #107 flight
    #Delayed by wether
    awk -F, '{print $24}' GNVtoATL | sort
    3 flights

## 
    #GNV to MIA
    #Total
    grep -E 'GNV\"\,\"Gainesville, FL\"\,\"FL\"\,\"MIA' GNV.flights >> GNVtoMIA 
    wc –l GNVtoMIA
    #205 flight
    #Delayed 15 min
    grep -E 'GNV\"\,\"Gainesville, FL\"\,\"FL\"\,\"MIA\"\,\"Miami\, FL\"\,\"FL\"\,\"[[:digit:]]*\",[[:digit:]]*\.[[:digit:]]*\,1' GNV.flights | wc –l
    #30 flight
    #Delayed by wether
    awk -F, '{print $24}' GNVtoATL | sort
    #0 flights

3. Within a function, print a list of all unique airport codes contained in the dataset. (*3 points*)
##
    awk -F',' '{print $7}' /ufrc/bsc4452/share/Class_Files/data/flights.May2017-Apr2018.csv >> ./test1/airport.code2
    sort test1/airport.code2 | uniq >> uniq.airport.code2
    wc -l uniq.airport.code2
    grep -v '\"DEST_CITY_NAME\"' test1/uniq.airport.code | wc -l
Total of 350 airports

4. Within a function list the cities in Florida that have airports in the dataset. (*2 points*)
##
    awk -F',' '{print $3,$4,$5}' /ufrc/bsc4452/share/Class_Files/data/flights.May2017-Apr2018.csv >> test1/question4
    grep 'FL\"$' test1/question4 | sort | uniq | wc –l
20 cities
"DAB" "Daytona Beach  FL"
"ECP" "Panama City  FL"
"EYW" "Key West  FL"
"FLL" "Fort Lauderdale  FL"
"GNV" "Gainesville  FL"
"JAX" "Jacksonville  FL"
"MCO" "Orlando  FL"
"MIA" "Miami  FL"
"MLB" "Melbourne  FL"
"PBI" "West Palm Beach/Palm Beach  FL"
"PGD" "Punta Gorda  FL"
"PIE" "St. Petersburg  FL"
"PNS" "Pensacola  FL"
"RSW" "Fort Myers  FL"
"SFB" "Sanford  FL"
"SRQ" "Sarasota/Bradenton  FL"
"TLH" "Tallahassee  FL"
"TPA" "Tampa  FL"

**Bonus question:**  Asks for user input (see chapter 28) to enter either a airport code or city, state name and then calculates the number of flights as in question 1. (*5 points extra credit*)

## To submit
You should submit your answer as one or more scripts in a git repository. Submit the link in Canvas.

You should start in Canvas, creating your group and then create the same group in github.

**Be sure to edit this README.md file with the names of the group members.**

## Grading
For questions, 1, 3 and 4, I will mostly be looking for the right answer.

**Your score on 1,3,4 (I'll fill this in when I grade):**


For question 2, you will receive points for:

Rubric item | Points | Your score
------------|--------|-----------
Using github| 1 point |  ** **
Having at least one commit from each member of the team | 2 points | ** **
Using meaningful commit messages | 2 points | ** **
Using functions correctly | 2 points | ** **
Using comments in code | 2 points | ** **
Using spacing to make code readable | 2 points |** **
Getting the correct answer | 2 points | ** **

**Extra credit:**


**Total points:**
 /20
