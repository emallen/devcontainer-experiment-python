# Test the linter

## MD009

This is a paragraph that uses the bad way of
having a hard line break.
It also has spaces at the end of the last line, which is a violation of
strict.

This paragraph uses the allowed \
mechanism for a hard line break.

## MD027

>  1. one
>  2. two
>  3. three
>  4. four
>  5. five
>  6. six
>  7. seven
>  8. eight
>  9. nine
> 10. ten

## MD029

First:

<!-- Test an error for one repeating (required config) -->
1. Narf
1. Poit
1. Egad

Next:

0. rule zero
1. Rule one
2. Rule two

Third:

<!-- Test an error for zero repeating -->
0. Apple
0. Berry
0. Cherry

Fourth:

<!-- markdownlint-capture -->
<!-- markdownlint-disable MD029 -->
42. The answer

    <!-- markdownlint-disable -->
    my friend is blowing in the wind.
    <!-- markdownlint-restore -->
<!-- markdownlint-disable MD029 -->
43. Unknown
<!-- markdownlint-restore -->
<!-- Test error next line because of restoring the state -->
44. Hello

## MD033

<!-- markdownlint-disable-next-line MD060 -->
| a  | b  |
| :- | :- |
| x | y |
| z | q<br/>r |
| s | t |

## MD035

This

---
That

## MD046

```Python
print 'this is valid code'

print 'yay'
```

<!-- Test an error for indented code blocks -->
    print 'this is invalid code'

    print 'boo'

## MD048

<!-- Test an error for tildes -->
~~~Python
print 'invalid code fence'
~~~

````Python
print 'More than 3 backticks rmmain valid'
````

## MD049

_Emphasis_ begins this paragraph.

<!-- Test an error for single asterisks on whole words -->
*Wrong* emphasis is flagged.

However, internal asterisks are required: Anti*dis*establishment
to avoid snake_case_confusion.

## MD050

**Strong Emphhasis** begins this paragraph.

<!-- Test an error for double-underscores -->
__Wrong__ strong emphasis is flagged.

As before, internal double-asterisks happen regardless of the seting:
lin**gui**stics.

## MD052

- [x] alpha
- [ ] beta
- [X] gamma

<!-- Test an error for unescaped square brackets areound a word. -->
Word in [brackets] should require escaping the brackets
like \[so\].

## MD053

<!-- Test an error for the default-permitted pseudo-comment -->
[//]: # (This behaves like a comment)

## MD054

[amazing site][link-target]

[link-target][]

<!-- Test an error for the shortcut syntax -->
[link-target]

[link-target]: http://example.com

<!-- Test an error for the inlined item -->
[http://example.com/inlined](http://example.com/inlined) should be
<http://example.com/inlined>,
but [http://example.com/outlined](http://example.com/inlined) evil spoofing
like the prior gets allowed because it's not able to be stopped.

## MD055

| Col 1 | Col 2 |
| :---- | :---- |
| foo | bar |

<!-- Test an error for missing pipes -->
Col 1 | Col 2
:---- | :----
foo | bar

<!-- Test an error for laeading pipes -->
| Col 1 | Col 2
| :---- | :----
| foo   | bar

<!-- Test an error for trailinging pipes -->
Col 1 | Col 2 |
:---- | :---- |
foo | bar |

## MD056

| Col 1 | Col 2 |
| :---- | :---- |
| foo | bar |
| baz | |
| fred | waldo |

## MD057

<!-- Test an error for no blank line before table -->
Amazing table
| Col 1 | Col 2 |
| :---- | :---- |
| foo | bar |

<!-- Test an error for no blank line after table -->
| Col 1 | Col 2 |
| :---- | :---- |
| foo | bar |
> Note the line after the table needs to be nonvanilla, like a blockquote.

## MD060

| x= | y= |
| -: | :- |
| 1 | 2 |

<!-- Test an error for aligned -->
| x= | y= |
| -: | :- |
| 1  | 2  |

<!-- Test an error for tight -->
|x=|y=|
|-:|:-|
|1|2|
