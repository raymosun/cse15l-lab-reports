# Week 10 Lab 5

## Bug 1

The markdown in 194.md was
```
[Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```

I found this test with different results by using `diff`.

My implementation found no links, while the provided implentation found the link "url". It looks like the actual output was supposed to have one link, "my_(url)", so it seems like both implementations got this case wrong.

For my code, I didn't consider that there was an alternate way to specify links in CommonMark. To fix this, I would have to detect when the closing bracket has a colon after, and then check for the alternate link syntax instead.

![Image](/img/w10l5/code1.png)

I would probably need to insert code checking for a colon here.

## Bug 2

The markdown in 489.md was
```
[link](foo
bar)
```

I also found this test with different results by using `diff`.

My implementation found the link "foo\nbar", while the provided implemenation found no links. The actual output should have been no links, so my implementation got this wrong and the provided implementation got it right.

The bug in my code was I didn't check if there are newlines between the parentheses.

![Image](/img/w10l5//code2.png)

I would have to add code checking for the index of a newline and "continue"-ing the loop if one is found between parentheses.

