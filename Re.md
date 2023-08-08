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

📕 ‘(.)\1\1+’ is used to identify words with consecutive repeated characters that occur more than two times. 
