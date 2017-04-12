+++
date = "2016-11-20"
title = "Hugo Deploys with Wercker and S3"
author = "Royce"

+++

How to deploy a Hugo generated static site to S3, and automate builds with Wercker.

<!--more--> 

## Brief

Serve a static site cheaply and efficiently on your own domain. 

## How To

Using [Hugo](https://gohugo.io/) to generate a static site means that we can host it on a cloud storage service like [Amazon S3](https://aws.amazon.com/s3/) for a few cents each month. 

Hugo will let us edit posts and pages quickly with MarkDown, and an automated build and deploy to S3 with [Wercker](www.wercker.com) makes publishing simple as pushing to a repo.

### Sign ups

You'll need to sign up for a few services: 

- [Amazon S3](https://aws.amazon.com/s3/)
- [Wercker](http://www.wercker.com)
- [GitHub](http://github.com)

### Local tools

You'll also need some basic tools on your machine: 

- `hugo`
- `git`

### Hugo

Get started with Hugo [here](https://gohugo.io/tutorials/automated-deployments/). Pretty straightforward setup for static site generation.

Steps recreated here: 

```
$ brew install hugo
$ hugo new site and-wells
$ cd and-wells
$ mkdir themes
$ cd themes
```

Go ahead and add your themes to the themes folder.

Make a post or page, then go check everything out locally. 

``` 
$ hugo new about.md
$ vim content/about.md
$ hugo server --buildDrafts
```

### GitHub

Make a repo on GitHub and add your Hugo files.

```
$ git init
$ echo "/public" >> .gitignore 
$ echo "User-agent: *\nDisallow:" > static/robots.txt
$ git remote add origin git@github.com:comraderoyce/and-wells.git
$ git push -u origin master
```

### S3

Sign up and then sign in to an AWS account. Spin up a new S3 instance. Make a new bucket for your site (the bucket name should be the same as the domain name you want to use including "www") and then turn on Static Web Hosting in the properties menu. Copy the endpoint, and point your domain to your new S3 bucket. 

You'll also need to get some keys to work through the deploy with Wercker. You'll find those in Security Credentials. 

Create a new Access Key. Save your key info to a safe place as Amazon will only show it to you once. 


### Wercker

Sign up and login in to Wercker. Go ahead and make a new application. The application creation process will let you connect your GitHub or Bit Bucket account. 

All of the other defaults in the application set up will work fine. 

Wercker will need your Amazon key information to deploy to S3. Add those in the Environments tab. Use `URL`, `KEY` and `SECRET`. The `URL` variable is the URL  of your bucket and will need to be in `s3://roycewells.io` format. You'll need these variables in the `wercker.yml` file that tells Wercker the steps of your build and deploy. 

The `werkcer.yml` file goes in the root folder of your site. 

```
# werkcer.yml
box: debian
build:
  steps:
    - arjen/hugo-build@1.13.1:
        version: "0.15"
        theme: royce
        config: config.toml
        flags: --buildDrafts
deploy:
  steps:
    - s3sync:
        key_id: $KEY
        key_secret: $SECRET
        bucket_url: $URL
        source_dir: public/
        opts: --acl-public --add-header=Cache-Control:max-age=604800
```

That should take care of the two steps that you will need, the build with hugo which and the deploy to S3. 

Back in the Wercker application dashboard, you'll need to add a new pipeline for the deploy step. In the workflow, add in the deploy pipleline piece, so you've got a build to deploy workflow set up. 

A simple push to the git repo should trigger the build on Wercker and then deploy to S3. This makes it very simple to quickly update your site or publish additional material. 

## Appendix

### Sources 

Wercker has changed their UI since a lot of these were written, but I was able to figure out most of the above by using these: 

- [Static Site Automated Deployment](https://samaxes.com/2016/02/static-site-automated-deployment/)
- [Automated Deployments with Wercker](https://gohugo.io/tutorials/automated-deployments/)
- [A continuous deployment workflow for Hugo with Wercker and S3](http://danbahrami.io/articles/wercker-s3-workflow-hugo-deploy/)
- [Deploy Hugo Files to S3](https://lustforge.com/2016/02/28/deploy-hugo-files-to-s3/)
- [How anyone in the world can create cheap static sites.](http://katsenblog.com/post/85144002449/how-anyone-in-the-world-can-create-cheap-static)
- [Pointing a Domain to an Amazon S3 Bucket](http://steveliles.github.io/pointing_a_domain_name_to_an_amazon_s3_bucket.html)






