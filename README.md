# RegEx Cheatsheet - Regular Expressions in JavaScript

<b>Regex (Regular Expressions)</b> are a way to search through a string of text in an advanced way

https://regexr.com/ for practice and reference

https://youtu.be/rhzKDrUiJVk to follow along
## Format 
starts with `/` ends with `/` everything contained within this is the regEx
### Counting and Special Character Selectors
- `e+` search for multiple strings of `e` i.e. `ee` or `eee` etc.
- `e+a?` search for multiple strings of `e` and optionally search for `a`
- `re*` search for multiple strings of `r` and optionally search for zero or more `e`'s
- `/.at/` or `.` matches anything i.e. `fat` `cat` and `eat`, but will not match a new line
- use `\` to "escape" special characters `\@`
- `\w` to match any word character
- `\W` to match any non-word character
- `\s` to match any form of white space
- `\S` to match any form of non-white space
- `\w{4}` matches any word that is `{4}`characters
- `\w{4,}` matches any word that is `{4}` or more characters
- `\w{4,5}` matches any word that is `{4,}` to `{5}`characters
### Range Selectors
- `/[fc]at/` any three letter `at` word that starts with `f` or `c` i.e. `fat` or `cat`
- `/[a-z]at/` starts with any letter in the <b>range</b> of `a` to `z` and ends with `at` i.e. `fat` `cat` and `eat`
  - `[a-z]`
  - `[A-Z]`
  - `[0-9]`
  - `[a-f]` 
### Capture Group Selectors
- `\(t|T)he\g` match `the` or `The` 
- `\(t|e|r){2,3}\.\g` matches between 2 to 3 of the characters `t` `e` or `r` then a `.`
- `/^The/` matches the beginning of the line only
- `/.\$/` match the end of our statement
### Look-aheads and Look-behinds
- `/(?<=[tT]he)./g` positive look-behind, returns the characters behind `the` or `The`, but doesn't actually capture the character
- `/(?<T[tT]he)./g` negative look-behind, returns <b>everything</b> that doesn't follow behind `the` or `The`
- `/(?=at)./g` positive look-ahead, returns anything that has an `at` after it
- `/(?!at)./g` look-ahead, returns anything that doesn't have an `at` after it
### Flags
after the end `/` you can add flags
- `/g` or global allows you to match anywhere in the string(multiple matches vs first match)
- `/i` case insensitive 
- `/m` multiline
##
````
const reg = /e+/g
const sentence = 
"The fat cat ran down the street.  
It was searching for a mouse to eat."

reg.test(sentence)
````
## Phone Number Example
````
let isPhoneNumber = /\d{10}/g
let phoneNumber = 1234567890
isPhoneNumber.test(phoneNumber)

isPhoneNumber = /\d{3}-?\d{3}-?\d{4}/g
phoneNumber = "123-456-7890"
isPhoneNumber.test(phoneNumber)

isPhoneNumber = /\d{3}[ -]?\d{3}[ -]?\d{4}/g
phoneNumber = "123 456 7890"
isPhoneNumber.test(phoneNumber)
````
Captures digits of phone number
````
/(\d{3})[ -]?(\d{3})[ -]?\(d{4})/gm
````
Returns group 1,2, and 3
````
$1$2$3
````
change group 1's name to areacode
````
/(?<areacode>\d{3})[ -]?(\d{3})[ -]?\(d{4})/gm
````
````
phoneNumber = "(123) 456-7890"
/\?(?<areacode>\d{3}\)?[ -]?(\d{3})[ -]?\(d{4})/gm
````
````
phoneNumber = "+ 1 123 456-7890"
/((\+1)[ -])?\?(?<areacode>\d{3}\)?[ -]?(\d{3})[ -]?\(d{4})/gm
````


## Email Example
````
const emailRegex = /\S+@\S+\.\S+/
const validEmail = "valid@gmail.com"
const fauxEmail = "invalid,con"
emailRegex.test(validEmail)
emailRegex.test(fauxEmail)
````
## Credit Card Example
````
// const creditCardRegex = //g
const validCreditCard = "1234 5678 9101 1123"
const fauxCreditCard = "abcd 0000 fake 1111 card 2222"
// emailRegex.test(validEmail)
// emailRegex.test(fauxEmail)
````

## Currency Example
> Implement a function that will determine if a string represents a valid currency amount Such strings will have the following properties: 
>> The amount must consist of base-10 digits 
>> The amount may optionally contain thousands separators using the ',' character. 
>> If thousands separators are present, they must be present at each thousands increment.
>> The amount must be prefixed by the currency symbol. We support US Dollars ($), Euros (€), and Japanese Yen (¥) only. 
>> Negative amounts may be indicated either by a negative sign before the currency symbol or by enclosing the amount (including currency symbol) in parentheses, such as ($450) 
>> Dollar and Euro amounts may contain an amount of cents, represented to exactly two digits of precision. 
>> If a decimal point is present, the cents must be specified 
>> Yen amounts may not contain decimal points * Amounts may not contain a leading zero, unless it is zero Dollars or Euros and cents are specified 
>> Any other characters, including leading or trailing whitespace, is invalid 
    

