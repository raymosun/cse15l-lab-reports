# Week 8 Lab 4 - Debugging

[My Repo](https://github.com/sunouray/markdown-parse)

[Reviewed Repo](https://github.com/leo3friedman/markdown-parse)

## Snippet 1
```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```

According to the CommonMark demo site, this snippet has the links "`google.com", "google.com", and "ucsd.edu".

The snippet was turned into a test for my implementation:

![Image](/img/w8l4/test1.png)

and the other code implementation:

![Image](/img/w8l4/test1other.png)

For my implementation, it failed as shown:

![Image](/img/w8l4/failme1.png)

For the implementation I reviewed, it failed as shown:

![Image](/img/w8l4/failother1.png)

The problem of backticks would probably require a more involved solution. You would have to find the index of backticks as you parse the text and also keep track of whether or not you are currently in backticks, from the whole file.

## Snippet 2

According to the CommonMark demo site, this snippet has the links "a.com", "a.com(())", and "example.com".

The snippet was turned into a test for my implementation:

![Image](/img/w8l4/test2me.png)

and the other code implementation:

![Image](/img/w8l4/test2other.png)

For my implementation, it failed as shown:

![Image](/img/w8l4/failme2.png)

For the implementation I reviewed, it failed as shown:

![Image](/img/w8l4/failother2.png)

I think the problem of nested parentheses would also require a more involved solution. You would probably need to track nested parentheses using a stack like Joe did.

## Snippet 3
```
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
    https://ucsd-cse15l-w22.github.io/
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```

According to the CommonMark demo site, this snippet only has the link "https://ucsd-cse15l-w22.github.io/".

The snippet was turned into a test for my implementation:

![Image](/img/w8l4/test3me.png)

and the other code implementation:

![Image](/img/w8l4/test3other.png)

For my implementation, it failed as shown:

![Image](/img/w8l4/failme3.png)

For the implementation I reviewed, it failed as shown:

![Image](/img/w8l4/failother3.png)

I think my program could be made to handle newlines in brackets and parentheses with a small code change. You would just have to parse whitespace my carefully and remove newlines and spaces inside parentheses but outside links.