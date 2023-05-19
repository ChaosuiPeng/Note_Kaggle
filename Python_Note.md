## Terminology
= assignment operator

() parentheses 

\[ ] square brackets 

{ } curly braces

, comma

: colon

缩进的（部分） indented indentation

', " single quotes, double-quotes

## Error Types
NameError

TypeError：typle不支持item assignment

ValueError: lists.index("一个不存在的名字“）

SyntaxError：invalid syntax. 比如一句话三个引号，python会非常confused。

## Conditional statements
if
```python
if temp > 38:
    message = "Fever!"
```

if ... else
```python
if temp > 38:
    message = "Fever!"
else:
    message = "Normal temperature."
```

if ... elif ... else
```python
if temp > 38:
    message = "Fever!"
elif temp > 35:
    message = "Normal temperature."
else:
    message = "Low temperature."
```

## Data Types
- Integers
- Floats
- Booleans
- Strings， Strings can be marked either by double or single quotation marks

print() - To print multiple things in Python with a single command, we need only separate them with a comma.

type()
```python
x = 14
print(x)
print(type(x))
```

abs() - returns the absolute value of an argument
```python
print(abs(32))
print(abs(-32))
```

round() -  it lets you round a number to a specified number of decimal places.
```python
# Round to 5 decimal places
rounded_pi = round(almost_pi, 5)
print(rounded_pi)
print(type(rounded_pi))
```

not - switch the value of a boolean
```python
z_five = not z_four
print(z_five)
print(type(z_five))
```

len() - get the length of a string
```python
print(len(w))
```

empty string has length zero
```python
shortest_string = ""
print(type(shortest_string))
print(len(shortest_string))
```

float() - convert a convertible string to a float
```python
my_number = "1.12321"
print(my_number)
print(type(my_number))

also_my_number = float(my_number)
print(also_my_number)
print(type(also_my_number))
```

int and float can also be called as functions which convert their arguments to the corresponding type
```python
print(float(10))
print(int(3.33))
# They can even be called on strings!
print(int('807') + 1)
```

bool() - turns things into bools
```python
print(bool(1)) # all numbers are treated as true, except 0
print(bool("asf")) # all strings are treated as true, except the empty string ""
```

\+ - concatenat two strings
```python
new_string = "abc" + "def"
print(new_string)
print(type(new_string))
```

multiply a string by an integer (not a float!!! This would cause TypeError)
```python
newest_string = "abc" * 3
print(newest_string)
print(type(newest_string))
```

## arithmetic
![1684258368325](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/2cafadf7-2fb7-424a-81e0-57ec103b87a7)

The // operator gives us a result that's rounded down to the next integer.
```python
print(5 // 2)
print(6 // 2)
```
![1684258455347](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/55c6a4e1-0bc2-41d6-af1e-3d14fe5c6e62)

⚠ Order of operations: PEMDAS - Parentheses, Exponents, Multiplication/Division, Addition/Subtraction.

## Data Structures
- lists
- sets
- dictionaries
- tuples

### Lists
lists can have items with any data type, including booleans, integers, and floats.

to create a Python list, we need to use square brackets \[ , ] and separate each item with a comma (each item is enclosed in quotation marks).

We can put int or other types in lists.
```python
primes = [2, 3, 5, 7]
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
```

make a list of lists
```python
hands = [
    ['J', 'Q', 'K'],
    ['2', '2', '2'],
    ['6', 'A', 'K'], # (Comma after the last element is optional)
]
# (I could also have written this on one line, but it can get hard to read)
hands = [['J', 'Q', 'K'], ['2', '2', '2'], ['6', 'A', 'K']]
```

A list can contain a mix of different types of variables:
```python
my_favourite_things = [32, 'raindrops on roses', help]
```

and print them
```python
flowers_list = ["pink primrose", "hard-leaved pocket orchid", "canterbury bells", "sweet pea", "english marigold", "tiger lily", "moon orchid", "bird of paradise", "monkshood", "globe thistle"]

print(type(flowers_list))
print(flowers_list)
```
![1684256830547](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/769b61fe-795c-4ea5-b445-8d61f3cbae2e)

**counting** 
len() - count the number of entries in a list
```python
print(len(flowers_list))
```

sum() - add every item in the list. Note that we can do similar calculations with slices of the list.
```python
print("Total books sold in one week:", sum(hardcover_sales))
print("Average books sold in first five days:", sum(hardcover_sales[:5])/5)
```

**indexing**

refer to any item in the list according to its position in the list. note that it is zero-based indexing.
```python
print("First entry:", flowers_list[0])
print("Second entry:", flowers_list[1])

# The list has length ten, so we refer to final entry with 9 or -1
print("Last entry:", flowers_list[9])
flowers_list[-1]
```

**checking**
in operator - to determine whether a list contains a particular value:
```python
# Is Earth a planet?
"Earth" in planets # return True / False
```

**Slicing** - to pull the first x entries, you use \[:x], and to pull the last y entries, you use \[-y:]
```python
print("First three entries:", flowers_list[:3])
# flowers_list[0:3] is our way of asking for the elements of planets starting from index 0 and continuing up to but not including index 3.

print("Final two entries:", flowers_list[-2:])
```


**modifying**

Lists are "mutable", meaning they can be modified "in place".
```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
planets[3] = 'Malacandra'
# or
planets[:3] = ['Mur', 'Vee', 'Ur']
```

.remove() - removing items
```python
flowers_list.remove("globe thistle")
print(flowers_list)
```

.append() - adding an item to the end. note that it's a method carried around by all objects of type list,
```python
flowers_list.append("snapdragon")
print(flowers_list)
```

.pop - removes and returns the last element of a list:
```python
planets.pop()
```

**sorting**

sorted returns a sorted version of a list:

The planets sorted in alphabetical order
```python
>>> sorted(planets)
['Earth', 'Jupiter', 'Mars', 'Mercury', 'Neptune', 'Saturn', 'Uranus', 'Venus']
```

**Searching **

get its index using the list.index method
```python
planets.index('Earth')
```

get the minimum with min() and the maximum with max()
```python
hardcover_sales = [139, 128, 172, 139, 191, 168, 170]
print("Minimum:", min(hardcover_sales))
print("Maximum:", max(hardcover_sales))
```
![1684257210121](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/aa4879ba-6974-498b-b347-4c6d7ba8397e)

## List Comprehensions
```python
squares = [n**2 for n in range(10)]
squares # returns "[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]"
```

this is equivalent to
```python
squares = []
for n in range(10):
    squares.append(n**2)
squares
```

升级版的comprehensions
```python
squares = [n**2 for n in range(10) if n**2 % 2 ==0]
squares # returns "[0, 4, 16, 36, 64]"
```

可以再复杂一点
```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']

# str.upper() returns an all-caps version of a string
loud_short_planets = [planet.upper() + '!' for planet in planets if len(planet) < 6]
loud_short_planets

# or make the structure clearer, split it up over 3 lines
[
    planet.upper() + '!' 
    for planet in planets 
    if len(planet) < 6
]

```



## Objects
an object can carry attributes and methods

for exanple: numbers in Python
```python
x = 12

# an associated variable called imag representing their imaginary part
# x is a real number, so its imaginary part is 0.
print(x.imag)

# Number of bits necessary to represent self in binary.
x.bit_length()
```

bit_length()
```python
>>> bin(37)
'0b100101'
>>> (37).bit_length()
6
```



## Tuples
ALMOST exactly the same as lists, except two ways:

**creating**
```python
t = (1, 2, 3)
t = 1, 2, 3 # equivalent to above
```

**immutable**
cannot be modified 
```python
t[0] = 100 # TypeError
```

**用法**
for functions that have multiple return values
```python
# as_integer_ratio() method of float objects returns a numerator and a denominator in the form of a tuple
x = 0.125
x.as_integer_ratio() # (1, 8)

numerator, denominator = x.as_integer_ratio()
print(numerator / denominator) # 0.125

```


## Loops
**for in**
The object to the right of the "in" can be any object that supports iteration.
```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
for planet in planets:
    print(planet, end=' ') # print all on same line

# output: Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune 
```

loop through each character in a string:
```python
s = 'steganograpHy is the practicE of conceaLing a file, message, image, or video within another fiLe, message, image, Or video.'
msg = ''
# print all the uppercase letters in s, one at a time
for char in s:
    if char.isupper():
        print(char, end='')   

# return : HELLO
```

returns a sequence of numbers:
```python
for i in range(5):
    print("Doing important work. i =", i)
```

while loops
```python
i = 0
while i < 10:
    print(i, end=' ')
    i += 1 # increase the value of i by 1

# return: 0 1 2 3 4 5 6 7 8 9
```




## Strings

Strings can be thought of as sequences of characters.

**ALMOST** everything we've seen that we can do to a list, we can also do to a string.

```python
# Indexing
planet = 'Pluto'
planet[0] # returns 'P'
```

```python
# Slicing
planet[-3:] # returns 'uto'
```

```python
# How long is this string?
len(planet) #returns 5
```

**Immutable**
 We can't modify them!!!! might cause TypeError!!!
 
 **Methods**

```python
# ALL CAPS
claim = "Pluto is a planet!"
claim.upper() # returns 'PLUTO IS A PLANET'
```

```python
# all lowercase
claim.lower() # returns 'pluto is a planet!'
```

```python
# Searching for the first index of a substring
claim.index('plan') # returns 11
```

```python
# checking startswith and endwith 
# Return True if S starts with the specified prefix, False otherwise.
claim.startswith(planet) #returns True

# false because of missing exclamation mark
claim.endswith('planet') 
```

```python
#splitting
words = claim.split()
words # returns ['Pluto', 'is', 'a', 'planet!']

datestr = '1956-01-31'
year, month, day = datestr.split('-')
```

```python
# joining
'/'.join([month, day, year]) # returns '01/31/1956'

# Yes, we can put unicode characters right in our string literals :)
' 👏 '.join([word.upper() for word in words])  # returns 'PLUTO 👏 IS 👏 A 👏 PLANET!'

planet + ', we miss you.'  # returns 'Pluto, we miss you.'

# ⚠ but remember to call str() first if we want to throw in any non-string objects. Otherwise there will be a TypeError
position = 9
planet + ", you'll always be the " + str(position) + "th planet to me."
```

```python
# formatting

"{}, you'll always be the {}th planet to me.".format(planet, position)  # returns "Pluto, you'll always be the 9th planet to me."


# 2 decimal point   3 decimal points, format as percent   separate with commas
pluto_mass = 1.303 * 10**22
earth_mass = 5.9722 * 10**24
population = 52910390
"{} weighs about {:.2} kilograms ({:.3%} of Earth's mass). It is home to {:,} Plutonians.".format(
    planet, pluto_mass, pluto_mass / earth_mass, population,
)  # returns "Pluto weighs about 1.3e+22 kilograms (0.218% of Earth's mass). It is home to 52,910,390 Plutonians."

# Referring to format() arguments by index, starting from 0
s = """Pluto's a {0}.
No, it's a {1}.
{0}!
{1}!""".format('planet', 'dwarf planet')
print(s)
# returns 
# Pluto's a planet.
# No, it's a dwarf planet.
# planet!
# dwarf planet!
```


## Dictionaries
 a built-in Python data structure for mapping keys to values

**creating**
 ```python
 numbers = {'one':1, 'two':2, 'three':3} # keys: corresponding values
 ```

**accessing values**
```python
numbers['one'] # returns 1
```

**adding another key, value pair**
```python
numbers['eleven'] = 11
numbers #returns {'one': 1, 'two': 2, 'three': 3, 'eleven': 11}
```

**dictionary comprehensions**
```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
planet_to_initial = {planet: planet[0] for planet in planets}
planet_to_initial

# returns
# {'Mercury': 'M',
#  'Venus': 'V',
#  'Earth': 'E',
#  'Mars': 'M',
#  'Jupiter': 'J',
#  'Saturn': 'S',
#  'Uranus': 'U',
#  'Neptune': 'N'}
```

**checking if a key is in the dictionary**
```python
'Saturn' in planet_to_initial # returns True
```

**accessing keys and values**
```python
# for loop
for k in numbers:
    print("{} = {}".format(k, numbers[k]))
# returns
# one = Pluto
# two = 2
# three = 3
# eleven = 11

# dict.keys() and dict.values()
# Get all the initials, sort them alphabetically, and put them in a space-separated string.
' '.join(sorted(planet_to_initial.values())) # returns 'E J M M N S U V'

# dict.item()
for planet, initial in planet_to_initial.items():
    print("{} begins with \"{}\"".format(planet.rjust(10), initial))
# returns 
#  Mercury begins with "M"
#    Venus begins with "V"
#    Earth begins with "E"
#     Mars begins with "M"
#  Jupiter begins with "J"
#   Saturn begins with "S"
#   Uranus begins with "U"
#  Neptune begins with "N"
```


## Math

We can see all the names in math using the built-in function dir(). （不知道有什么用）

we can access some variables.
```python
math.pi # returns 3.1415926....
```

functions
```python
math.log(4, 2) # returns 2.0
```

## numpy
```python
rolls = numpy.random.randint(low=1, high=6, size=10)
rolls # returns array([3, 4, 3, 4, 5, 5, 2, 1, 3, 3])
```
