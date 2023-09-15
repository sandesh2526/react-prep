# Javascript Regular Expression(Regex)

Regular expressions are used in programming languages to match parts of strings. You create patterns to help you do that matching.

## test() method usage and pattern

test() method matches the pattern and then return true if matched else false

### Pattern with /wordToBeChecked/

If you want to find the word the in the string The dog chased the cat, you could use the following regular expression: /the/. Notice that quote marks are not required within the regular expression.

```javascript
let testStr = "freeCodeCamp";
let testRegex = /Code/;
testRegex.test(testStr);    // .test() method takes the regex, applies it to a string  and returns true or false
```

### OR(|) inside /word|To|Be|Searched/

We can use the or(|) to specify one or more strings to be searched inside other string and check if anyone of them exist inside string to be checked as follows:

```javascript
let testStr = "I love my dog as it protects us from bandits"
let testRegex = '/dog|cat|hamster/'
testregex.test(testStr); // returns true as dog exists inside the string
```

### Ignore case flag /Pattern/i

We can ignore the case of pattern and mathching string by using the flag.
The flags are appended as:  /Pattern/(flag)

```javascript
let testStr = "The case should not matter for FIREExtinguiSHER";
let testRegex = '/FireExtinguisher/i'
testRegex.test(testStr) // returns true
```

## match() method

The match method helps in finding the actual matched pattern string

```javascript
"Hello, World!".match(/Hello/); // Hello
let ourStr = "Regular expressions";
let ourRegex = /expression/;
ourStr.match(ourRegex); // expression 
```

Note that the .match syntax is the "opposite" of the .test method you have been using thus far:

```javascript
'string'.match(/regex/);
/regex/.test('string');
```

### flag g

To search or extract a pattern more than once, you can use the global search flag: g.

```javascript
let repeatRegex = /Repeat/g;
testStr.match(repeatRegex);
```

### dot wildcard

The wildcard character . will match any one character. The wildcard is also called dot and period. You can use the wildcard character just like any other character in the regex. For example, if you wanted to match hug, huh, hut, and hum, you can use the regex /hu./ to match all four words.

```javascript
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr);   // true
huRegex.test(hugStr);   // true
```

### Character Classes

You can search for a literal pattern with some flexibility with character classes. Character classes allow you to define a group of characters you wish to match by placing them inside square ([ and ]) brackets.

For example, you want to match bag, big, and bug but not bog. You can create the regex /b[aiu]g/ to do this. The [aiu] is the character class that will only match the characters a, i, or u.

```javascript
let bigStr = "big";
let bagStr = "bag";
let bugStr = "bug";
let bogStr = "bog";
let bgRegex = /b[aiu]g/;
bigStr.match(bgRegex);  // big
bagStr.match(bgRegex);  // bag
bugStr.match(bgRegex);  // bug
bogStr.match(bgRegex);  // nll
```

### marching a range of characters using the '-'

Inside a character set, you can define a range of characters to match using a hyphen character: -.
For example, to match lowercase letters a through e you would use [a-e].

```javascript
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex);  // cat
batStr.match(bgRegex);  // bat
matStr.match(bgRegex);  // null
// we can also match the numbers
let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex);
/*[
  'J', 'e', 'n', 'n',
  'y', '8', '6', '7',
  '5', '3', '0', '9'
] */
```

### Negated Characters

To create a negated character set, you place a caret character (^) after the opening bracket and before the characters you do not want to match.
For example /[^aeiou]/gi matches all characters that are not a vowel

```javascript
let quoteSample = "3 blind mice.";
let myRegex = /[^0-9aeiou]/ig; 
let result = quoteSample.match(myRegex); // logs all the consonants
```

### match a grop of characters using '+'

You can use the + character to check if that is the case. Remember, the character or pattern has to be present consecutively. That is, the character has to repeat one after the other.

For example, /a+/g would find one match in abc and return ["a"]. Because of the +, it would also find a single match in aabc and return ["aa"].

If it were instead checking the string abab, it would find two matches and return ["a", "a"] because the a characters are not in a row - there is a b between them. Finally, since there is no a in the string bcd, it wouldn't find a match.

```javascript
let difficultSpelling = "Mississippi";
let myRegex = /s+/gi; // Change this line
let result = difficultSpelling.match(myRegex);  // [ ss, ss ]
```

### Match zero or more chatacters with '*'

The character to do this is the asterisk or star: *.

```javascript
let soccerWord = "gooooooooal!";
let goRegex = /go*/;    // matches zero or more 'o' characters
soccerWord.match(goRegex);  // returns 'goooooooo'
```

### Lazy Matching with '?'

In regular expressions, a greedy match finds the longest possible part of a string that fits the regex pattern and returns it as a match. The alternative is called a lazy match, which finds the smallest possible part of the string that satisfies the regex pattern.

