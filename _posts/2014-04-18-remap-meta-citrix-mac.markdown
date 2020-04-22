---
layout: post
title:  "Remap Emacs Meta Key in Citrix on Mac"
date:   2014-04-18 21:32
categories: emacs
comments: true
disqus_id: "remap_meta_citrix_mac"
---
For work, I run Windows applications in my Mac frequently using
Citrix. I have GNU Emacs for Windows installed on the Citrix machine
so dealing with text editing is easier. Meta key mapping was screwed
up by default. No matter what kind of lisp code I used or settings I
changed I couldn't get my Alt/Option or Command key to act as Meta
(say for `M-x`). I either had to do `Esc-x` or `Option-Command-x`
which are both equally horrendous.

After a while I found out this keyboard mapping setting tucked away in
Citrix client. When you have any Citrix apps open, if you click
`Citrix Viewer->Preferences->Keyboard` you'll see **Send Alt character
using** setting and then a dropdown option containing two choices. The
default being `Option-Command`. I switched it to use `Command`. I
would've preferred if there was just an Option remap to Alt but sadly
there wasn't. So it appears Citrix modifies the keys sent from my Mac
keyboard to windows apps and remapping this key made emacs more
usable.

Now I can do `Command-x` for `M-x`

<img class="center-image" src="/assets/images/remap-meta-citrix-mac1.png"
alt="Citrix Viewer Preferences for Keyboard">


<img class="center-image" src="/assets/images/remap-meta-citrix-mac2.png"
alt="Send Alt Characters Using Setting">
