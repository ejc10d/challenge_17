# Regex Tutorial - Matching an Email

This tutorial will explain the components of how to match an email using Regular Expression. In our journey to becoming a full stack devloper, we have already encountered a use-case for this type of match. When a user interacts with the front in on a form and is asked to enter their email, part of the process we have been taught to include in our code is error handling. We also want to ensure that enters a vaild email. This type of validation is completed on any professional website that is asking for user credentails. It would be advantageous for new developers to be able to not only recognize the regex at it is implemented in existing code, but also to be able to apply this regex to a new form on the job. 

## Summary

The regular expression I will be explaining is to match an email of a user to ensure that the string passed into a form handler is actually an email and not just a list of nonsense characters to clear the form requirement. 

To do this regex will be checking for a string of alphanumeric characters (maybe containing a . or a -) to be followed by the @ symbol, then a . followed by a number of web address endings like com, net, edu or .org. 

The regular expression of this will look similar to this example: 
[ \w.]+@[ \w.]+\.(com|net|edu|org)

In this example all of the following would be matched: 
<br> test@gmail.com
e.c10d@my.fsu.edu
john.smith@yahoo.net
jane_doe@ucf.org <br>

In Javascript if we set a var equal to a regular expression like var email = [ \w.]+@[ \w.]+\.(com|net|edu|org). We are then able to cross compare that what the user passes into a form element is in fact an email and not just nonsense. We can do that by using the built in test function like this: 
    function handleForm() {
    var text = emailfield.value();

    var email = [ \w.]+@[ \w.]+\.(com|net|edu|org);

    createP(email.test(text));
}

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Flags](#flags)

## Regex Components
Literal characters to meta characters. Literal characters are just the characters standing by themselves. This would be similar to a string. This matches with the literal characters that you pass through. Meta characters are used in regular expressions to allow for a number of other characters to be passed through. An example of this would be /w wich would refer to word parts. This includes alphanumeric characters. /d would refer to a digit or integer. 

### Anchors
^ would be the beginning of the line. $ would mean the end of a line. /b would be a word boundary. 


### Quantifiers
Quantifiers are a way to modify meta characters. * stands for 0 or more, + stands for 1 or more, ? stands for 0 or 1 more (think "opptionally"), curly brackets can be used in this fashion {min, max}, or to signify a specific number like this: {n}. These help us make the reular expression flexbile or restrictive enough to get the result for which we are looking. An example of this would be \w{5} to find all words that have at least five letters in it. 

For the case of searching a phone number this would be helpful because instead of writing \d\d\d-\d\d\d-\d\d\d\d, meaning 3 digits, followed by 3 digits, followed by 4 digits, we can simplify this to \d{3}-\d{3}-\d{4}. This wouldn't be necessary for the email match that I'm attempting but it is good to note. 

### OR Operator
I believe this would be in reference to the | or alternative operator so in the example [red | green] it would match red in the phrase red apple and green in the phrase green apple. 

### Character Classes
A character class is bound by square brackets [a, b, c]. This allows for us to match for the letter a, or b, or c. This is helpful if you are only looking for words and not other items on the page that might include numbers. In this case you can use \b[ A-Za-z ]{4}\b. The ^ in this case would mean NOT so [ ^abc ] would find anything that is not a, b, or c.

In the email match I created, we have to use something called alternation. This would look something like (net | com | org | edu). Where () are used to match all cases of net, com or net.

### Grouping and Capturing
When we do a search in regular expression the occurances found are given a group number. This original match for what is passed in the regex is called group number 0. We can additionally tell the query to capture different parts of the regular expression query by using ( ) within the regex to tell the query that we'd like to assign another group number (beyond 0) to that part of the regex to reference later for the replace method. This can be done by calling $1 or \1. $1 is for the replace method. \1 is used when we are referencing this part of the regex within itself. 

This would be useful when you would like to redact some inportant information out of a document. The best example would be back to the phone number example. We could find all occurances of a phone number using the regex: \(?\d{3})[-.]\d{3}[-.]\d{4} and then decide we'd like to redact the last 7 digits for each phone number. To do this we would use $1-XXX-XXXX. This would go into the ( ) in the regex, in this case it would be the area code. And replace the rest of the number with Xs with only dashes inbetween. 


### Greedy and Lazy Match
.* is the  greedy match. It will take in anything. So in the case of \[.*\] we would  be able to get a literal open bracket followed by anything else on that line. In order to change this from being so greedy we have to include a ? in the regex in this way: 
\[.*?\]

### Boundaries
/b is the regex for a word boundary. If you were to wrap a query in /b like /b/w{4}/b, your results would be only four letter words (or letter/number combinations) because it is looking for a word boundary in front of and before the four word characters (including numbers).

### Back-references
The best example of back-references is for doubling words. When using the regular expression \b(\w+)\s\1\b we are able to tell regex to match repeated words. This happens because of what we already know, boundaries and meta characters, and combinding it with grouping and capturing. Rather than using $1 for a replace we are using the \1 in this case. This is used to reference the part of the regex that we have in ( ) in this case it is the exact word part. This will only match the exact same words that occur in a row. 

### Look-ahead and Look-behind
Look-ahead takes two forms, positive and negative. Negative look-ahead would return all cases of a character followed by the next character. Both characters are included. A postive look-ahead is similar but the second character is not part of the match. A great example of this is the letter q. If we want to find all occurances of a q followed by a u we could do two things: a negative look-ahead - q(?!u) - in this case u is included in the match. Or a positive look-ahead - q(?=u) - in this case the u is NOT included in the match. 

### Flags
Flags are used in the actual use case of programing with regular expressions. If passing in regular expressions in as variables, the match will only return the first occurance of the match and will stop or exit once it can return a match.

The two flags that are helpful in programming are g and i. g stands for  global (refering to scope) and the i is for case insensitive.

Global scope will find everything that you have passed through and return all matches. i will allow all matches to include the matches regardless of the capitalization of the text with which it is attempting to match. 

These flags follow the regular expression. The return for the match is in an array so it is very helpful in a programming use. 

## Author

My name is Eliot Crandall. I am a elementary school teacher who is learning to code on the side. I would like to pursue a carreer in full stack development upon completing the UCF Full Stack Bootcamp. So far we have learned front end and back end development. I have mostly enjoyed front end but was surprized by how much value I got out of learning the back end of everything we are doing. Mysql stands out to me. If you'd like to see the projects that I've accomplished thus far, you can check out my Github profile [here](https://github.com/ejc10d)
