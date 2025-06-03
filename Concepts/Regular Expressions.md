All the regex functions in Python are in the re module. Enter the following into the interactive shell to import this module:

```python
import re
```

Passing a string value representing your regex to re.compile() returns a Regex pattern object. The pattern written using re.compile is searched in the string given to the search() method. If there is no value in the string that matches the pattern we are looking for, None is returned. If there is a matching pattern in the string, a `Match` object with the expression group() method is returned.  Here for example 

```python
phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
mo = phoneNumRegex.search('My number is 415-555-4242.')

print(f'Phone number found: {mo.group()}') # Phone number found: 415-555-4242
```

## Grouping with Parentheses

If you want to separate the area code from the rest of the phone number. You can add parentheses this will be create a group. `regex: (\d\d\d)-(\d\d\d-\d\d\d\d)` After you wrote this you can access the area code with `group(1)`. You can grab different parts of the matched test. Passing 0 or nothing to the group() method will return the entire matched text. For example

```python
phoneNumRegex = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)')
mo = phoneNumRegex.search('My number is 415-555-4242.')

print(f'Phone number found: {mo.group()}') # Phone number found: 415-555-4242
print(f'Phone number found: {mo.group(0)}') # Phone number found: 415-555-4242
print(f'Area code found: {mo.group(1)}') # Area code found: 415
print(f'Rest of the number: {mo.group(2)}') # Rest of the number: 555-4242
```

If you want the find parentheses is the string you have to use '\\' escape character. For example

```python
phoneNumRegex = re.compile(r'(\(\d\d\d\)) (\d\d\d-\d\d\d\d)')
mo = phoneNumRegex.search('My number is (415) 555-4242.')

print(f'Area code found: {mo.group(1)}') # Area code found: (415)
```

You have to use the escape character in this special meaning characters: `'.', '^', '$', '*', '+', '?', '{ }', '[ ]', '\', '|', '( )'` -> `'\.', '\^', '\$', '\*', '\+', '\?', '\{ \}', '\[ \]', '\\', '\|', '\( \)'`

## Matching Multiple Group with the Pipe

The regex pattern you write can do more than just find something in a string. The | character is called a pipe. You can write this in your pattern when you want to find more than one thing in a sentence. For example

```python
instrument = re.compile(r'Drum|Guitar|Bass Guitar')
mo = instrument.search('I can play Drum and Bass Guitar')

print(f'Instrument: {mo.group()}') # Instrument: Drum
```

The phrase we searched for had both drums and bass guitar in it, and we only got drums because the | character can search for many things in the phrase, but it gives us the first one it finds.  There is another way to use this expression let's examine the example.

```python
hero = re.compile(r'(Bat|Super|Spider)man')
mo = hero.search('Spiderman made himself a webshooter')

print(f'Hero: {mo.group()}') # Hero: Spiderman
print(f'Title: {mo.group(1)}') # Hero: Spider
```

## Optional Matching with the Question Mark

In regex we use ? when we want to add expressions that are not necessarily in a pattern. Regex will freeze the expression if it finds it. If not, the code continues normally. 

```python
instrument = re.compile(r'(Bass)? Guitar')
mo1 = instrument.search('I play Guitar')
mo2 = instrument.search('I play Bass Guitar')

print(f'First Instrument: {mo1.group()}') # First Instrument: Guitar
print(f'Second Instrument: {mo2.group()}') # Second Instrument: Bass Guitar
```

## Matching Zero or More with the Star

In Regex, * (called asterisk or asterisk) gives our pattern the following meaning: if the expression in parentheses is not in the string, continue to follow the other conditions of the pattern, but if it is, no matter how many there are, fetch it and follow the other conditions of the pattern. Lets look the example

```python
instrument = re.compile(r'Drum(stick)*')
mo1 = instrument.search('I need drum')
mo2 = instrument.search('I need drumstick')
mo3 = instrument.search('I need drumstickstickstick')

print(f'First: {mo1.group()}') # First: Drum
print(f'Second: {mo2.group()}') # Second: Drumstick
print(f'Third: {mo3.group()}') # Third: Drumstickstickstick
```

## Matching One or More with the Plus

