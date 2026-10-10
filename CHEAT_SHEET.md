# Python Basics — Interview Cheat Sheet

> Quick revision for basic Python coding interviews. No OOP or advanced topics.
> Focus: initialization, loops, lists, sets, dictionaries, strings, sorting, and common patterns.

## 1. Initialize Data Structures

| Structure | Syntax | Example |
|---|---|---|
| List | `[]` | `nums = [3, 1, 2]` |
| Empty list | `list()` or `[]` | `nums = []` |
| Set | `{...}` | `s = {1, 2, 3}` |
| Empty set | `set()` | `s = set()` |
| Dictionary | `{key: value}` | `d = {"a": 10}` |
| Empty dictionary | `{}` | `d = {}` |
| Tuple | `(...)` | `t = (1, 2, 3)` |
| String | Quotes | `s = "hello"` |

```python
nums = [1, 2, 2, 3]
unique = {1, 2, 3}
person = {"name": "Amit", "age": 21}
```

**Remember**
- List: ordered, duplicates allowed.
- Set: unique elements; iteration order is not guaranteed.
- Dictionary: key-value pairs; keys are unique.
- `{}` creates an empty dictionary, not an empty set. Use `set()`.

## 2. Loops

### List

```python
nums = [10, 20, 30]

for x in nums:
    print(x)

for i in range(len(nums)):
    print(i, nums[i])

for i, x in enumerate(nums):
    print(i, x)
```

### Set

```python
s = {10, 20, 30}

for x in s:
    print(x)
```

### Dictionary: keys, values, and pairs

```python
d = {"a": 10, "b": 20}

# Keys
for key in d:
    print(key)

# Values
for value in d.values():
    print(value)

# Key-value pairs
for key, value in d.items():
    print(key, value)
```

### String

```python
s = "hello"

for ch in s:
    print(ch)
```

### List of dictionaries

```python
users = [
    {"name": "A", "age": 20},
    {"name": "B", "age": 25},
]

for user in users:
    print(user["name"], user["age"])
```

## 3. List Operations

```python
a = [3, 1, 2]

a.append(4)       # Add one element
a.extend([5, 6])  # Add multiple elements
a.insert(0, 9)    # Insert at index 0

a.remove(3)       # Remove first matching value
x = a.pop()       # Remove and return last element
a.pop(0)          # Remove element at index 0

a.sort()          # Sort the original list
a.reverse()       # Reverse the original list

len(a)            # Length
a[0]              # First element
a[-1]             # Last element
a[1:3]            # Slice: indices 1 and 2
3 in a            # Membership check
```

### Copying and removing duplicates

```python
a = [1, 2, 2, 3]

b = a.copy()
unique = list(set(a))  # Removes duplicates; order is not guaranteed

# Remove duplicates while preserving insertion order
unique_ordered = list(dict.fromkeys(a))  # [1, 2, 3]
```

## 4. Set Operations

```python
a = {1, 2, 3}
b = {3, 4, 5}

a.add(4)             # Add element
a.discard(2)         # Remove if present; no error if absent
3 in a               # Membership check

a | b                # Union
a & b                # Intersection
a - b                # Difference: elements in a but not b
a ^ b                # Symmetric difference: in either, but not both

len(a)               # Number of unique elements
```

**Common uses:** duplicate removal, fast membership checks, finding common/unique elements.

## 5. Dictionary Operations

```python
d = {"a": 10, "b": 20}

d["a"]                # Read value: 10
d["c"] = 30           # Add key
d["a"] = 99           # Update value
d.get("x", 0)         # Missing key -> default 0

"a" in d              # Checks keys
10 in d.values()      # Checks values

d.keys()              # All keys
d.values()            # All values
d.items()             # Key-value pairs

del d["a"]             # Delete key
d.pop("b", None)       # Remove key safely
len(d)                 # Number of key-value pairs
```

### Frequency counting (very common)

