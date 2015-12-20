---
layout: post
title:  "Ansi-Term Remote Directory Tracking"
date:   2015-12-20 15:00
categories: emacs
comments: true
disqus_id: "ansi-term-remote-dir-track"
---

Suppose you are using `M-x ansi-term` in emacs and you issue `ssh
user@remotehost` command in the terminal session. Now when you do `C-x
C-f` to find a file, your mini-buffer is probably going to display
files and folders from the working directory from your localhost
machine.

```bash
# M-x ansi-term
mkvenkatesh@localhost:~/$ ssh mkvenkatesh@remotehost
mkvenkatesh@remotehost:~/$
# Logged into remotehost. C-x C-f will open working directory from localhost
```

Wouldn't it be wonderful if emacs tracked the remote host working
directory on such occasions? i.e when you are SSH'd into a remote host
using ansi-term, `C-x C-f` would automatically call tramp and open the
current working directory of the *remote host* in the mini-buffer so
you can work with folders and files easily. You can do this by putting
the code from [here]
(http://www.enigmacurry.com/2008/12/26/emacs-ansi-term-tricks/) (See
**TRAMP Integration** section), also shown below, into `.bash_profile`
in your *remote host*.

```bash
if [ $TERM = eterm-color ]; then
 function eterm-set-cwd {
 $@
 echo -e "\033AnSiTc" $(pwd)
 }

 function eterm-reset {
 echo -e "\033AnSiTu" $(whoami)
 echo -e "\033AnSiTc" $(pwd)
 echo -e "\033AnSiTh" $(hostname -f)
 }

 for temp in cd pushd popd; do
  alias $temp="eterm-set-cwd $temp"
 done

 eterm-reset
fi
```

Open `.bash_profile` in your remote host with emacs using the command
below and add the code from above to the end of the file.

```elisp
C-x C-f /ssh:mkvenkatesh@remotehost:/home/mkvenkatesh/.bash_profile
```

I was using this code in my DigitalOcean Ubuntu droplet box and of
course it didn't work. I had to make couple changes to the code and I
hope someone will find this useful as well.

The first thing to verify is if the correct `TERM` variable is used in
the code. In your remote host SSH session issue `echo $TERM` to make
sure it says `eterm-color`. If it says something different adjust the
first line in the code above to that value.

```bash
# verify TERM variable
if [ $TERM = eterm-color ]; then
```

The second thing that I had to change was the hostname section. The
remote host that I was connecting through SSH didn't have a domain
name (finiteheap.com) yet so I had to use the IP address. For any
remote host that you connect to that doesn't have a DNS entry, can
only be reached by an IP address so make sure to adjust the code
appropriately so TRAMP knows how to reach the server.

```bash
echo -e "\033AnSiTh" $(hostname -f)
# was updated to
echo -e "\033AnSiTh" 104.160.65.45
```
