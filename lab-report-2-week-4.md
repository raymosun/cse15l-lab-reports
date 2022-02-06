# Week 4 Lab 2

## Change 1
![Image](/img/w4l2/fix1.png)
Breaking test case [(link)](https://github.com/sunouray/markdown-parse/commit/989bfc8ea469e8a27c13aa8ad90283eb17630f42)


```
# Title 2

[a link!](https://ucsd-cse15l-w22.github.io/week/week3/)

some words [are] here (special words

[a second link!](https://www.google.com/)
```

Symptom: wrong output
```
PS C:\Users\sunra\Documents\GitHub\markdown-parse> java MarkdownParse test-file2.md
[https://ucsd-cse15l-w22.github.io/week/week3/, special words

[a second link!](https://www.google.com/]
```

The **failure-inducing input** had an incomplete set of the symbols `[]()`. Since the code had a **bug** where it did not recognize imcomplete sets of symbols and ignore them, it treated the incomplete symbols as a valid link, and continued copying text as a "link" until it reached the `)` of an entirely different link (the **symptom**).

## Change 2
![Image](/img/w4l2/fix2.png)
Breaking test case [(link)](https://github.com/sunouray/markdown-parse/commit/3779cb20067c3cd29c9b894a92c378a891213c9a)

```
[https://ucsd-cse15l-w22.github.io/week/week3/](https://ucsd-cse15l-w22.github.io/week/week3/)
[sdfsdf](sdfgsdfgsdg)
[](sdfsdfsdfsdf)
//sdfgsdfgsdfgsdfgdfg
```

Symptom: infinite loop
```
PS C:\Users\sunra\Documents\GitHub\markdown-parse> java .\MarkdownParse.class test-file3.md
Error: Could not find or load main class .\MarkdownParse.class
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
        at java.base/java.lang.StringLatin1.newString(StringLatin1.java:769)
        at java.base/java.lang.String.substring(String.java:2709)
        at MarkdownParse.getLinks(MarkdownParse.java:26)
        at MarkdownParse.main(MarkdownParse.java:34)
```

The code had a **bug** where it would not exit its while loop unless it finished a link at the last character of the file. Since the **failure-inducing input** had additional text after its last link, the **symptom** was that Java entered an infinite loop.

## Change 3
![Image](/img/w4l2/fix3.png)
Breaking test case [(link)](https://github.com/sunouray/markdown-parse/commit/e5e2663db1f77ad5468a343c546423d80b1f99e8)

```
[some stuff](stuff) 

[some stuff] (link)
```

Symptom: incorrect output
```
PS C:\Users\sunra\Documents\GitHub\markdown-parse> java MarkdownParse test-file4.md
[stuff, link]
```

Since the **failure-inducing input** file had a space between `[]` and `()` symbols, that section of the text is not actually a link. Since the code had a **bug** where it didn't require that no characters be between the `[]` and `()`, the **symptom** was the program included the false link anyway.