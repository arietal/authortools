# authortools
LaTeX tools for authors

# This package provides useful tools for authors such as

1. TODO list management - done
2. Author notes (and replies) - done
3. Change tracking - done
4. Text highlighting - done
5. Read markers (graphical bookmarks) - tbd

# How to use this package:
1. Define the paper authors, using
     \defineauthor{<name>}{<handle>}{<short/single letter handle>}{color}

    for example:
    ```latex
    \defineauthor{Arie}{arie}{a}{blue!60!black}
    \defineauthor{Nachshon}{nachshon}{n}{purple}
    \defineauthor{Erez}{erez}{e}{red!50!black}
    ```
    
2. After defining the authors, a set of commands is going to be available for
   each author. Assuming the first author defined above, the commands will be
    * \anote{<text>} - Add a text note
    * \anotedone{<text>} - Add a text note that is marked done
    * \areply{<text>} - To add within the context of a note
    * \ainsert{<text>} - Add text that is marked as inserted
    * \adelete{<text>} - Mark text as deleted
    * \achanged{<text1>}{<text2>} - Add text1 marked as inserted, and mark text2 
                                  as deleted
    * \ahighlight{<text>} - Highlight the argument text (as if with a highlighter)
    * \arie - prints "Arie:" in the text in bold font, and the author's color
    * \arie[] - prints "Arie" as above
    * \arie[<text>] prints "Arie text" as above
3. Additional (general) commands
    * \todo{<text>} - Add a todo item
    * \todo[<callout>]{<text>} - Add a todo for an author, for example
        - \todo[\arie]{todo item}
    * \done{<todo or note>} - Mark a todo or note as done
    * \cboff - Turn of changebar functionality (for compatibility with figure*)
    * \cbon - Turn changebar functionality back on
    * \highlight{<text>} - Anonymously highlight text
    * \todolist - Print the list of todo items    
    * \authornoteslist - Print the list of author notes

# Package options:
The following options may be passed to the authortools package in the \usepackage[*option list*]{authortools} command.
* **hideall** - A master switch for hiding all annotations
* **hideauthornotes** - Hide author ntoes
* **showdoneauthornotes** - Show author notes that have been marked done (hidden by default)
* **hidechangetracking** - Hide change tracking
* **hidetodos** - Hide todo items
* **showcompletedtodos** - Show completed todo items (hidden by default)


# Cool Tips and Tricks

## Note References
You can do some cool stuff with notes. For example,

```latex
\anote[\label{anote-mynote}]{This is my note about ....}
```

and somewhere else in the text,

```latex
\anote{blah blah as I mentioned in my note \ref{anote-mynote}, this ....}
```

If the text in the second note is short (like quick ref), then the note number would 
get filtered out of the text in the \authornoteslist. 
You can still achieve the same effect by doing:

```latex
\anote[See my note \ref{anote-mynote}]{}
```

Since the text between [ and ] is passed unfilitered to the note command

Finally, in both cases hyper-linking works. Clicking on the note number 
would jump that note.


## Redirecting a note to multiple authors
You can direct notes (and todos) to multiple authors by adding callouts
to them between [ and ] of the note or todo command. 

```latex
\todo[{\erez[]}, \nachshon]{Please review the paragraph above for correctness}
```

Note that if you simply use [\erez, \nachshon] The text would show 
Erez:, Nachshon: Please review ...

However, by passing the optional argument to \erez as empty (and thus 
removing the default ':' after the author's name) you would get the cleaner
result of
Erez, Nachshon: Please review ...
