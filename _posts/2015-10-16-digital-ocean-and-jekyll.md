---
layout: post
title:  "Digital Ocean and Jekyll"
date:   2015-10-16 16:53
categories: webdev
comments: true
disqus_id: "do_jekyll"
---

## Digital Ocean ##

The old Finite Heap site was hand built and was hosted with
[MyDomain](https://mydomain.com) under a shared Linux hosting
plan. The hosting plan was okay for a static site. It was about
$51/year and had SFTP option and I think that was the highlight of
it. CPU and memory were shared and disk space/bandwidth was
unlimited. For a static site that doesn't get many visitors this is
more than anyone needs. Oh and my old hosting plan had support for PHP
and Perl scripting but that would have probably hit the CPU limit for
a moderately busy app. I wasn't planning to use any server side
languages anyway so it suited my purpose for couple years.

<img class="center-image" src="/assets/my-domain-do-logo.jpg"
alt="MyDomain and DigitalOcean">

Then came the talk and hype of
[DigitalOcean](https://www.digitalocean.com). A full VPS with SSH
login and complete control over the box starting with $5/month? That
never happened in the hosting world. I didn't think I would use that
much capacity so I never switched to DigitalOcean and I was waiting
for them to go out of business for giving such cheap but fantastic
options. I was wrong and they flourished. Why not have more options
and control over your hosting when the pricing is almost the same
between the two companies. Now a 512MB memory with 1 CPU core and 20GB
SSD storage is just <strong>$5/month</strong> so I pulled the plug on
MyDomain and finally went with DigitalOcean.

<img class="center-image" src="/assets/do-hosting-plan.jpg"
alt="Base DigitalOcean droplet pricing">

DigitalOcean has some really nice features. They call a VPS instance a
droplet. You can create a droplet based on variety of Linux flavors
and you can select regions, size and automatic backups. They also
provide free snapshots! Backups cost money though. You can add your
public SSH key while you create a droplet so you can later SSH into it
and manage the box easily. Their knowledge-base articles are the best
documentation I've see for server maintenance, tools setup and
configuration. The articles that they send you through email after you
create a droplet is pretty nice and I was able to setup my Ubuntu
droplet fairly quickly with some basic security and server
configuration (nginx, fail2ban, SSH hardening, UFW rules etc).

##Jekyll##

<img class="center-image" src="/assets/jekyll.jpg"
alt="Jekyll">

While switching to DigitalOcean I decided to use
[Jekyll](https://jekyllrb.com/) instead of hand crafting the site
code. It's so much easier to focus on the content instead of site
maintenance. It's faster to write blog posts in markdown and just
issue one command to build up the static site with tons of
features. Jekyll provides an easy way to manage layouts, includes,
variables, pagination, drafts, tagging, categories and various other
features. I'm really happy and productive with this setup i.e
DigitalOcean + nginx + Jekyll. I hope I stay on this for a while
before I get distracted by something shiny and start all over again.
