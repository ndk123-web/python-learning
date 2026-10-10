## 1. Initialize karna

| Data structure   | Syntax         | Example         |
| ---------------- | -------------- | --------------- |
| List             | `[]`           | `a = [3, 1, 2]` |
| Empty list       | `list()`       | `a = list()`    |
| Set              | `{...}`        | `s = {1, 2, 3}` |
| Empty set        | `set()`        | `s = set()`     |
| Dictionary       | `{key: value}` | `d = {"a": 10}` |
| Empty dictionary | `{}`           | `d = {}`        |
| Tuple            | `(...)`        | `t = (1, 2, 3)` |
| String           | Quotes         | `s = "hello"`   |

```
nums = [1, 2, 2, 3]unique = {1, 2, 3}person = {"name": "Amit", "age": 21}
```

Remember:

- List: ordered, duplicates allowed.
- Set: unique elements, no guaranteed iteration order.
- Dict: key-value pairs, keys unique.
- `{} ` is an empty dictionary, not a set.

## 2. Loop through everything

List

```
nums = [10, 20, 30]for x in nums:    print(x)for i in range(len(nums)):    print(i, nums[i])for i, x in enumerate(nums):    print(i, x)
```

Set

```
s = {10, 20, 30}for x in s:    print(x)
```

Dictionary — keys, values, both

```
d = {"a": 10, "b": 20}for key in d:    print(key)for value in d.values():    print(value)for key, value in d.items():    print(key, value)
```

String

```
s = "hello"for ch in s:    print(ch)
```

Nested list / list of dictionaries

```
users = [    {"name": "A", "age": 20},    {"name": "B", "age": 25}]for user in users:    print(user["name"], user["age"])
```

## 3. List operations

```
a = [3, 1, 2]a.append(4)       # Add one elementa.extend([5, 6])  # Add multiple elementsa.insert(0, 9)    # Insert at index 0a.remove(3)       # Remove first matching valuex = a.pop()       # Remove and return last elementa.pop(0)          # Remove element at index 0a.sort()          # Sort original lista.reverse()       # Reverse original listlen(a)            # Lengtha[0]              # First elementa[-1]             # Last elementa[1:3]            # Slice: index 1, 23 in a            # Membership check
```

Copying and duplicates:

```
a = [1, 2, 2, 3]b = a.copy()unique = list(set(a))
```

Note: `list(set(a))` removes duplicates but does not guarantee original order.

## 4. Set operations

```
a = {1, 2, 3}b = {3, 4, 5}a.add(4)             # Add elementa.discard(2)         # Remove if present; no error if missing3 in a               # Membershipa | b                # Union: {1, 2, 3, 4, 5}a & b                # Intersectiona - b                # Differencea ^ b                # Symmetric differencelen(a)               # Number of unique elements
```

Use cases: duplicate removal, membership checks, common elements, unique values.

## 5. Dictionary operations

```
d = {"a": 10, "b": 20}d["a"]                # Get value: 10d["c"] = 30           # Add keyd["a"] = 99           # Update valued.get("x", 0)         # Missing key -> 0"a" in d              # Checks keys10 in d.values()      # Checks valuesd.keys()              # All keysd.values()            # All valuesd.items()             # Key-value pairsdel d["a"]             # Delete keyd.pop("b", None)       # Remove key safelylen(d)                 # Number of key-value pairs
```

Frequency counting — very important:

```
s = "banana"freq = {}for ch in s:    freq[ch] = freq.get(ch, 0) + 1# {'b': 1, 'a': 3, 'n': 2}
```

For a list:

```
nums = [1, 2, 1, 3, 2, 1]freq = {}for x in nums:    freq[x] = freq.get(x, 0) + 1
```

Group values by key:

```
groups = {}for word in ["ant", "apple", "bat"]:    key = word[0]    if key not in groups:        groups[key] = []    groups[key].append(word)# {'a': ['ant', 'apple'], 'b': ['bat']}
```

## 6. Sorting — must remember

A. Normal list

```
nums = [5, 2, 8, 1]sorted_nums = sorted(nums)# [1, 2, 5, 8]descending = sorted(nums, reverse=True)# [8, 5, 2, 1]nums.sort()  # Modifies original list
```

B. List of dictionaries — tere interview wala case

```
segments = [    {"id": "12", "speaker": "maya"},    {"id": "5", "speaker": "candidate"},    {"id": "20", "speaker": "pori"}]# Sort by id as stringresult = sorted(segments, key=lambda x: x["id"])# Sort by id numericallyresult = sorted(segments, key=lambda x: int(x["id"].strip()))# Sort by speakerresult = sorted(segments, key=lambda x: x["speaker"])# Descending by id numericallyresult = sorted(    segments,    key=lambda x: int(x["id"].strip()),    reverse=True)
```

C. Dictionary by values

```
d = {"apple": 3, "banana": 1, "cherry": 2}sorted_items = sorted(d.items(), key=lambda x: x[1])# [('banana', 1), ('cherry', 2), ('apple', 3)]
```

D. Sort by multiple fields

```
students = [    {"name": "A", "marks": 80},    {"name": "B", "marks": 80},    {"name": "C", "marks": 90}]result = sorted(students, key=lambda x: (-x["marks"], x["name"]))
```

This sorts marks descending, then name ascending.

Remember:

