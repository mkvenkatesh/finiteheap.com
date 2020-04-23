# Finite Heap #

Finiteheap is my personal blog/site built
with [Jekyll](http://jekyllrb.com). This site is hosted
in [Amazon S3](https://aws.amazon.com/s3/)
with [Cloudfront](https://aws.amazon.com/cloudfront/).

## Libraries Used ##
+ [Jekyll](http://jekyllrb.com)
+ [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/cli-s3.html)

## Dev Tools Used ##
+ [Emacs](https://www.gnu.org/software/emacs/)

## Workflow ##

1. Make new posts or edit existing posts
2. Try the following Git commands

```bash
-- stage all objects that were created or modified 
$> git add *

-- check status
$> git status

-- commit
$> git commmit -a -m "message"

-- push to Github
$> git push origin master

```

3. Verify site locally at [http://localhost:4000](http://localhost:4000) by
   running the following command

```
$> bundle update
$> bundle exec jekyll serve
```

3. Deploy code to S3

```bash
#!/bin/bash

JEKYLL_ENV=production bundle exec jekyll build
aws s3 sync _site/ s3://finiteheap.com --delete --size-only

```

4. Cloudfront caches objects, so if any objects are changed, like say
   `index.html`, use **Invalidations** tab in AWS CloudFront Distribution
   settings to push an invalidation to the edge servers. Use '*' to invalidate
   all objects, or you can be more specific.

## License ##

Finiteheap.com site content is licensed under [Creative Commons
Attribution 4.0 license](https://creativecommons.org/licenses/by/4.0/).

Source code distributed under [MIT License](https://finiteheap.com/MIT-LICENSE).
