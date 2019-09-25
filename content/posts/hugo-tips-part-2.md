---
title: "Hugo Tips Part 2"
date: 2019-09-24T21:34:42+02:00
---

# Hugo Tips: Part 2

I only have 3 tips this time, but they are important:

1. Always always always remember to run `env HUGO_ENV="production" hugo` (or the equivalent on your system) rather than just plain `hugo`. It is possible that running `hugo` will write the files in `development` mode, which puts NOCRAWL, NOINDEX tags on every page. These tags will prevent search engines from crawling your site. For Windows, it should be `set HUGO_ENV=production`.

2. If you have your site hosted on AWS (like me!), the AWS command line is by far the simplest way to get everything uploaded to the s3 bucket. 

    `aws s3 sync . s3://my-bucket/ --acl public-read`

    This command will upload only the changed files and replace the outdated version on s3.

3. A related point: always verify the public permissions for the site!

Sources:

- [Hugo Environment Variables](https://discourse.gohugo.io/t/questions-about-hugo-environment-variables/17865)
- [How to set environment variables in Hugo](https://www.drydenwilliams.co.uk/code/2017/05/29/set-environment-variables-in-hugo/)
- [Using High-Level (s3) Commands with the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html)