In regex, if the * character does not do anything, go ahead, if it does, take it regardless of how many there are. If the + character does not do anything, return it, if it does, take it regardless of how many there are

```python
instrument = re.compile(r'Drum(stick)+')
mo1 = instrument.search('I need drum')
mo2 = instrument.search('I need drumstick')
mo3 = instrument.search('I need drumstickstickstick')

print(f'First: {mo1.group() == None}') # First: True
print(f'Second: {mo2.group()}') # Second: Drumstick
print(f'Third: {mo3.group()}') # Third: Drumstickstickstick
```

## Matching Specific Repetitions with Braces

Just now it was taking all the * and + characters if there were many, now we will see how to limit it. It is the {} character that indicates how many or what range the first repeated expression should be in. For example `(Hello){3}` is a pattern that will work if there is a section called HelloHelloHello. It will need to repeat as many times as the number typed inside the {} brackets. We can also set an upper and lower limit if we want. `(Hello){3, 5}` This will work if the number of hello's is between 3 and 5 (including 3 and 5) we can do this without setting a lower bound `(Hello){,5}` This will return Hello statements from zero to 5

```python
HelloPattern1 = re.compile(r'(Hello){3}')
HelloPattern2 = re.compile(r'(Hello){3,5}')
HelloPattern3 = re.compile(r'(Hello){,5}')

mo1 = HelloPattern1.search('HelloHelloHello') # Thats True
mo2 = HelloPattern2.search('HelloHelloHelloHello') # Thats True
mo3 = HelloPattern3.search('HelloHello') # Thats True
```


## Greedy and Non-Greedy Matching 

In Python, regexes work greedy. This means it works greedy: for example if `(Hello){3,5}` is the expression and there are 5 hello's in the string, it will take them all. If he was non-greedy, he would get 3 hello's, so he would stop at the minimum limit. We can convert our expression from greedy to non-greedy using the ? character for example: `(Hello){3,5}?` now this expression is non-greedy, it will receive as many hello as its lower bound.

## The findall() Method

The search() expression we used in the regex retrieves the first expression in the string that satisfies the condition of the pattern, the findall() method retrieves all the expressions in the string that match the pattern. Let's analyze the example

```python
phone_num = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
mo = phone_num.seach('Main: 123-456-7890 Secondary: 234-567-8901')
mo2 = phone_num.findall('Main: 123-456-7890 Secondary: 234-567-8901')

print(mo1) # 123-456-7890
print(mo2) # [123-456-7890, 234-567-8901]
```

## Character Class

Character class is used to check if a character is from a specific set. Square brackets are defined by `[]` and match only **one character**.

## Basic Character Class

```python
[abc]
```

This expression matches any of the characters **“a, b or c ”**.

## Negative Character Class

```python
[^abc]
```

When `^` is used in square brackets, it matches any character other than these characters. Example: `[^xyz]` → matches characters other than x, y, z.

## Character Spacing

```python
[a-z] // Lowercase letters from a to z
[A-Z] // Uppercase letters from A to Z
[0-9] // Numbers from 0 to 9
[a-zA-Z] // All letters (lowercase + uppercase)
[a-z0-9] // Lowercase letters and numbers
```

A range can be defined by inserting `-` between characters.

## Predefined Character Classes

| Shorthand character class | Represents                                                                                           |
| ------------------------- | ---------------------------------------------------------------------------------------------------- |
| \d                        | Any numeric digit from 0 to 9.                                                                       |
| \D                        | Any character that is not a numeric digit from 0 to 9                                                |
| \w                        | Any letter, numeric digit, or the underscore character (Think of this as matching "word" characters) |
| \W                        | Any, character that is not a letter, numeric digit or the underscore character                       |
| \s                        | Any space, tab, or newline character. (Think of this as matching "space" character)                  |
| \S                        | Any character that is not a space, tab, or newline                                                   |

### Example 1: `[aeiou]`

Matches with a vowel.

- Matches: `a`, `e`, `i`
    
- Does not match: `b`, `z`, `1`

---
### Example 2: `[0-9][0-9]`

Captures a two-digit number. Example: `23`, `05`, `99`

---
### Example 3: `[^a-zA-Z0-9]`

Matches non-alphanumeric characters. For example: `!`, `#`, `%`, `.`