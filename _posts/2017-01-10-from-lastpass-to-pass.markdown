---
layout: post
title:  "LastPass to Pass"
date:   2017-01-10 22:00
categories: bash
comments: true
disqus_id: "from_lastpass_to_pass"
---

## LastPass ##

I loved [LastPass][1]. It was simple and it just worked. Between
having same password for every site or weak passwords that I could
store in my head, LastPass was a welcome replacement and a very
convenient one at it for managing website passwords and encrypted
notes.

<img class="center-image" src="/assets/images/lp-logo.png"
alt="LastPass Logo">

## Pass ##

I still highly recommend LastPass for anyone that's looking for a
password manager but I recently switched to [`pass`][2]. I have been
spending lot of time lately in Emacs and ansi-term and I was looking
for a command line password manager that's simple but very
secure. Looking around, I came across `pass` and I have been very
happy to use it as a replacement for LastPass.

The basic premise with `pass` is that you manage one or more .gpg
files and `pass` provides a neat wrapper around manipulating and
dealing with the .gpg files.

### Features ###

+ Light-weight command line utility
+ Uses [GnuPG][3] for encryption and decryption
+ Version control encrypted content using [Git][4]
+ Generate random passwords
+ Search ("grep") within your encrypted content
+ Copy password (clip) to clipboard or show the password
+ Move, copy, rename or edit your password-store .gpg files
+ Bash completion for `pass` commands and password store paths

### Migration and Workflow ###

I moved over all my passwords, notes and other encrypted information
from LastPass to `pass` and I love my workflow now. I don't miss the
convenience of LastPass at all. It takes a second to clip my password
for a given site using `pass` in ansi-term or [iterm2][5] and then
paste it into the web browser. The only complaint I have is that
grepping files seems to be very slow when you have tons of .gpg
files. Passing a path to the `pass grep` command would be a very good
option.

You can impose any structure you want in organizing your passwords but
I find the following organization very easy to work with. For e.g: If
I have two Gmail accounts I would store it as below in `pass`

```shell
$ pass insert personal/gmail.com/user1
$ pass insert personal/gmail.com/user2
```

<img class="center-image border" src="/assets/images/pass-structure.png"
alt="Pass Organization">

Head on to the [`pass`][2] site for more information if you want to
try it.

[1]: https://www.lastpass.com/
[2]: https://www.passwordstore.org/
[3]: https://www.gnupg.org
[4]: https://git-scm.com/
[5]: https://www.iterm2.com/