```python
s = "banana"
freq = {}

for ch in s:
    freq[ch] = freq.get(ch, 0) + 1

# {'b': 1, 'a': 3, 'n': 2}
```

Same pattern for a list:

```python
nums = [1, 2, 1, 3, 2, 1]
freq = {}

for x in nums:
    freq[x] = freq.get(x, 0) + 1

# {1: 3, 2: 2, 3: 1}
```

### Group values by key

```python
groups = {}

for word in ["ant", "apple", "bat"]:
    key = word[0]

    if key not in groups:
        groups[key] = []

    groups[key].append(word)

# {'a': ['ant', 'apple'], 'b': ['bat']}
```

## 6. Sorting

### Sort a normal list

```python
nums = [5, 2, 8, 1]

ascending = sorted(nums)                    # New list: [1, 2, 5, 8]
descending = sorted(nums, reverse=True)     # [8, 5, 2, 1]

nums.sort()  # Modifies nums in place
```

- `sorted(iterable)` returns a new sorted list.
- `list.sort()` modifies the original list and returns `None`.

### Sort a list of dictionaries by a field

```python
segments = [
    {"id": "12 ", "speaker": "maya"},
    {"id": "5", "speaker": "candidate"},
    {"id": "20", "speaker": "pori"},
]

# Sort by id as a string
by_id_string = sorted(segments, key=lambda x: x["id"])

# Sort by numeric id, ignoring surrounding whitespace
by_id_number = sorted(
    segments,
    key=lambda x: int(x["id"].strip())
)

# Sort by speaker
by_speaker = sorted(segments, key=lambda x: x["speaker"])

# Descending numeric id
by_id_desc = sorted(
    segments,
    key=lambda x: int(x["id"].strip()),
    reverse=True
)
```

### Sort a dictionary by its values

```python
d = {"apple": 3, "banana": 1, "cherry": 2}

sorted_items = sorted(d.items(), key=lambda item: item[1])
# [('banana', 1), ('cherry', 2), ('apple', 3)]
```

### Sort by multiple fields

```python
students = [
    {"name": "A", "marks": 80},
    {"name": "B", "marks": 80},
    {"name": "C", "marks": 90},
]

# Marks descending, then name ascending
result = sorted(students, key=lambda x: (-x["marks"], x["name"]))
```

### Understand `lambda`

```python
key=lambda x: x["age"]
```

- `x` is one element from the list.
- `x["age"]` extracts the age.
- Python sorts elements by the extracted value.

## 7. String Operations

```python
s = "  Hello World  "

s.strip()                 # Remove surrounding whitespace
s.lower()                 # Lowercase
s.upper()                 # Uppercase
s.capitalize()            # First character uppercase
s.title()                 # Capitalize each word

s.replace("World", "Python")
s.split()                 # Split on whitespace
"-".join(["a", "b"])       # "a-b"

s.startswith("  He")      # True
s.endswith("  ")          # True
s.find("World")            # Index, or -1 if absent
s.count("l")               # Count occurrences

s[::-1]                   # Reverse string
s[0]                      # First character
s[-1]                     # Last character
s[1:4]                    # Slice
len(s)                    # Length
```

### Normalize before comparing

```python
speaker = dictionary["speaker"].strip().lower()

if speaker in {"candidate", "maya"}:
    print("Matched")
```

- `.strip()` removes leading/trailing whitespace.
- `.lower()` makes comparison case-insensitive.

### Split, reverse words, and join

```python
s = "python is easy"

words = s.split()             # ['python', 'is', 'easy']
reversed_words = words[::-1]
result = " ".join(reversed_words)  # "easy is python"
```

## 8. Conditions and Membership

```python
if x > 10:
    print("Big")
elif x == 10:
    print("Equal")
else:
    print("Small")
```

```python
x in nums
x not in nums

if 0 < x < 10:
    print("Between 0 and 10")

if x == 1 or x == 2:
    print("One or two")

if x in {1, 2}:
    print("One or two")
```

## 9. Loop Helpers and Ranges

