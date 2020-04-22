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

```bash
#!/bin/bash

JEKYLL_ENV=production bundle exec jekyll build
aws s3 sync _site/ s3://finiteheap.com --delete --size-only

```

## License ##

Finiteheap.com site content is licensed under [Creative Commons
Attribution 4.0 license](https://creativecommons.org/licenses/by/4.0/).

Source code distributed under [MIT License](https://finiteheap.com/MIT-LICENSE).
