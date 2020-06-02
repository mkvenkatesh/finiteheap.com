---
layout: post
title:  "My Emacs Journey"
date:   2020-04-26 16:00
categories: emacs
comments: true
disqus_id: "my_emacs_journey"
---

## Revival ##

It's been more than 3 years since my last post on this site. I'm not sure how
the time went by without any updates but I know that the major factor in not
being able to write was when I switched to a new employer in early 2017. This
meant a move across the country and being busy with work and life. This post is
an attempt to break this pause.

Few days ago, I upgraded my site from `Jekyll 3.x` to `Jekyll 4.0` which was
painful the way I did it. With the upgrade, I got rid off Google Ads and
Analytics on the site and turned off ads in `Disqus`. This blog is not popular
enough to generate ad revenue and the ads were making the site look like a
malware ridden tech blog. I really don't care for any site analytics either.
I'll rather have no external or third party JS loaded into this site. The site
loads and looks a lot better now.

I had a lot of unfinished blog posts in my _drafts folder. I was going through
and most of them are not relevant for publishing anymore. The drafts were from
3-4 years ago with very little information in them and I won't be able to
complete and publish them. Couple of the drafts were about `Emacs`. I was about
to delete them as well but figured I'd just post it out here after a little
cleanup. Here are my Emacs drafts...

## Emacs Journey ##

I was using Emacs for everything or at least I was trying to. I used Emacs for
editing, terminal operations, note taking (`org-mode`), password management,
Oracle client operations etc. I wanted to be in Emacs when I opened my computer
until I closed it. With that need came the obsession to customize and learn
Emacs in and out. The customization was such a painful endeavor and I spent a
lot of time trying to set up dependencies and adjust setting or copy snippets of
`elisp` code online and tweaking it here and there.