```python
range(5)          # 0, 1, 2, 3, 4
range(1, 5)       # 1, 2, 3, 4
range(5, 0, -1)   # 5, 4, 3, 2, 1

for i, value in enumerate(nums):
    print(i, value)

names = ["A", "B"]
marks = [80, 90]

for name, mark in zip(names, marks):
    print(name, mark)
```

## 10. Comprehensions

```python
squares = [x * x for x in nums]

evens = [x for x in nums if x % 2 == 0]

unique = {x for x in nums}

# Count each distinct value (fine for small lists; repeated count scans)
freq = {x: nums.count(x) for x in set(nums)}
```

For large inputs, use the dictionary frequency-counting loop from Section 5 instead of repeatedly calling `nums.count(x)`.

## 11. Useful Built-ins

| Function | Purpose |
|---|---|
| `len(x)` | Length / number of items |
| `sum(nums)` | Sum |
| `min(nums)` | Minimum |
| `max(nums)` | Maximum |
| `sorted(nums)` | Return sorted list |
| `reversed(nums)` | Reverse iterator |
| `enumerate(nums)` | Index and value |
| `zip(a, b)` | Pair items from iterables |
| `any(items)` | True if at least one item is truthy |
| `all(items)` | True if every item is truthy |
| `abs(x)` | Absolute value |
| `round(x, 2)` | Round to two decimal places |
| `type(x)` | Object type |
| `int(x)`, `str(x)`, `float(x)` | Type conversion |

## 12. Common Interview Patterns

### Filter a list of dictionaries

```python
new_segments = [
    d for d in segments
    if d["speaker"].strip().lower() in {"maya", "candidate"}
]
```

### Find common elements

```python
common = set(a) & set(b)
```

### Find the most frequent element

```python
freq = {}

for x in nums:
    freq[x] = freq.get(x, 0) + 1

most_frequent = max(freq, key=freq.get)
```

### Check a palindrome

```python
is_palindrome = (s == s[::-1])
```

### Get the top three numbers

```python
top_three = sorted(nums, reverse=True)[:3]
```

### Safely access the last element

```python
if nums:
    last = nums[-1]
```

### Avoid `KeyError`

```python
value = d.get("missing_key", 0)
```

## 13. Common Mistakes

| Mistake | Correct approach |
|---|---|
| `{} ` used as empty set | Use `set()` |
| Loop over dictionary values using `for x in d` | Use `for x in d.values()` |
| Need both key and value | Use `for k, v in d.items()` |
| Missing key might cause `KeyError` | Use `d.get(key, default)` |
| Assign result of `list.sort()` | Use `sorted(list)` to get a returned list |
| Numeric IDs sorted as strings | Use `key=lambda x: int(x.strip())` |
| Whitespace/case mismatch | Normalize with `.strip().lower()` |
| Access last item of empty list | Check `if nums:` first |
| Assume set iteration order | Do not depend on set order |
| `key=lambda x: x["field"]` feels confusing | It extracts the sort key from each element |

## 14. Rapid Revision Checklist

Before an interview, make sure you can write these without looking:

- [ ] Initialize a list, set, and dictionary.
- [ ] Loop through list elements and use `enumerate()`.
- [ ] Loop through dictionary keys, values, and items.
- [ ] Use `append`, `add`, `get`, `pop`, and `discard`.
- [ ] Normalize strings using `strip()` and `lower()`.
- [ ] Use `split()`, `join()`, slicing, and `replace()`.
- [ ] Sort lists and lists of dictionaries using `key=lambda`.
- [ ] Count frequencies using `dict.get()`.
- [ ] Use sets for unique values and intersections.
- [ ] Handle empty lists and missing dictionary keys.

## Suggested Revision Method

1. Read the sheet once.
2. Close it and rewrite the examples in a blank editor.
3. If you forget syntax, look up only that syntax.
4. Close the sheet and write the code again from memory.
5. Practise small variations rather than memorizing outputs.
