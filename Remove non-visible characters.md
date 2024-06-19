# Remove non-visible characters/Weird string behavior

```
using System;
using System.Text.RegularExpressions;

string input = "Hello\u200B World\u200C!"; // Example string with non-visible characters

string result = Regex.Replace(input, @"\p{C}+", ""); // Remove non-visible characters

Console.WriteLine(result); // Output: Hello World!
```
