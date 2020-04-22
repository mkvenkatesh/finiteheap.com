---
layout: post
title:  "Moving from DigitalOcean to Amazon S3, Cloudfront and Route 53"
date:   2017-01-08 20:30
categories: webdev
comments: true
disqus_id: "from_do_to_aws"
---

## Old Stack

For FiniteHeap, I was using [MyDomain][1] for registrar services
and [DigitalOcean][2] for hosting and DNS service. I
used [letsencrypt][3] for SSL. I use [Zoho Mail][4] as my domain's
mail service. I used to pay $5/month for my DigitalOcean droplet and
about $10/year for domain renewals. It was not a bad deal but I did
not fully utilize my droplet as I intended it to. For hosting
a [Jekyll][10] site, which is static, I did not need a full blown
Linux VPS with SSH control. Initially I was thinking I would write
some web applications and host it in the droplets but that never came
so it's time I dialed back my hosting services.

## Current Stack with AWS

Few days back I switched my stack to Amazon Web Services. I
transferred my domain from MyDomain to [Amazon Route 53][5]. This took
less than a day even though the quoted time frame was more than a
week. The transfer steps were pretty straight forward once you enter
the domain name that needs to be transferred in Amazon Route 53
screens.

Once the domain was transferred, it was time to move my site and DNS
records off DigitalOcean to AWS. I decided to use [Amazon S3][6] for
my static site hosting since it's scalable, reliable and super
cheap. On top of that, adding Amazon's CDN - [Cloudfront][7] was just
icing on the cake and insanely cheap as well.

There was one more reason I went with Cloudfront. Hosting your site
with **S3 doesn't offer you HTTPS capability**. This is where
Cloudfront comes in. When setting up Cloudfront cluster for your S3
site, you can either import SSL/TLS certificates (from letsencrypt or
other SSL providers) or use Amazon's own SSL certificates for free! I
just went with [Amazon Certificate Manager][9] since it was easier to
provision, manage and assign them to Cloudfront clusters easily.

I followed this [article][8] from Amazon's Docs on how to use S3 and
Cloudfront to host a static site. That link is all you need. I don't
need to write them down here again.

I moved all my DNS records from DigitalOcean, including MX records for
Zoho Mail, to Route 53 by using a hosted zone and also updated the
nameservers for my domain to point to the hosted zone's
nameservers.

### Stack Transition

| Service | Old | New |
| :-----: | :-- | :-- |
| **Registrar** | MyDomain ($10/yr) | Amazon Route 53 ($12/yr) |
| **DNS Service** | DigitalOcean (free) | Amazon Route 53 ($0.50/mo) |
| **Hosting** | DigitalOcean ($5/mo) | Amazon S3 (< $0.30/mo for my use) |
| **CDN** | None | Amazon Cloudfront (< $0.10/mo for my use) |
| **Hosted Mail** | Zoho Mail (free) | Zoho Mail (free) |
| **SSL** | Letsencrypt (free) | Amazon Certificate Manager (free) |

<br>

### Workflow

Now I have myself a world class website infrastructure for pennies.

My workflow now involves, writing posts using Jekyll, do `jekyll
build`, push code to Github and then use AWS CLI to sync the `_site`
Jekyll contents from my local machine to S3 using the following
command.

```shell
$ aws s3 sync _site/ s3://finiteheap.com --delete --size-only
```

I use the `--size-only` attribute below to copy the files
that have changed in size in `_site` directory instead of the default
way of checking the modified dates. The problem with Jekyll is
building the site deletes the `_site` folder and regenerates all the
files in it which will have new modified date (unless you use the
experimental incremental build feature) so every S3 sync would upload
all the files from local machine to S3. Little undesirable for me so I
went with checking for size and keeping an eye during sync's to make
sure everything that's changed with the site gets pushed out.

I think for now I'm happy with this setup. Let's see what my first
month's bill is going to be like.

[1]: http://www.mydomain.com/
[2]: https://www.digitalocean.com/
[3]: https://letsencrypt.org/
[4]: https://www.zoho.com/mail/
[5]: https://aws.amazon.com/route53/
[6]: https://aws.amazon.com/s3/
[7]: https://aws.amazon.com/cloudfront/
[8]: http://docs.aws.amazon.com/gettingstarted/latest/swh/website-hosting-intro.html
[9]: https://aws.amazon.com/certificate-manager/
[10]: https://jekyllrb.com
