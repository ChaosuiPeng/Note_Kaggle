### re module (regular expressions) is used to perform pattern-based string substitution.

See an example:
here, we are using **capturing groups** and **backreferences** in regular expressions to identify and replace sequences of repeated characters within a string.
```python
import re

str = "aaabbbcccddddeeeeffff"

seqReplacePattern = r"\1\1"
sequencePattern = r"(.)\1\1+"
str = re.sub(sequencePattern, seqReplacePattern, str)

print(str) # Output: 'aabbccddeeff'
```

📕 📕 📕 

(.)\1\1+： This is used to identify words with consecutive repeated characters that occur more than two times. 

(.): This is the first capturing group that captures any single character.

\1: This is a backreference that refers to the character captured by the first capturing group. It is used to match the same character again.

\1\1+: This part matches one or more occurrences of the same character captured by the first capturing group. It identifies sequences of repeated characters that occur more than two times.

Some details about 'r'
```python
pattern = "\\d"  # Without 'r', double backslashes are needed to escape the backslash

pattern = r"\d"  # With 'r', backslashes are treated as literal characters
```