- `sorted(x)` → returns a new sorted list.
- `x.sort()` → modifies the original list.
- `key=lambda x: x["age"]` → sort using the `age` field.
- `reverse=True` → descending order.
- `"12"` and `"5"` sort differently as strings than as numbers.

## 7. String operations

```
s = "  Hello World  "s.strip()             # Remove leading/trailing whitespaces.lower()             # Lowercases.upper()             # Uppercases.capitalize()        # First character uppercases.title()             # Each word capitalizeds.replace("World", "Python")s.split()             # Split on whitespace"-".join(["a", "b"])  # "a-b"s.startswith("  He")  # Trues.endswith("  ")      # Trues.find("World")       # Index, or -1 if not founds.count("l")          # Count occurrencess[::-1]               # Reverse strings[0]                  # First characters[-1]                 # Last characters[1:4]                # Slicelen(s)                # Length
```

Interview pattern: normalize before comparing

```
speaker = dictionary["speaker"].strip().lower()if speaker in {"candidate", "maya"}:    print("Matched")
```

`strip()` removes surrounding whitespace; `lower()` makes the comparison case-insensitive.

Split and join:

```
s = "python is easy"words = s.split()# ['python', 'is', 'easy']reversed_words = words[::-1]result = " ".join(reversed_words)# "easy is python"
```

## 8. Conditions, membership and loops

```
if x > 10:    print("Big")elif x == 10:    print("Equal")else:    print("Small")
```

```
x in nums                 # Membershipx not in nums             # Not presentif x > 0 and x < 10:    print("Between")if x == 1 or x == 2:    print("One or two")
```

Loop helpers:

```
range(5)          # 0, 1, 2, 3, 4range(1, 5)       # 1, 2, 3, 4range(5, 0, -1)   # 5, 4, 3, 2, 1for i, value in enumerate(nums):    print(i, value)
```

Comprehensions:

```
squares = [x * x for x in nums]evens = [x for x in nums if x % 2 == 0]unique = {x for x in nums}freq = {x: nums.count(x) for x in set(nums)}
```

The last example works, but for large inputs, a frequency-counting loop is generally more efficient.

## 9. Useful built-ins

| Function           | Use                         |
| ------------------ | --------------------------- |
| `len(x)`           | Length / number of items    |
| `sum(nums)`        | Sum                         |
| `min(nums)`        | Minimum                     |
| `max(nums)`        | Maximum                     |
| `sorted(nums)`     | Sorted copy                 |
| `reversed(nums)`   | Reverse iterator            |
| `enumerate(nums)`  | Index + value               |
| `zip(a, b)`        | Pair elements               |
| `any(nums)`        | At least one truthy element |
| `all(nums)`        | All elements truthy         |
| `abs(x)`           | Absolute value              |
| `round(x, 2)`      | Round to 2 decimals         |
| `type(x)`          | Type of object              |
| `int(x)`, `str(x)` | Type conversion             |

Example:

```
names = ["A", "B"]marks = [80, 90]for name, mark in zip(names, marks):    print(name, mark)
```

## 10. Common interview patterns

Remove duplicates while preserving order

```
nums = [1, 2, 1, 3, 2]result = list(dict.fromkeys(nums))# [1, 2, 3]
```

Find common elements

```
common = set(a) & set(b)
```

Filter a list of dictionaries

```
result = [    d for d in segments    if d["speaker"].strip().lower() in {"maya", "candidate"}]
```

Find the most frequent element

```
freq = {}for x in nums:    freq[x] = freq.get(x, 0) + 1most_frequent = max(freq, key=freq.get)
```

Count words

```
words = "hi hello hi".split()freq = {}for word in words:    freq[word] = freq.get(word, 0) + 1
```

Check palindrome

```
s == s[::-1]
```

Sort and select top 3

```
top_three = sorted(nums, reverse=True)[:3]
```

## 11. Common mistakes — interview mein dhyaan rakhna

| Mistake                         | Correct approach                           |
| ------------------------------- | ------------------------------------------ |
| Empty set: `{}`                 | `set()`                                    |
| Dict values loop karna          | `d.values()`                               |
| Dict key-value loop             | `d.items()`                                |
| Missing key safely read         | `d.get(key, default)`                      |
| `sort()` ka result assign karna | Use `sorted()` if you need a returned list |
| `"12"` vs `"5"` numeric sorting | `key=lambda x: int(x)`                     |
| Whitespace/case mismatch        | `.strip().lower()`                         |
| Set se duplicates remove karna  | `set(nums)`                                |
| Dictionary mein membership      | `key in d` checks keys                     |
| Empty list ka last index        | Check before accessing `a[-1]`             |

## 12. Last-minute revision checklist

Revision tracker

0/10

List / set / dict initialize karna

List, set, dict par loops

Dictionary keys, values, items

append, add, get, pop, discard

String strip, lower, split, join, slicing

sorted, sort, lambda, reverse=True

Frequency counting using dict.get()

Filtering list of dictionaries

Set intersection / union

Empty input and missing-key edge cases

Meri recommendation: Is sheet ko ek baar read kar, phir examples ko hide karke blank editor mein khud likh. Sirf padhne se familiarity aayegi; bina dekhe likhne se interview recall improve hoga.

Aur tere interview ke liye sabse important five topics hain: dictionary iteration, set membership, string normalization, sorting with `key=lambda`, and frequency counting. Inko pehle pakka kar.
