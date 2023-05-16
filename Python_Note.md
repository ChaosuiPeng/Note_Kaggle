
## Error Types
NameError

TypeError

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
- Strings

print() - To print multiple things in Python with a single command, we need only separate them with a comma.

type()
```python
x = 14
print(x)
print(type(x))
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

## Data Structures
- lists
- sets
- dictionaries
- tuples

### Lists
lists can have items with any data type, including booleans, integers, and floats.

to create a Python list, we need to use square brackets \[ , ] and separate each item with a comma (each item is enclosed in quotation marks).
```python
flowers_list = ["pink primrose", "hard-leaved pocket orchid", "canterbury bells", "sweet pea", "english marigold", "tiger lily", "moon orchid", "bird of paradise", "monkshood", "globe thistle"]

print(type(flowers_list))
print(flowers_list)
```
![1684256830547](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/769b61fe-795c-4ea5-b445-8d61f3cbae2e)

len() - count the number of entries in a list
```python
print(len(flowers_list))
```
indexing - refer to any item in the list according to its position in the list
```python
print("First entry:", flowers_list[0])
print("Second entry:", flowers_list[1])

# The list has length ten, so we refer to final entry with 9
print("Last entry:", flowers_list[9])
```

Slicing - to pull the first x entries, you use \[:x], and to pull the last y entries, you use \[-y:]
```python
print("First three entries:", flowers_list[:3])
print("Final two entries:", flowers_list[-2:])
```

.remove() - removing items
```python
flowers_list.remove("globe thistle")
print(flowers_list)
```

.append() - adding items
```python
flowers_list.append("snapdragon")
print(flowers_list)
```

get the minimum with min() and the maximum with max()
```python
hardcover_sales = [139, 128, 172, 139, 191, 168, 170]
print("Minimum:", min(hardcover_sales))
print("Maximum:", max(hardcover_sales))
```
![1684257210121](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/aa4879ba-6974-498b-b347-4c6d7ba8397e)


sum() - add every item in the list. Note that we can do similar calculations with slices of the list.
```python
print("Total books sold in one week:", sum(hardcover_sales))
print("Average books sold in first five days:", sum(hardcover_sales[:5])/5)
```
![1684257220027](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/781cc23b-87bf-41b8-b49d-1640b0bb366f)
![1684257285411](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/87143dc9-e9d2-4abf-9e00-b7fa6ed0b430)