All this was going splendidly until I started experiencing [Pinky
RSI](https://www.math.ucdavis.edu/~greg/pinky-rsi.html). I initially had
`Control` key set as my `C-`, but after experiencing RSI, I switched to using
`Caps Lock` for `C-`. Using `Caps Lock` helped a little bit but didn't
completely eliminate my pinky issue. The pinky pain combined with the
maintenance nightmare of all my extension and constant tweaking, breaking,
learning, painful upgrades etc. left me dissatisfied with the state of my text
editor usage.

I wanted something that had less friction. I wanted something where I don't have
to invest too much time to learn or customize and just use the tool to get a job
done. I switched to `Sublime` text for a bit but I didn't like it that much. I
finally ended up with [Visual Studio Code](https://code.visualstudio.com/) and
it's been going very well. I haven't customized VS code too much nor have I
spent countless hours trying to learn the editor. I just use it out of the box,
look up some keyboard shortcuts when I need it, and get the work done. I'm very
happy with it and don't have any problems with RSI.

The visual explorer is very easy to get to my files, the regex search on a
project level, the integration with `Git`, spell checker, syntax highlighting,
code folding, code snippets/suggestions, editor window splits and movements,
terminal integration - everything just works out of the box. It's just so much
easier now. I was wanting to be a 10x in my text/coding/file management and
`Emacs` is certainly the tool for it but I lost patience and I'm happy to be at
3x with `VS Code`.

I had the following markdown drafted a long time ago about Emacs. I figured I'll
just post it out here in case anyone finds interesting tidbits or workarounds
for their Emacs usage.

### My Emacs Workflow in Mac OS X ###

Here is how I have setup Emacs on Mac OS X. This may not be the ideal
workflow for everybody but it works for me pretty good.

This post was last updated on `Jan 1, 2017` so all the information
below is current as of the date shown.

Here's my [.emacs][1] for the impatient ones and also a screenshot of
the editor with the beautiful [solarized-dark][2] theme.

![My Emacs Editor][3]

[1]: https://github.com/mkvenkatesh/dotfiles/blob/master/.emacs
[2]: https://github.com/bbatsov/solarized-emacs
[3]: /assets/images/my-emacs.png

### Versions ###

* Mac OS X 10.11.6 (OS X El Capitan)
* GNU Emacs 25.1.1 installed via [Homebrew][4]
* Node 7.1.0 installed via [nvm][5] 0.32.1
* Ruby 2.3.3 installed via [rbenv][6] 1.1.0
* Python 2.7.13 installed via [pyenv][7] 1.0.6

**Note:** It is paramount that you setup Node, Ruby and Python
properly in your computer. There are lot of third party tools that are
required by Emacs packages and they are often NodeJS, Ruby or Python
packages installed via npm, gem and pip respectively. I have used
version/environment managers to manage the installation of these three
tools and I highly recommend doing it this way but it's not a
necessity.

[4]: http://brew.sh
[5]: https://github.com/creationix/nvm
[6]: https://github.com/rbenv/rbenv
[7]: https://github.com/yyuu/pyenv

### Installation ###

There are multiple ways to get Emacs on Mac OS X but the following, I
think, would be the most popular of them.

* GNU Emacs with Homebrew (**Recommended**)
* [Emacs For Mac OS X](https://emacsformacosx.com/)
* [Yamamoto Mitsuharu's Emacs Mac Port](https://github.com/railwaycat/homebrew-emacsmacport)

I have tried all the three different options (along
with [Aquamacs](http://aquamacs.org/)) and I have to say the stock
version of GNU emacs from Homebrew has been the best for me. Your
mileage may vary.

If you have [Homebrew](http://brew.sh/) setup in mac, all you have to
do to install GNU Emacs for OS X is to issue the following command
from a terminal.

```shell
brew update
brew install emacs --with-cocoa --with-gnutls
```

The option `--with-cocoa` will install the graphical version of Emacs
along with the terminal version. `--with-gnutls` will provide SSL/TLS
supports for Emacs. It doesn't hurt to compile emacs with gnutls
options in case you decide to setup your email client or other tools
that needs these secure protocols from emacs.

### Graphical Vs Terminal Emacs ###

This is a decision you have to make. I initially went with just using the
terminal version for as long as possible.  I had
[iterm2](https://www.iterm2.com/) as my terminal emulator which provided
excellent functionality but ultimately it was not enough for me to just use the
terminal version of emacs as my sole editor. I missed having `super` and `hyper`
keys. I missed having the fringe for certain operations and there were other
small issues that pushed me over from using just the terminal version. Now I use
graphical version all the time and have the terminal version just as a backup.

If you want to use Emacs effectively, you want to run Emacs as a
server and use `emacsclient` to connect to it to edit files. The
advantage with having the emacs server running is that your `.emacs`
file would've been already evaluated and all the libraries or
variables will be set so when you issue an `emacsclient` command to edit
a file, it will be zippy.

To use emacs server/daemon effectively, don't do `brew services start emacs`. If
you do, run `brew services stop emacs`. Basically don't run emacs in daemon
mode. Just include the `server-start` command in your .emacs file and then open
the application on GUI app in login. Now you can use the running GUI instance to
visit files, or double click on files in Mac to open files in the same frame
`(set ns-pop-up-frames)`. from the terminal you can do `emacsclient -n .netrc`
to open a file in the existing GUI frame. If no frame exists, you can start one
with `emacsclient -c`

Some aliases that I have defined;

```bash
export ALTERNATE_EDITOR="alternate-emacs"
export EDITOR="emacsclient -t"
export VISUAL="emacsclient -n"
alias kill_emacs_server='emacsclient -e "(kill-emacs)"'
alias ec='emacsclient -n'
alias ect='emacsclient -t'
```

`alternate-emacs` is a bash script containing the following;

```bash
#!/bin/bash
open -a Emacs
```

### Emacs - Ansi-Term/Iterm2 Shell Integration ###

If you have iterm2 shell integration and use emacs's ansi-term, make
sure to move the shell integration script to `.bash_profile` instead of
`.bashrc`. Since ansi-term is an interactive non-login shell,
`.bash_profile` is not executed.

### iterm2 shell integration script ###

```bash
test -e "${HOME}/.iterm2_shell_integration.bash" && source "${HOME}/.iterm2_shell_integration.bash"
```

If you don't do this you will get some weird gibberish when bash starts in
ansi-term mode. For me, I get the following;

```bash
1337;RemoteHost=<user>@Venkateshs-Work-MBP.local1337;CurrentDir=/Users/<user>/Dropbox (Persona
l)/dotfiles1337;ShellIntegrationVersion=3;shell=bash133;C;133;D;01337;RemoteHost=<user>@Venkates
hs-Work-MBP.local1337;CurrentDir=/Users/<user>/Dropbox (Personal)/dotfiles133;A<user>@Venkates
hs-Work-MBP:~/Dropbox (Personal)/dotfiles$ 133;B
```

To disable the bell in ansi-term set `'(ring-bell-function (quote ignore))`

### ssh ###
Install `tramp-term` and bind key `s-x`. `authinfo.gpg` can be setup to get
passwords automatically for tramp sessions. remote directory tracking is
automatically done with `tramp-term.el`. `ssh_config` specifies some connection
configuration options.

### EDITOR Variable ###

I was getting `*ERROR*: Cannot open terminfo database file` in ansi-term for
certain applications like `pass` that uses EDITOR variable. I was using
`emacsclient -t`, instead now I use `emacsclient`

### SQL Setup ###

Make sure you set `SQLPATH` variable in bash profile and also in your emacs
using `setenv` or `exec-path-from-shell` to specify your `sqlplus` script (user
profile) folder.

## Fin ##

I had lot more sections planned out to detail my Emacs configuration and usage
patterns but I didn't get to complete and it's too late for me to write them out
now, given that I've been out of Emacsland for the last three years. The
keystrokes are still etched in my hand memory though. Every time I open emacs
for any reason in the terminal today, I can still effectively navigate and edit
files.