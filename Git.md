# Yet Another Git Manual

## A glib preface: my soapbox about design, software, and why this document exists

### Good design

When people talk about "good design" in the context of software, they often talk about "good UI." Let's talk about that first.

The term "good UI" is pretty ambiguous. It could refer to pretty UI or clean UI or fast UI, all of which are very different. One aspect that I would consider very important is the focus on _concepts_. The UI of a program should revolve around a small number of concepts, which should be used consistently and clearly throughout the program. There should be no surprises with concepts. They should just make sense.

As an example, consider Gmail. One concept in Gmail is what I would call the "conversation list." A conversation list is just what it sounds like: a list of conversations. Your inbox, your starred messages, your list of sent mail are all conversation lists. If you click on any of the messages And click the back button (or `u` if you have keyboard shortcuts enabled), you're taken back to the previous conversation list. Conversation lists look and behave the same if you click on a label or if you search, even in an arbitrarily complex way. The Inbox and a search for `size:2m older_than:1y` should both produce conversation lists that behave identically.

But well-designed software is more than just UI. The design of both the front-end and back-end code should be elegant, and it should match the data schema. And in my experience, at least, the easiest way to do that is to build it around those same concepts. If your concepts make sense and permeate the code at all levels, everything is easier. Your software becomes naturally intuitive to use, your UI becomes a lot more natural, and it's not a pain to write code to drive that UI.

### The problem with Git

Git does **excellently** as far as its concepts are concerned, but nevertheless has a **horrible** UI. To be clear, I don't just mean that it's a command-line program. Plenty of command-line programs have a very good UI in the sense that they're consistent and map well to their concepts. What I mean is that the various options, subcommands, flags, and other things you can pass to the `git` command are inconsistent, unintuitive, and obscure the concepts that they're build around. Unlike software that is not designed around clear concepts (and thus make it very hard to build well-designed UI for), Git is a program with very clear concepts and a UI that obscures them.

### Why this document exists

Git is a very powerful and useful tool, but the awful UI makes the learning curve very steep. If you want to learn it, the existing documentation roughly falls into one of two categories:

* The tutorials: These often will give you step by step instructions about how to achieve some common tasks. Since Git is a command-line program, these usually amount to a small set of commands to follow.

* The "how Git works" documents: These eschew the Git UI altogether and describe how the innards of Git work. Depending on the details of the document, you might be able to make your own little Git clone by the end of these.

The main problem with the above options is that they're too far on the two ends of the spectrum of documentation. The tutorials are nice if you just want to accomplish a basic task, but they make it hard to become anything but a very novice user. The bigger problem is that Git is a program that makes it very easy to get yourself into a situation that makes it seem like everything is broken. Unless the tutorial covered the specific situation you got yourself into, it's going to be hard to come out of it unless you know what's going on. Meanwhile, the "how Git works" documents are unnecessarily complex. Unless you're curious, you shouldn't have to know how Git works. When you drive a car, you don't have to learn about how engines work. Why should software be any different?

The other problem with the above two documents is that both of them ignore the specific concepts in Git, which as I said, are actually quite nice and powerful. The "how Git works" documents in particular ignore them altogether, and instead present readers with an unnecessarily complex and detailed descriptions of the inner workings of the program: in other words, precisely what the concepts should be designed to abstract away.

#### Who this document is intended for

This document is intended for folks who want to understand how to use Git beyond the one or two commands they know, but _don't_ care to know how Git "actually works" behind the scenes. If you just want to throw something on GitHub, this document is probably not for you (the [GitHub bootcamp](https://help.github.com/categories/bootcamp/) might be a pretty good place to start in that case). Similarly, if you're really curious about how Git actually works **and are pretty comfortable with it already**, this document might be too boring (the [Git Internals](http://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain) chapter of the _Pro Git_ book might be good in that case). If you consider yourself a novice with Git and want to become a more advanced user, this document is for you.

In terms of prerequisites, you do **not** need to be a programmer (or even be interested in programming) to read this book. All the examples we'll be using will be in plain old English. However, you **do** need to be comfortable with the Unix-like command line. At the very least, you should be comfortable entering commands and navigating directories. If you're not, there are plenty of tutorials and books available on the Internet.

Finally, what to expect after you finish this document: You will **not** know everything there is to know about Git, even just at the "concepts" level. You probably won't even know a majority of about each of the commands. What you will know, however, is the general theory behind the various commands. More importantly, you will have a vocabulary for the various concepts used throughout the program. This will make it easier to read the documentations and ask questions, and it will make it easier to find the answers to your questions online. In other words, you will have a much better idea of what you don't know.


## Formatting used in this document

To make reading this book easier, here is a summary of the various formatting decisions used in this document. You may have already noticed some of these above:

* This document uses `monospace font` for commands, file contents, and overall "computery" stuff.

* Anything indented in monospace that begins with a `$` sign is a command you should enter. For example:

         $ git version
         git version 2.3.2 (Apple Git-55)
     
  You should **not** enter the `$` sign when entering that command. It is only there to signify that this is a command (many Unix shells have their prompts end with the `$` sign, which is why it's there).

* Definitions are written in _intalicized_ font.

* Emphasized words are written in **bold** font.

* The word "Git" (capitalized in normal font) refers to the program itself.

* The word `git` (lowercase and in monospace) will refer specifically to the command.


## Getting started

If you don't have Git installed on your machine yet, you can get it from the [official website](http://git-scm.com/). Once you download it, you should configure it by telling it your name and email. Not only is this a good idea in general (for example, if you're sharing data with other people), Git will yell at you in some cases if you don't do it. Most often, you will want to configure it globally on your machine:

    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com

This will write your user and email to the **global** configuration file, which is located at `~/.gitconfig`. If you leave out the `--global`, it will get written to the **local** configuration file, which is located at `.git/config` in the Git repository you are currently in. Note that this presuppose