However, you can use the ? character to change it to lazy matching. "titanic" matched against the regex of /t[a-z]*?i/ returns ["ti"].

```javascript
let text = "<h1>Winter is coming</h1>";
let myRegex = /<.*?>/; // without '?' it will return the entire string as everything can be matched with '*>'
let result = text.match(myRegex);
console.log(result[0]);    // returns the <h1>
```

### Matching the beginnings with '^'

The caret character (^) inside a character set to create a negated character set in the form '[^thingsThatWillNotBeMatched]'.
Outside of a character set, the caret is used to search for patterns at the beginning of strings.

```javascript
let firstString = "Ricky is first and can be found.";
let firstRegex = /^Ricky/;
firstRegex.test(firstString);   // true
let notFirst = "You can't find Ricky now.";
firstRegex.test(notFirst);      // false
```

### Match the endings with the '$'

You can search the end of strings using the dollar sign character $ at the end of the regex.

```javascript
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding);
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding);
```

### closet character class '\w'

The closest character class in JavaScript to match the alphabet is \w. This shortcut is equal to [A-Za-z0-9_]

```javascript
let longHand = /[A-Za-z0-9_]+/;
let shortHand = /\w+/;
let numbers = "42";
let varNames = "important_var";
longHand.test(numbers);       //true  
shortHand.test(numbers);      //true  
longHand.test(varNames);      //true  
shortHand.test(varNames);     //true  
```

You can search for the opposite of the \w with \W. \W is equal to '[^A-Za-z0-9_]'

```javascript
let shortHand = /\W/;
let numbers = "42%";
let sentence = "Coding!";
numbers.match(shortHand);   // %
sentence.match(shortHand);  // !
```

### The closet class to match all the numbers '\d'

The shortcut to look for digit characters is \d, with a lowercase d. This is equal to the character class [0-9], which looks for a single character of any number between zero and nine.

```javascript
let movieName = "2001: A Space Odyssey";
let numRegex = /[\d]/g; // Change this line
let result = movieName.match(noNumRegex).length; // 4
```

similarly the '\D' would match the non number literals

### Match the whitespaces using '\s'

You can search for whitespace using \s, which is a lowercase s. This pattern not only matches whitespace, but also carriage return, tab, form feed, and new line characters. You can think of it as similar to the character class [ \r\t\f\n\v].

```javascript
let whiteSpace = "Whitespace. Whitespace everywhere!"
let spaceRegex = /\s/g;
whiteSpace.match(spaceRegex);   // [ " ", " " ]
// We can use '\S' to match anything except whitespace
nonSpaceRegex = /\S/g;
whiteSpace.match(nonSpaceRegex);
```

### Specify Upper and Lower Number of Matches

We can specify the lower and upper number of patterns with quantity specifiers. Quantity specifiers are used with curly brackets ({ and }). You put two numbers between the curly brackets - for the lower and upper number of patterns

```javascript
let A4 = "aaaah";
let A2 = "aah";
let multipleA = /a{3,5}h/;
multipleA.test(A4); // true as the string contains 4 a's
multipleA.test(A2); // false
multipleA = /a{2,}/ // Specifies the minimum limit as the limit 
```

### Specify Exact Number of matches

If you want to specify specific number of letter matches we can use curly braces. For example, to match only the word hah with the letter 'a' 3 times, your regex would be '/ha{3}h/'.

### possible existance of letter using '?'

You can specify the possible existence of an element with a question mark, ?. This checks for zero or one of the preceding element. You can think of this symbol as saying the previous element is optional.

For example, there are slight differences in American and British English and you can use the question mark to match both spellings.

```javascript
let american = "color";
let british = "colour";
let rainbowRegex= /colo?r/;
rainbowRegex.test(american);  // true
rainbowRegex.test(british);   // true
```

### Lookaheads

Lookaheads are patterns that tell JavaScript to look-ahead in your string to check for patterns further along.
There are two kinds of lookaheads: positive lookahead and negative lookahead.

A positive lookahead will look to make sure the element in the search pattern is there, but won't actually match it. A positive lookahead is used as (?=...) where the ... is the required part that is not matched.

On the other hand, a negative lookahead will look to make sure the element in the search pattern is not there. A negative lookahead is used as (?!...) where the ... is the pattern that you do not want to be there. The rest of the pattern is returned if the negative lookahead part is not present.

```javascript
let password = "abc123";
let something = "uuuuuuuuuuuuuuuuuuuuuuuiiiiiiiiiiiiiiiiiiiioooooooooooooooo";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
let someCheck = /?=(i+)/
console.log(something.match(someCheck)); // ''
console.log(checkPass.test(password));   // true
```

### Replace the text

You can search and replace text in a string using .replace() on a string. The inputs for .replace() is first the regex pattern you want to search for. The second parameter is the string to replace the match or a function to do something.

```javascript
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
```

The replace call would return the string The sky is blue..
