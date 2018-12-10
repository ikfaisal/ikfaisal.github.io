---
title:  "Practice Python Skills"
categories: generalassembly python
permalink: /:categories
---

![image tooltip here](http://imgur.com/1ZcRyrc.png){:height="36px" width="36px"}

---

# Project 1

### Building "Pokemon Stay"

---
You are an analyst at a "scrappy" online gaming company that specializes in remakes of last year's fads.

Your boss, who runs the product development team, is convinced that Pokemon Go's fatal flaw was that you had to actually move around outside. She has design mock-ups for a new game called Pokemon Stay: in this version players still need to move, but just from website to website. Pokemon gyms are now popular online destinations, and catching Pokemon in the "wild" simply requires browsing the internet for hours in the comfort of your home.

She wants you to program a prototype version of the game, and analyze the planned content to help the team calibrate the design.

#### Package imports

The pprint package below is the only package imported here, and it's not even strictly required to do any of the project. Printing python variables and objects with pprint can help to format them in a "prettier" way.


```python
from pprint import pprint
```

<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 1. Defining a player

---

The player variables are:

    player_id : id code unique to each player (integer)
    player_name : entered name of the player (string)
    time_played : number of time played the game in minutes (float)
    player_pokemon: the player's captured pokemon (dictionary)
    gyms_visited: ids of the gyms that a player has visited (list)

Create the components for a player object by defining each of these variables. The dictionary and list variables should just be defined as empty; you can use any (correctly typed) values for the others.

## Component of player object


```python
# Component of player object

player_id = 1
player_name = 'Bill'
time_played = float(120)
player_pokemon = {}
gyms_visited = []
```

<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 2. Defining "gym" locations

---

As the sole programmer, Pokemon Stay will have to start small. To begin, there will be 10 different gym location websites on the internet. The gym locations are:

    1. 'reddit.com'
    2. 'amazon.com'
    3. 'twitter.com'
    4. 'linkedin.com'
    5. 'ebay.com'
    6. 'netflix.com'
    7. 'amazon.com'
    8. 'stackoverflow.com'
    9. 'github.com'
    10. 'quora.com'

1. Set up a list of all the gym locations. This will be a list of strings.
2. Append two of these locations to your player's list of visited gyms.
3. Print the list.

# Gym Locations


```python
# List of gym locations

gym_locations = ['reddit.com', 'amazon.com', 'twitter.com', 'linkedin.com', 'ebay.com', 'netflix.com', 'amazon.com', 'stackoverflow.com', 'github.com', 'quora.com']
```


```python
# Visit reddit, netflix for player 1

gyms_visited.append('reddit.com')
gyms_visited.append('netflix.com')
```


```python
# Print list of gym

pprint(gym_locations)
```

    ['reddit.com',
     'amazon.com',
     'twitter.com',
     'linkedin.com',
     'ebay.com',
     'netflix.com',
     'amazon.com',
     'stackoverflow.com',
     'github.com',
     'quora.com']


<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 3. Create a pokedex

---

We also need to create some pokemon to catch. Each pokemon will be defined by these variables:

    pokemon_id : unique identifier for each pokemon (integer)
    name : the name of the pokemon (string)
    type : the category of pokemon (string)
    hp : base hitpoints (integer)
    attack : base attack (integer)
    defense : base defense (integer)
    special_attack : base special attack (integer)
    special_defense : base sepecial defense (integer)
    speed : base speed (integer)

We are only going to create 3 different pokemon with these `pokemon_id` and `pokemon_name` values:

    1 : 'charmander'
    2 : 'squirtle'
    3 : 'bulbasaur'

Create a dictionary that will contain the pokemon. The keys of the dictionary will be the `pokemon_id` and the values will themselves dictionaries that contain the other pokemon variables. The structure of the pokedex dictionary will start like so:

     {
         1: {
                 'name':'charmander',
                 'type':'fire',
                 ...

The `type` of charmander, squirtle, and bulbasaur should be `'fire'`, `'water'`, and `'poison'` respectively. The other values are up to you, make them anything you like!

Print (or pretty print) the pokedex dictionary with the 3 pokemon.

## Dictionary of Pokemon


```python
# Define pokedex dictionary and assign value

pokedex = {
    1: {
        'name': 'charmander',
        'type': 'fire',
        'hp': 10,
        'attack': 10,
        'defence': 10,
        'special_attack': 10,
        'special_defence': 10,
        'speed': 10
    },
    2: {
        'name': 'squirtle',
        'type': 'water',
        'hp': 20,
        'attack': 20,
        'defence': 20,
        'special_attack': 20,
        'special_defence': 20,
        'speed': 20
    },
    3: {
        'name': 'bulbasaur',
        'type': 'poison',
        'hp': 30,
        'attack': 30,
        'defence': 30,
        'special_attack': 30,
        'special_defence': 30,
        'speed': 30
    }
}
```


```python
# Print pokedex dictionary

pprint(pokedex)
```

    {1: {'attack': 10,
         'defence': 10,
         'hp': 10,
         'name': 'charmander',
         'special_attack': 10,
         'special_defence': 10,
         'speed': 10,
         'type': 'fire'},
     2: {'attack': 20,
         'defence': 20,
         'hp': 20,
         'name': 'squirtle',
         'special_attack': 20,
         'special_defence': 20,
         'speed': 20,
         'type': 'water'},
     3: {'attack': 30,
         'defence': 30,
         'hp': 30,
         'name': 'bulbasaur',
         'special_attack': 30,
         'special_defence': 30,
         'speed': 30,
         'type': 'poison'}}


<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 4. Create a data structure for players

---

### 4.1

In order to maintain a database of multiple players, create a dictionary that keeps track of players indexed by `player_id`.

The keys of the dictionary will be `player_id` and values will be dictionaries containing each player's variables (from question 1).

Construct the `players` dictionary and insert the player that you defined in question 1, then print `players`.


```python
# Create a dictionary to track player

playerdex1 = {
    'player_id': player_id,
    'player_name': player_name,
    'time_played': time_played,
    'player_pokemon': player_pokemon,
    'gyms_visited': gyms_visited
}

```


```python
# Create a dictionary to maintain multiple players
players = {}
```


```python
# Insert the first player

players[playerdex1['player_id']] = playerdex1
```


```python
# Print players

pprint(players)
```

    {1: {'gyms_visited': ['reddit.com', 'netflix.com'],
         'player_id': 1,
         'player_name': 'Bill',
         'player_pokemon': {},
         'time_played': 120.0}}


---

### 4.2

Create a new player with `player_id = 2` in the `players` dictionary. Leave the `'player_pokemon'` dictionary empty. Append `'alcatraz'` and `'pacific_beach'` to the `'gyms_visited'` list for player 2.

The `'player_name'` and `'time_played'` values are up to you, but must be a string and float, respectively.

Remember, the player_id is the key for the player in the players dictionary.

Print the `players` dictionary with the new player inserted.


```python
# Create a new player

playerdex2 = {
    'player_id': 2,
    'player_name': 'George',
    'time_played': float(90),
    'player_pokemon': {},
    'gyms_visited': []
}
```


```python
# Insert new player to players

players[playerdex2['player_id']] = playerdex2
```


```python
# Visit alcatraz, pacific_beach for player 2

players[playerdex2['player_id']]['gyms_visited'].append('alcatraz')
players[playerdex2['player_id']]['gyms_visited'].append('pacific_beach')
```


```python
# Print players dictionary with all players inserted

pprint(players)
```

    {1: {'gyms_visited': ['reddit.com', 'netflix.com'],
         'player_id': 1,
         'player_name': 'Bill',
         'player_pokemon': {},
         'time_played': 120.0},
     2: {'gyms_visited': ['alcatraz', 'pacific_beach'],
         'player_id': 2,
         'player_name': 'George',
         'player_pokemon': {},
         'time_played': 90.0}}


<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 5. Add captured pokemon for each player

---

The `'player_pokemon'` keyed dictionaries for each player keep track of which of the pokemon each player has.

The keys of the `'player_pokemon'` dictionaries are the pokemon ids that correspond to the ids in the `pokedex` dictionary you created earlier. The values are integers specifying the stats for the pokemon.

Give player 1 a squirtle. Give player 2 charmander and a bulbasaur.

Print the players dictionary after adding the pokemon for each player.



```python
# Dictionary to keep track of pokemons for each player

player_pokemon = {}
```


```python
# Key is the if of pokedex, values are integer value of stats for that pokemon
# Assign squirtle to player_pokemon which is 2

player_pokemon[2] = pokedex[2]
```


```python
# Assign pokemon to player 1

players[1]['player_pokemon'] = player_pokemon
```


```python
# Give player 2 charmander and a bulbasaur which is 1 and 3

player_pokemon = {}

player_pokemon[1] = pokedex[1]
player_pokemon[3] = pokedex[3]
```


```python
# Give player 2 charmander and a bulbasaur

players[2]['player_pokemon'] = player_pokemon
```


```python
# Print the players dictionary after adding the pokemon for each player.

pprint(players)
```

    {1: {'gyms_visited': ['reddit.com', 'netflix.com'],
         'player_id': 1,
         'player_name': 'Bill',
         'player_pokemon': {2: {'attack': 20,
                                'defence': 20,
                                'hp': 20,
                                'name': 'squirtle',
                                'special_attack': 20,
                                'special_defence': 20,
                                'speed': 20,
                                'type': 'water'}},
         'time_played': 120.0},
     2: {'gyms_visited': ['alcatraz', 'pacific_beach'],
         'player_id': 2,
         'player_name': 'George',
         'player_pokemon': {1: {'attack': 10,
                                'defence': 10,
                                'hp': 10,
                                'name': 'charmander',
                                'special_attack': 10,
                                'special_defence': 10,
                                'speed': 10,
                                'type': 'fire'},
                            3: {'attack': 30,
                                'defence': 30,
                                'hp': 30,
                                'name': 'bulbasaur',
                                'special_attack': 30,
                                'special_defence': 30,
                                'speed': 30,
                                'type': 'poison'}},
         'time_played': 90.0}}




## 6. What gyms have players visited?

---
<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">
### 6.1

Write a for-loop that:

1. Iterates through the `pokemon_gyms` list of gym locations you defined before.
2. For each gym, iterate through each player in the `players` dictionary with a second, internal for-loop.
3. If the player has visited the gym, print out "[player] has visited [gym location].", filling in [player] and [gym location] with the current player's name and current gym location.

## Find Gyms Players Have Visited

```python
for gym in gym_locations:
    for player in players:
        if gym in (players[player]['gyms_visited']):
            print(players[player]['player_name'], 'has visited ' + gym)
```

    Bill has visited reddit.com
    Bill has visited netflix.com


<img src="http://imgur.com/xDpSobf.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">
### 6.2

How many times did that loop run? If you have N gyms and also N players, how many times would it run as a function of N?

Can you think of a more efficient way to accomplish the same thing?

(You can write your answer as Markdown text.)


```python
# That loop run 20 times. If we have N gyms, N players it'll run N*N times.
# Another way to accomplish the same thing would be using list comprehension.
```


```python
[(players[player]['player_name'] + ' has visited ' + gym) for player in players for gym in gym_locations if gym in (players[player]['gyms_visited'])]
```
    ['Bill has visited reddit.com', 'Bill has visited netflix.com']

<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 7. Calculate player "power".

---

Define a function that will calculate a player's "power". Player power is defined as the sum of the base statistics all of their pokemon.

Your function will:

1. Accept the `players` dictionary, `pokedex` dictionary, and a player_id as arguments.
2. For the specified player_id, look up that player's pokemon and their level(s).
3. Find and aggregate the attack and defense values for each of the player's pokemon from the `pokedex` dictionary.
4. Print "[player name]'s power is [player power].", where the player power is the sum of the base statistics for all of their pokemon.
5. Return the player's power value.

Print out the pokemon power for each of your players.

## Calculate Power of Players


```python
def calculate_power(players, pokedex, player_id):
    """
    Calculate power of players

    Args:
        players (dictionary): players dictionary.
        pokedex (dictionary): pokedex dictionary.
        player_id (int): id of player.

    Returns:
        int: Return the player's power value which is the sum of the base statistics for all of their pokemon.
    """
    aggr_power = 0
    for key in players[player_id]['player_pokemon']:
        # Find and aggregate the attack and defense values for each of the player's pokemon from the pokedex dictionary.
        aggr_power += pokedex[key]['attack'] + pokedex[key]['defence'] + pokedex[key]['special_attack'] + pokedex[key]['special_defence']

    return aggr_power
```

```python
# Print out the pokemon power for each player

for player in players:
    aggr_power = calculate_power(players, pokedex, player)
    print(f"{players[player]['player_name']}'s power is {aggr_power}")
```

    Bill's power is 80
    George's power is 160


<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 8. Load a pokedex file containing all the pokemon

---

### 8.1

While you were putting together the prototype code, your colleagues were preparing a dataset of Pokemon and their attributes. (This was a rush job, so they may have picked some crazy values for some...)

The code below loads information from a comma separated value (csv) file. You need to parse this string into a more useable format. The format of the string is:

- Rows are separated by newline characters: \n
- Columns are separated by commas: ,
- All cells in the csv are double quoted. Ex: "PokedexNumber" is the first cell of the first row.


Using for-loops, create a list of lists where each list within the overall list is a row of the csv/matrix, and each element in that list is a cell in that row. Additional criteria:

1. Quotes are removed from each cell item.
2. Numeric column values are converted to floats.
3. There are some cells that are empty and have no information. For these cells put a -1 value in place.

Your end result is effectively a matrix. Each list in the outer list is a row, and the *j*th elements of list together form the *j*th column, which represents a data attribute. The first three lists in your pokedex list should look like this:

    ['PokedexNumber', 'Name', 'Type', 'Total', 'HP', 'Attack', 'Defense', 'SpecialAttack', 'SpecialDefense', 'Speed']
    [1.0, 'Bulbasaur', 'GrassPoison', 318.0, 45.0, 49.0, 49.0, 65.0, 65.0, 45.0]
    [2.0, 'Ivysaur', 'GrassPoison', 405.0, 60.0, 62.0, 63.0, 80.0, 80.0, 60.0]

## Load Pokedex File


```python
# Code to read in pokedex info
raw_pd = ''
pokedex_file = 'pokedex_basic.csv'
with open(pokedex_file, 'r') as f:
    raw_pd = f.read()

# the pokedex string is assigned to the raw_pd variable
```

## Clean Data


```python
import pandas as pd

def is_number(obj):
    """
    Check whether object is float or not

    Args:
        obj (str): string.

    Returns:
        bool: Try to convert the string to float. If successful, returns True. Otherwise False.
    """
    try:
        float(obj)
        return True
    except:
        return False

def replacechars(columnname):
    """
    Quotes are removed
    Numeric column values are converted to floats

    Args:
        columnname (str): string.

    Returns:
        str: Remove from string and convert numeric values to float
    """
    replacedcolumnname = ""
    special_chars = ['"']
    for c in columnname:
        if c not in special_chars:
            replacedcolumnname = replacedcolumnname + c

    if replacedcolumnname == '':
        replacedcolumnname = -1
    else:
        if is_number(replacedcolumnname):
            replacedcolumnname = float(replacedcolumnname)

    return replacedcolumnname
```


```python
list_pokedex_file = []
# Rows are separated by newline characters: \n
comma_str = raw_pd.split("\n")
for i in comma_str:
    cleanlist = []
    # Columns are separated by commas:
    dirtylist = i.split(',')
    for j in dirtylist:
        cleanlist.append(replacechars(j))
    list_pokedex_file.append(cleanlist)
```


```python
# Print first three lists

pprint(list_pokedex_file[0:3])
```

    [['PokedexNumber',
      'Name',
      'Type',
      'Total',
      'HP',
      'Attack',
      'Defense',
      'SpecialAttack',
      'SpecialDefense',
      'Speed'],
     [1.0, 'Bulbasaur', 'GrassPoison', 318.0, 45.0, 49.0, 49.0, 65.0, 65.0, 45.0],
     [2.0, 'Ivysaur', 'GrassPoison', 405.0, 60.0, 62.0, 63.0, 80.0, 80.0, 60.0]]


<img src="http://imgur.com/xDpSobf.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

### 8.2 Parse the raw pokedex with list comprehensions

---

Perform the same parsing as above, but **using only a single list comprehension** instead of for loops. You may have nested list comprehensions within the main list comprehension! The output should be exactly the same.

## List Comprehension


```python
# Not working. Need to do a nested comprehension.
list_of_lists_comp = []
comma_str = raw_pd.split("\n")
list_of_lists_comp = [replacechars(i).split(',') for i in comma_str]
```


```python
pprint(list_of_lists_comp[0:3])
```

    [['PokedexNumber',
      'Name',
      'Type',
      'Total',
      'HP',
      'Attack',
      'Defense',
      'SpecialAttack',
      'SpecialDefense',
      'Speed'],
     ['001', 'Bulbasaur', 'GrassPoison', '318', '45', '49', '49', '65', '65', '45'],
     ['002', 'Ivysaur', 'GrassPoison', '405', '60', '62', '63', '80', '80', '60']]


<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 9. Write a function to generate the full pokedex

---

Write a function that recreates the pokedex you made before, but with the data read in from the full pokemon file. The `PokedexNumber` should be used as the `pokemon_id` key values for the dictionary of pokemon.

Your function should:

1. Take the parsed pokedex information you created above as an argument.
2. Return a dictionary in the same format as your original pokedex you created before containing the information from the parsed full pokedex file.

To test the function, print out the pokemon with id = 100.


```python
# Print Original Pokedex to Refresh Memory

pprint(pokedex)
```

    {1: {'attack': 10,
         'defence': 10,
         'hp': 10,
         'name': 'charmander',
         'special_attack': 10,
         'special_defence': 10,
         'speed': 10,
         'type': 'fire'},
     2: {'attack': 20,
         'defence': 20,
         'hp': 20,
         'name': 'squirtle',
         'special_attack': 20,
         'special_defence': 20,
         'speed': 20,
         'type': 'water'},
     3: {'attack': 30,
         'defence': 30,
         'hp': 30,
         'name': 'bulbasaur',
         'special_attack': 30,
         'special_defence': 30,
         'speed': 30,
         'type': 'poison'}}



```python
def recreate_pokedex(parsed_pokedex):
    """
    Args:
        parsed_pokedex (list): list of pokemon.

    Returns:
        dict: Return a dictionary in the same format as original pokedex
    """

    # Get all haeders
    keys = parsed_pokedex[0]

    # Get all values
    values = parsed_pokedex[1:]    

    i = 1 # key of pokedex dictionary
    for v in values:
        # zip each row to corresponding header and convert them to dictionary
        dictionary = dict(zip(keys, v))
        pokedex[i] = dictionary
        i = i + 1

    return pokedex

pokedex_dict = recreate_pokedex(list_pokedex_file)
```


```python
pprint(pokedex_dict[100])
```

    {'Attack': 35.0,
     'Defense': 30.0,
     'HP': 30.0,
     'Name': 'Gastly',
     'PokedexNumber': 92.0,
     'SpecialAttack': 100.0,
     'SpecialDefense': 35.0,
     'Speed': 80.0,
     'Total': 310.0,
     'Type': 'GhostPoison'}


<img src="http://i.imgur.com/GCAf1UX.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 10. Write a function to generate a "filtered" pokedex
---
Your function should:
1. Take the parsed pokedex information you created above as an argument.
1. Take a dictionary as a parameter with keys matching the features of the Pokedex, filtering by exact match for string type values, and/or filter continuous variables specified value that is greater than or equal to the dictionary key parameter.
1. Return multiple elements from the Pokedex

Example:

```python

# Only filter based on parameters passed
filter_options = {
    'Attack':   25,
    'Defense':  30,
    'Type':     'Electric'
}

# Return records with attack >= 24, defense >= 30, and type == "Electric"
# Also anticipate that other paramters can also be passed such as "SpecialAttack", "Speed", etc.
filtered_pokedex(pokedex_data, filter=filter_options)

# Example output:
# [{'Attack': 30.0,
#  'Defense': 50.0,
#  'HP': 40.0,
#  'Name': 'Voltorb',
#  'SpecialAttack': 55.0,
#  'SpecialDefense': 55.0,
#  'Speed': 100.0,
#  'Total': 330.0,
#  'Type': 'Electric'},
#  {'Attack': 30.0,
#  'Defense': 33.0,
#  'HP': 32.0,
#  'Name': 'Pikachu',
#  'SpecialAttack': 55.0,
#  'SpecialDefense': 55.0,
#  'Speed': 100.0,
#  'Total': 330.0,
#  'Type': 'Electric'},
#  ... etc
#  ]

```



## Generate Filtered pokedex


```python
def filtered_pokedex(pokedex_data, filter_options):
    """
    Filter all filter options and return multiple elements from the pokedox

    Args:
        pokedex_data (dict): parsed pokedex information.
        filter_options (dict): dictionary as a parameter with keys matching the features of the Pokedex

    filtering by exact match for string type values, and/or filter continuous variables
    specified value that is greater than or equal to the dictionary key parameter

    Returns:
        list: Return multiple elements from the Pokedex
    """

    filtered_pokedex_list = []
    filter_keys = list(filter_options.keys()) # list of keys from filter

    for key, val in pokedex_data.items():
        isTrue = False
        for filter in filter_keys:
            # filtering by exact match for string type values
            if type(filter_options[filter]) is str:
                if (val[filter] == filter_options[filter]):
                    isTrue = True
                else:
                    isTrue = False
            # filter continuous variables specified value  
            # that is greater than or equal to the dictionary key parameter
            else:
                if (val[filter] >= filter_options[filter]):
                    isTrue = True
                else:
                    isTrue = False
        # if all conditions are true, append dictionary to list
        if (isTrue == True):
            filtered_pokedex_list.append(val)

    return filtered_pokedex_list    
```


```python
# Filter option to find matching pokemons
filter_options = {
    'Attack': 24,
    'Defense': 30,
    'Type': 'Electric'
}
filtered_pokedex_list = filtered_pokedex(pokedex_dict, filter_options)
```
## 9. Descriptive statistics on the prototype pokedex

<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">
### 9.1

What is the population mean and standard deviation of the "Total" attribute for all characters in the Pokedex?




```python
# Import numpy to calculate descriptive statistics

import numpy as np
```


```python
pokedex_total = [val['Total'] for key, val in pokedex_dict.items()]
```


```python
# Calculate mean
np_mean = np.mean(pokedex_total)
```


```python
# Calculate Standard Deviation
np_std = np.std(pokedex_total)
```


```python
print('Population Mean:', np_mean)
print('Standard Deviation:', np_std)
```

    Population Mean: 435.1275
    Standard Deviation: 119.96202000529168


<img src="http://imgur.com/l5NasQj.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">
### 9.2

The game is no fun if the characters are wildly unbalanced! Are any characters "overpowered", which we'll define as having a "Total" more than three standard deviations from the population mean?

## Find Overpowered Characters


```python
# "Total" more than three standard deviations from the population mean
overpowered = np_mean + 3 * np_std

filter_options = {
    'Total': overpowered
}
overpowered_characters = filtered_pokedex(pokedex_dict, filter_options)
```


```python
# Print overpowered characters
pprint(overpowered_characters)
```

    [{'Attack': 190.0,
      'Defense': 100.0,
      'HP': 126.0,
      'Name': 'MewtwoMega Mewtwo X',
      'PokedexNumber': 150.0,
      'SpecialAttack': 154.0,
      'SpecialDefense': 100.0,
      'Speed': 130.0,
      'Total': 800.0,
      'Type': 'PsychicFighting'}]


<img src="http://imgur.com/xDpSobf.png" style="float: left; margin: 25px 15px 0px 0px; height: 25px">

## 10. Calibrate the frequency of Pokemon

The design team wants you to make the powerful Pokemon rare, and the weaklings more common. How would you set the probability $p_i$ of finding Pokemon *i* each time a player visits a gym?

Write a function that takes in a Pokedex number and returns a value $p_i$ for that character.

Hint: there are many ways you could do this. What do _you_ think makes sense? Start with simplifying assumptions: for example, you could assume that the probabilities of encountering any two Pokemon on one visit to a gym are independent of each other.


```python
import numpy as np
import scipy.stats as stats
import seaborn as sns
import matplotlib.pyplot as plt

def plot_calibrate_frequency(pokedex_dict):

    sns.set_style('whitegrid')

    %config InlineBackend.figure_format = 'retina'
    %matplotlib inline

    xpoints = [val['Total'] for key, val in pokedex_dict.items()]

    #Define variables for 1,2,3 sigma
    std1 = np_mean + np_std
    std1_neg = lower_limit_one_sigma = np_mean - np_std
    std2 = np_mean + 2 * np_std
    std2_neg = lower_limit_two_sigma = np_mean - 2 * np_std
    std3 = np_mean + 3 * np_std
    std3_neg = lower_limit_two_sigma = np_mean - 3 * np_std

    #Start Figure
    #---------------------------------------
    # Initialize a matplotlib "figure"
    fig, ax = plt.subplots(figsize=(8,5))

    # 68%:
    ax.axvline(std1_neg, ls='dashed', lw=3, color='#333333', alpha=0.7)
    ax.axvline(std1, ls='dashed', lw=3, color='#333333', alpha=0.7)

    # 95%
    ax.axvline(std2_neg, ls='dashed', lw=3, color='#666666', alpha=0.7)
    ax.axvline(std2, ls='dashed', lw=3, color='#666666', alpha=0.7)

    # 99.7%
    ax.axvline(std3, ls='dashed', lw=3, color='#999999', alpha=0.7)
    ax.axvline(std3_neg, ls='dashed', lw=3, color='#999999', alpha=0.7)

    # plot the lines using matplotlib's hist function:
    ax.hist(xpoints,normed=True, bins=100)
    plt.show()
```


```python
import numpy as np
import scipy.stats as stats
import seaborn as sns
import matplotlib.pyplot as plt

def calibrate_frequency(pokedex_number):
    """
    Filter all filter options and return multiple elements from the pokedox

    Args:
        pokedex_number (int): Pokedex number to find out the character

    using 68-95-99.7 rule, find out the overpowered character and returns probability of finding
    that character of each visit

    Returns:
        list: Returns a value which is the probability of finding a character
    """

    pokedex_total = [val['Total'] for key, val in pokedex_dict.items() if val['PokedexNumber'] == pokedex_number]


    # Set Rules Variables
    lower_limit_one_sigma = np_mean - np_std
    upper_limit_one_sigma = np_mean + np_std

    lower_limit_two_sigma = np_mean - 2 * np_std
    upper_limit_two_sigma = np_mean + 2 * np_std

    X = max(pokedex_total)

    print('Total: ', X)

    empirical_68 = 1 - 0.6827
    empirical_95 = 1 - 0.9545
    empirical_99 = 1 - 0.9973

    # Check where X lies according to 68–95–99.7 rule
    if (X > lower_limit_one_sigma and X < upper_limit_one_sigma):
        return empirical_68
    elif (X > lower_limit_two_sigma) and (X < upper_limit_two_sigma):
        return empirical_95
    else:
        return empirical_99
```


```python
plot_calibrate_frequency(pokedex_dict)
```


![image tooltip here](/img/output_77_0.png)



```python
for pokedex_number in [val['PokedexNumber'] for key, val in pokedex_dict.items()]:
    print('Pokedex Number:', pokedex_number)
    print('P(' + str(pokedex_number) + '): ' + str(calibrate_frequency(pokedex_number)))
```
