---
title: 
alias: 

tags:
date created: Wednesday, November 24th 2021, 11:06:28 pm
date modified: Thursday, December 23rd 2021, 5:27:03 am
---

# ) AWK

## Summary

AWK (awk) is a domain-specific language designed for text processing and typically used as a data extraction and reporting tool. Like [[sed]] and [[grep]], it's a filter, and is a standard feature of most [[Unix]]-like operating systems.

The AWK language is a data-driven scripting language consisting of a set of actions to be taken against streams of textual data – either run directly on files or used as part of a pipeline – for purposes of extracting or transforming text, such as producing formatted reports. The language extensively uses the string datatype, associative arrays (that is, arrays indexed by key strings), and regular expressions. While AWK has a limited intended application domain and was especially designed to support one-liner programs, the language is Turing-complete, and even the early Bell Labs users of AWK often wrote well-structured large AWK programs.

AWK was created at Bell Labs in the 1970's, and its name is derived from the surnames of its authors: Alfred Aho, Peter Weinberger, and Brian Kernighan. The acronym is pronounced the same as the bird auk, which is on the cover of The AWK Programming Language.

> When written in all lowercase letters, as awk, it refers to the Unix or Plan 9 program that runs scripts written in the AWK programming language.

## Wiki

### Notes

[AWK - Wikipedia](https://en.wikipedia.org/wiki/AWK) [[January 16th, 2021]] 23:09 | Link Highlight Article

In addition to normal arithmetic and logical operators, AWK expressions include the tilde operator, `~`, which matches a [regular expression](https://en.wikipedia.org/wiki/Regular_expression) against a string. As handy [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar), /regexp/ without using the tilde operator matches against the current record; this syntax derives from [sed](https://en.wikipedia.org/wiki/Sed), which in turn inherited it from the [ed](https://en.wikipedia.org/wiki/Ed_(text_editor)) editor, where `/` is used for searching…

### Commands

AWK commands are the statements that are substituted for action in the examples above. AWK commands can include function calls, variable assignments, calculations, or any combination thereof. AWK contains built-in support for many functions; many more are provided by the various flavors of AWK. Also, some flavors support the inclusion of [dynamically linked libraries](https://en.wikipedia.org/wiki/Dynamically_linked_library), which can also provide more functions.

#### The Print Command

The print command is used to output text. The output text is always terminated with a predefined string called the output record separator (ORS) whose default value is a newline. The simplest form of this command is:

```print```

This displays the contents of the current record. In AWK, records are broken down into fields, and these can be displayed separately:

```print $1```

Displays the first field of the current record

```print $1, $3```

Displays the first and third fields of the current record, separated by a predefined string called the output field separator (OFS) whose default value is a single space character

Although these fields ($X) may bear resemblance to variables (the $ symbol indicates variables in [Perl](https://en.wikipedia.org/wiki/Perl)), they actually refer to the fields of the current record. A special case, $0, refers to the entire record. In fact, the commands "```print```" and "```print $0```" are identical in functionality.

The print command can also display the results of calculations and/or function calls:

Output may be sent to a file:

or through a [pipe](https://en.wikipedia.org/wiki/Pipe_(Unix))

### Built-in Variables

Awk's built-in variables include the field variables: $1, $2, $3, and so on ($0 represents the entire record). They hold the text or values in the individual text-fields in a record.

#### Other Variables Include:

```NR```: 'N'umber of 'R'ecords: keeps a current count of the number of input records read so far from all data files. It starts at zero, but is never automatically reset to zero.[(14)](https://en.wikipedia.org/wiki/AWK#cite_note-GNU.org_Records-14)

```FNR```: 'F'ile 'N'umber of 'R'ecords: keeps a current count of the number of input records read so far in the current file. This variable is automatically reset to zero each time a new file is started.[(14)](https://en.wikipedia.org/wiki/AWK#cite_note-GNU.org_Records-14)

```NF```: 'N'umber of 'F'ields: contains the number of fields in the current input record. The last field in the input record can be designated by $NF, the 2nd-to-last field by $(NF-1), the 3rd-to-last field by $(NF-2), etc.

```FILENAME```: Contains the name of the current input-file.

```FS```: 'F'ield 'S'eparator: contains the "field separator" character used to divide fields in the input record. The default, "white space", includes any space and tab characters. FS can be reassigned to another character to change the field separator.

```RS```: 'R'ecord 'S'eparator: stores the current "record separator" character. Since, by default, an input line is the input record, the default record separator character is a "newline".

```OFS```: 'O'utput 'F'ield 'S'eparator: stores the "output field separator", which separates the fields when Awk prints them. The default is a "space" character.

```ORS```: 'O'utput 'R'ecord 'S'eparator: stores the "output record separator", which separates the output records when Awk prints them. The default is a "newline" character.

```OFMT```: 'O'utput 'F'or'M'a'T': stores the format for numeric output. The default format is "%.6g".

### Variables and Syntax

Variable names can use any of the characters [A-Za-z0-9_], with the exception of language keywords. The operators + - * / represent addition, subtraction, multiplication, and division, respectively. For string [concatenation](https://en.wikipedia.org/wiki/Concatenation), simply place two variables (or string constants) next to each other. It is optional to use a space in between if string constants are involved, but two variable names placed adjacent to each other require a space in between. Double quotes [delimit](https://en.wikipedia.org/wiki/Delimit) string constants. Statements need not end with semicolons. Finally, comments can be added to programs by using `#` as the first character on a line.

### User-defined Functions

In a format similar to [C](https://en.wikipedia.org/wiki/C_(programming_language)), function definitions consist of the keyword `function`

This statement can be invoked as follows:

Functions can have variables that are in the local scope. The names of these are added to the end of the argument list, though values for these should be omitted when calling the function. It is convention to add some [whitespace](https://en.wikipedia.org/wiki/Whitespace_character) in the argument list before the local variables, to indicate where the parameters end and the local variables begin.

## Examples

### Hello World

Here is the customary "[Hello, world](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program)" program written in AWK:

```AWK
BEGIN

{

print

"Hello, world!"

}
```

Note that an explicit `exit` statement is not needed here; since the only pattern is `BEGIN`, no command-line arguments are processed.

### Print Lines Longer Than 80 Characters
- Print all lines longer than 80 characters. Note that the default action is to print the current line.

```AWK
length

($0)

>

80
```

### Count Words

Count words in the input and print the number of lines, words, and characters (like [wc](https://en.wikipedia.org/wiki/Wc_(Unix))):

```AWK
{

words

+=

NF

chars

+=

length

+

1
```

`#` add one to account for the newline character at the end of each record (line)

```AWK
}

END

{

print

NR

,

words

,

chars

}
```

As there is no pattern for the first line of the program, every line of input matches by default, so the increment actions are executed for every line. Note that `words += NF` is shorthand for `words = words + NF`.

Sum last word

```AWK
{

s

+=

$

NF

}

END

{

print

s

+

0

}
```

s is incremented by the numeric value of $NF, which is the last word on the line as defined by AWK's field separator (by default, white-space). NF is the number of fields in the current line, e.g. 4. Since $4 is the value of the fourth field, $NF is the value of the last field in the line regardless of how many fields this line has, or whether it has more or fewer fields than surrounding lines. $ is actually a unary operator with the highest [operator precedence](https://en.wikipedia.org/wiki/Operator_precedence). (If the line has no fields, then NF is 0, $0 is the whole line, which in this case is empty apart from possible white-space, and so has the numeric value 0.)

At the end of the input the END pattern matches, so s is printed. However, since there may have been no lines of input at all, in which case no value has ever been assigned to s, it will by default be an empty string. Adding zero to a variable is an AWK idiom for coercing it from a string to a numeric value. (Concatenating an empty string is to coerce from a number to a string, e.g. s "". Note, there's no operator to concatenate strings, they're just placed adjacently.) With the coercion the program prints "0" on an empty input, without it an empty line is printed.

### Match a Range of Input Lines

```AWK
NR

%

4

==

1

,

NR

%

4

==

3

{

printf

"%6d %s\n"

,

NR

,

$

0

}
```

- The action statement prints each line numbered. The printf function emulates the standard C [printf](https://en.wikipedia.org/wiki/Printf) and works similarly to the print command described above. The pattern to match, however, works as follows: NR is the number of records, typically lines of input, AWK has so far read, i.e. the current line number, starting at 1 for the first line of input. % is the [modulo](https://en.wikipedia.org/wiki/Modulo_operation) operator. NR % 4 == 1 is true for the 1st, 5th, 9th, etc., lines of input. Likewise, NR % 4 == 3 is true for the 3rd, 7th, 11th, etc., lines of input. The range pattern is false until the first part matches, on line 1, and then remains true up to and including when the second part matches, on line 3. It then stays false until the first part matches again on line 5.

- Thus, the program prints lines 1,2,3, skips line 4, and then 5,6,7, and so on. For each line, it prints the line number (on a 6 character-wide field) and then the line contents. For example, when executed on this input:

		Rome Florence Milan Naples Turin Venice...

The previous program prints:

	1 Rome 2 Florence 3 Milan 5 Turin 6 Venice...

Printing the initial or the final part of a file

As a special case, when the first part of a range pattern is constantly true, e.g. 1, the range will start at the beginning of the input. Similarly, if the second part is constantly false, e.g. 0, the range will continue until the end of input. For example,

```AWK
/^--cut here--$/

,

0
```

prints lines of input from the first line matching the regular expression ^--cut here--$, that is, a line containing only the phrase "--cut here--", to the end.

### Calculate Word Frequencies

[Word frequency](https://en.wikipedia.org/wiki/Word_frequency) using [associative arrays](https://en.wikipedia.org/wiki/Associative_array):

```AWK
BEGIN

{

FS

=

"[^a-zA-Z]+"

}

{

for

(

i

=

1

;

i

<=

NF

;

i

++

)

words

[

tolower

(

$

i

)

++

}

END

{

for

(

i

in

words

)

print

i

,

words

[

i

]

}
```

- The BEGIN block sets the field separator to any sequence of non-alphabetic characters. Note that separators can be regular expressions. After that, we get to a bare action, which performs the action on every input line. In this case, for every field on the line, we add one to the number of times that word, first converted to lowercase, appears. Finally, in the END block, we print the words with their frequencies. The line…

### …for (i in words)

Creates a loop that goes through the array words, setting i to each subscript of the array. This is different from most languages, where such a loop goes through each value in the array. The loop thus prints out each word followed by its frequency count. `tolower` was an addition to the One True awk (see below) made after the book was published.

### Match Pattern From Command Line

This program can be represented in several ways. The first one uses the [Bourne shell](https://en.wikipedia.org/wiki/Bourne_shell) to make a shell script that does everything. It is the shortest of these methods:

```
'#'!/bin/sh

pattern

=

"

$1

"

shift

...awk...

'/'

"

$pattern

"

'/ { print FILENAME ":" $0 }'

"

$@

"
```

- The `$pattern` in the awk command is not protected by single quotes so that the shell does expand the variable but it needs to be put in double quotes to properly handle patterns containing spaces. A pattern by itself in the usual way checks to see if the whole line (`$0`) matches. `FILENAME` contains the current filename. awk has no explicit concatenation operator; two adjacent strings concatenate them. $0` expands to the original unchanged input line.

- There are alternate ways of writing this. This shell script accesses the environment directly from within awk:

```AWK
`#`!/bin/sh

export

pattern

=

"

$1

"

shift

...awk...

'$0 ~ ENVIRON["pattern"] { print FILENAME ":" $0 }'

"

$@

"
```

- This is a shell script that uses ```ENVIRON```, an array introduced in a newer version of the One True awk after the book was published. The subscript of ```ENVIRON``` is the name of an environment variable; its result is the variable's value. This is like the [getenv](https://en.wikipedia.org/wiki/Getenv) function in various standard libraries and [POSIX](https://en.wikipedia.org/wiki/POSIX). The shell script makes an environment variable ```pattern``` containing the first argument, then drops that argument and has awk look for the pattern in each file.

`~` checks to see if its left operand matches its right operand; `!~` is its inverse. Note that a regular expression is just a string and can be stored in variables.

The next way uses command-line variable assignment, in which an argument to awk can be seen as an assignment to a variable:

```
`#`!/bin/sh

pattern

=

"

$1

"

shift

...awk...

'$0 ~ pattern { print FILENAME ":" $0 }'

"pattern=

$pattern

"

"

$@

"
```

Or You can use the -v var=value command line option (e.g. awk -v pattern="$pattern" …).

Finally, this is written in pure awk, without help from a shell or without the need to know too much about the implementation of the awk script (as the variable assignment on command line one does), but is a bit lengthy:

```
BEGIN

{

pattern

=

ARGV

[

1

]

for

(

i

=

1

;

i

<

ARGC

;

i

++

)

`#` remove first argument

ARGV

[

i

]

=

ARGV

[

i

+

1

]

ARGC

--

if

(

ARGC

==

1

)

{

`#` the pattern was the only thing, so force read from standard input (used by book)

ARGC

=

2

ARGV

[

1

]

=

"-"

}

}

$

0

~

pattern

{

print

FILENAME

":"

$

0

}
```

The ```BEGIN``` is necessary not only to extract the first argument, but also to prevent it from being interpreted as a filename after the ```BEGIN``` block ends. ```ARGC```, the number of arguments, is always guaranteed to be ≥1, as ```ARGV[0]``` is the name of the command that executed the script, most often the string ```"awk"```. Also note that ```ARGV[ARGC]``` is the empty string, ```""```. ```_``` initiates a comment that expands to the end of the line.

Note the ```if``` block. awk only checks to see if it should read from standard input before it runs the command. This means that…

### …awk 'prog'

only works because the fact that there are no filenames is only checked before `prog` is run! If you explicitly set `ARGC` to 1 so that there are no arguments, awk will simply quit because it feels there are no more input files. Therefore, you need to explicitly say to read from standard input with the special filename ```-```.

### Self-contained AWK Scripts

On Unix-like operating systems self-contained AWK scripts can be constructed using the [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) syntax.

For example, a script that prints the content of a given file may be built by creating a file named `print.awk` with the following content:

```
`#`!/usr/bin/awk -f

{

print

$

0

}
```

It can be invoked with: `./print.awk <filename>`

The `-f` tells AWK that the argument that follows is the file to read the AWK program from, which is the same flag that is used in sed. Since they are often used for one-liners, both these programs default to executing a program given as a command-line argument, rather than a separate file.

## Versions and Implementations

AWK was originally written in 1977 and distributed with [Version 7 Unix](https://en.wikipedia.org/wiki/Version_7_Unix).

In 1985 its authors started expanding the language, most significantly by adding user-defined functions. The language is described in the book [The AWK Programming Language](https://en.wikipedia.org/wiki/The_AWK_Programming_Language), published 1988, and its implementation was made available in releases of [UNIX System V](https://en.wikipedia.org/wiki/UNIX_System_V). To avoid confusion with the incompatible older version, this version was sometimes called "new awk" or nawk. This implementation was released under a [free software license](https://en.wikipedia.org/wiki/Free_software_license) in 1996 and is still maintained by Brian Kernighan (see external links below).[

***

Old versions of Unix, such as [UNIX/32V](https://en.wikipedia.org/wiki/UNIX/32V), included `awkcc`, which converted AWK to C. Kernighan wrote a program to turn awk into C++; its state is not known.[(15)](https://en.wikipedia.org/wiki/AWK#cite_note-15)

**BWK awk**, also known as **nawk**, refers to the version by [Brian Kernighan](https://en.wikipedia.org/wiki/Brian_Kernighan). It has been dubbed the "One True AWK" because of the use of the term in association with the book that originally described the language and the fact that Kernighan was one of the original authors of AWK.[(7)](https://en.wikipedia.org/wiki/AWK#cite_note-AWK1-7) FreeBSD refers to this version as one-true-awk.[(16)](https://en.wikipedia.org/wiki/AWK#cite_note-16) This version also has features not in the book, such as `tolower` and `ENVIRON` that are explained above; see the FIXES file in the source archive for details.
- This version is used by, for example,
	- [Android](https://en.wikipedia.org/wiki/Android_(operating_system)),
	- [FreeBSD](https://en.wikipedia.org/wiki/FreeBSD),
	- [NetBSD](https://en.wikipedia.org/wiki/NetBSD),
	- [OpenBSD](https://en.wikipedia.org/wiki/OpenBSD),
	- [macOS](https://en.wikipedia.org/wiki/MacOS), and
	- [illumos](https://en.wikipedia.org/wiki/Illumos).
	- *Brian Kernighan and Arnold Robbins are the main contributors to a source repository for nawk:* [Page not found · GitHub · GitHub](https://www.github.com/onetrueawk/awk.)

***

**gawk** ([GNU](https://en.wikipedia.org/wiki/GNU) awk) is another free-software implementation and the only implementation that makes serious progress implementing [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization) and TCP/IP networking. It was written before the original implementation became freely available. It includes its own debugger, and its [profiler](https://en.wikipedia.org/wiki/Profiling_(computer_programming)) enables the user to make measured performance enhancements to a script. It also enables the user to extend functionality with shared libraries. Some [Linux distributions](https://en.wikipedia.org/wiki/Linux_distribution) include gawk as their default AWK implementation.[

**gawk-csv**. The [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) extension of gawk provides facilities for handling input and output CSV formatted data.[(17)](https://en.wikipedia.org/wiki/AWK#cite_note-17)

**mawk** is a very fast AWK implementation by Mike Brennan based on a [bytecode](https://en.wikipedia.org/wiki/Bytecode) interpreter.

**libmawk** is a fork of mawk, allowing applications to embed multiple parallel instances of awk interpreters.

**awka** (whose front end is written atop the mawk program) is another translator of AWK scripts into C code. When compiled, statically including the author's libawka.a, the resulting executables are considerably sped up and, according to the author's tests, compare very well with other versions of AWK, [Perl](https://en.wikipedia.org/wiki/Perl), or [Tcl](https://en.wikipedia.org/wiki/Tcl). Small scripts will turn into programs of 160–170 kB.

**tawk** (Thompson AWK) is an AWK [compiler](https://en.wikipedia.org/wiki/Compiler) for [Solaris](https://en.wikipedia.org/wiki/Solaris_(operating_system)), [DOS](https://en.wikipedia.org/wiki/DOS), [OS/2](https://en.wikipedia.org/wiki/OS/2), and [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows), previously sold by Thompson Automation Software (which has ceased its activities).[(18)](https://en.wikipedia.org/wiki/AWK#cite_note-18)

***

**Jawk** is a project to implement AWK in [Java](https://en.wikipedia.org/wiki/Java_(programming_language)), hosted on SourceForge.[(19)](https://en.wikipedia.org/wiki/AWK#cite_note-19) Extensions to the language are added to provide access to Java features within AWK scripts (i.e., Java threads, sockets, collections, etc.).

**xgawk** is a fork of gawk[(20)](https://en.wikipedia.org/wiki/AWK#cite_note-20) that extends gawk with dynamically loadable libraries. The XMLgawk extension was integrated into the official GNU Awk release 4.1.0.

**QSEAWK** is an embedded AWK interpreter implementation included in the QSE library that provides embedding [application programming interface](https://en.wikipedia.org/wiki/Application_programming_interface) (API) for [C](https://en.wikipedia.org/wiki/C_(programming_language)) and [C++](https://en.wikipedia.org/wiki/C%2B%2B).[(21)](https://en.wikipedia.org/wiki/AWK#cite_note-21)

**libfawk** is a very small, function-only, reentrant, embeddable interpreter written in C

[BusyBox](https://en.wikipedia.org/wiki/BusyBox) includes an AWK implementation written by Dmitry Zakharov. This is a very small implementation suitable for embedded systems.

***

### Books

Title | Link |  [ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier)) | Retrieved… | Author | Date Published

:------- | ------- | ------- | ------- | -------| -------:
__ | [Aho, Alfred V.](https://en.wikipedia.org/wiki/Alfred_Aho) | | | Aho, Alfred V. | |
__ | [Kernighan, Brian W.](https://en.wikipedia.org/wiki/Brian_Kernighan) | | | Kernighan, Brian W. | |
__ | [Weinberger, Peter J.](https://en.wikipedia.org/wiki/Peter_J._Weinberger) | | | Weinberger, Peter J. | 1988-01-01

The AWK Programming Language | New York, NY: [Addison-Wesley](https://en.wikipedia.org/wiki/Addison-Wesley). | 0-201-07981-X | 2017-01-22 | Robbins, Arnold | 2001-05-15

Effective awk Programming (3rd ed.) | Sebastopol, CA: [O'Reilly Media](https://en.wikipedia.org/wiki/O%27Reilly_Media) | 0-596-00070-7 | 2009-04-16 | | |

__ | [Dougherty, Dale](https://en.wikipedia.org/wiki/Dale_Dougherty) | | | Dougherty, Dale & Robbins, Arnold | 1997-03-01

sed & awk (2nd ed.) | Sebastopol, CA: [O'Reilly Media](https://en.wikipedia.org/wiki/O%27Reilly_Media) | 1-56592-225-5 | 2009-04-16 | Robbins, Arnold | 2000

Effective Awk Programming: A User's Guide for Gnu Awk (1.0.3 ed.). | Bloomington, IN: [iUniverse](https://en.wikipedia.org/wiki/IUniverse). [Archived](https://web.archive.org/web/20090412190359/https://www.gnu.org/software/gawk/manual/) from the original on 12 April 2009 | 0-595-10034-1 | 2009-04-16

# See Also

## [[Wikipedia]]

- [Data transformation](https://en.wikipedia.org/wiki/Data_transformation)
- [Event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming)
- [List of Unix commands](https://en.wikipedia.org/wiki/List_of_Unix_commands)
- [sed](https://en.wikipedia.org/wiki/Sed)

## Others

- [awk(1): pattern scanning/processing - Linux man page](https://linux.die.net/man/1/awk)
- [awk(1p) - Linux manual page](https://man7.org/linux/man-pages/man1/awk.1p.html)
- [Awk Tutorial - Tutorialspoint](https://www.tutorialspoint.com/awk/index.htm)
- [A practical guide to learning awk | Opensource.com](https://opensource.com/article/20/9/awk-ebook)
- [Awk - A Tutorial and Introduction - by Bruce Barnett](https://www.grymoire.com/Unix/Awk.html)
- [📍 AWK Wiki Notes 🏧 🔗 AWK - Wikipedia 📡](https://en.wikipedia.org/wiki/AWK)
- [AWK command in Unix/Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
- [The GNU Awk User’s Guide](https://www.gnu.org/software/gawk/manual/gawk.html)
