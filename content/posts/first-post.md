---
title: "First Post"
date:  2018-05-07T20:55:01-07:00
draft: false
---

## About me

I am a recent graduate of Georgia Tech's OMSCS program. I am currently employed at a software company in Tucson. I graduated from the University of Arizona in 2016 with an engineering degree.

I plan to use this blog as a record of my work and my ideas. My current interests include machine learning and data science, mineral exploration (especially geophysical methods), geostatistics, GIS, and remote sensing.  

## Building the Blog

My blog is static HTML hosted on AWS. The proliferation of WordPress and other dynamic CMSs always confused me, especially when they crop up in applications like mine (a small personal site) where they are overkill at best and outright dangerous at worst. With the rise of serverless and PaaS there seems to be a renewed interest in plain old HTML sites, and plenty of different options for going static.

My first website was a single HTML page. I did not use a framework. I simply edited the HTML directly, by hand, and uploaded it to my server when I needed to make changes. Given this experience I can fully appreciate the headache that the Hugo framework saves me. [Definitely check it out!](https://gohugo.io/)

### Custom Domain Name

In terms of the DNS configuration, I have a custom domain name pointing at a cloudfront distribution, with an SSL certificate from Amazon’s Certificate Manager. I initially had some problems configuring all this, but it turned out to be a lot easier than most of the articles would have you believe.

If Amazon is your registrar it winds up being extremely easy to get an SSL certificate. Simply visit https://us-east-2.console.aws.amazon.com/acm/, press "Request Certificate", "Request a public certificate", enter your domain name (I just used nicholasshea.com, and the wildcard *.nicholasshea.com specified as an additional name, to cover www.nicholasshea.com and in case I decide to add an API endpoint at api.nicholasshea.com or something similar), and select DNS validation.

Amazon will ask you to enter a DNS record for your domain to prove it's yours. Amazon includes an option to do this automatically if you own your domain through Amazon Route 53. Be sure to click the arrow to display the option, it's not immediately obvious where to select this.

When creating your cloudfront distribution, be sure to select the SSL cert option and set the correct CNAMES (the same domains you set for the SSL certificate when you set that up). Other than that, just make sure you have a S3 bucket with your static site inside, and set that as the origin of the cloudfront distribution.

The last configuration change is made in Route 53. Using the domain name of your Cloudfront distribution (ddxkwihvl2t2m.cloudfront.net, in my case) set up two alias records for each of the site roots you want to use (nicholasshea.com and www.nicholasshea.com).

Now you should be done! Try it and see if it works for you. 

I made three pretty painful mistakes: 

1. I forgot to set the s3 bucket to public.
2. I did not select the http-to-https upgrading option. Instead I initially chose to drop all non-HTTPS traffic. This will drop a lot of traffic, as it turns out.
3. Be sure you include yourdomain.com and wildcard *.yourdomain.com as additional name when registering the. Otherwise you will get weird SSL cert errors when accessing www versus root. 

If you manage to avoid those pitfalls, this is a quick and painless process! 

I’ve listed a few of the resources that were most helpful to me, hopefully they are helpful to other beginners:

* [AWS Certificate Manager – Deploy SSL/TLS-Based Apps on AWS](https://aws.amazon.com/blogs/aws/new-aws-certificate-manager-deploy-ssltls-based-apps-on-aws/)
* [Setting Up an HTTPS Static Site Using Amazon AWS S3 and Cloudfront](https://medium.com/@esfoobar/setting-up-an-https-static-site-using-amazon-aws-7ab270c4e277)
* [Hosting a HTTPS website using AWS S3 and CloudFront](https://medium.com/@itsmattburgess/hosting-a-https-website-using-aws-s3-and-cloudfront-ee6521df03b9)
* [CloudFront: Creating a Distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html)
