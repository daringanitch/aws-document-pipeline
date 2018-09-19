# Cloud Ops Document Pipeline

CI/CD Pipeline for publishing .md (markdown format) documents to static S3 Website.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites workstation

### Install MkDocs
```
 #pip install mkdocs
 ```
### Terraform

- Terraform, https://www.terraform.io/downloads.html

- Create new repo in github for your website
- Clone repo  to your local workstation
- Create web-hook for repo and keep in safe place for later use in modifying the codepipeline tf.


## Setup

Clone the git repository of doc-pipeline to your local workstation, you will use the terraform scripts to build the s3 bucket and the codepipline for deployment of site.

```
Git clone https://github.spehosting.com/CloudOps/doc-pipeline.git
```

- cd into the s3-bucket-website directory
- Modify the S3-WEB.tf
- bucket name should be FDQN of website you plan to deploy.
-- ex. "s3-website-test.spehosting-ext.com"

run:

```
$terraform init
$terraform apply
```


- cd into the code-pipeline directory
- Modify the docs-repo.tf
- fill in the variables

run:

```
$terraform init
$terraform apply
```

## Creating the website locally

## mkdocs

https://www.mkdocs.org/#mkdocs

Run following command

```
$mkdoc new (FQDN of s3 website)
```

this is where you will build the initial website
```
$cd (FQDN of s3 website)
```

Start up your website
```
$mkdocs serve
```

http://localhost:8000

modify the mkdocs.yml file with the following:

```
site_name: Your Site Name Here

nav:
    - Home: index.md

theme: readthedocs
```

- check site



## Deployment

- place buildspec.yml file in site directory(used by code pipeline to deploy code to s3.
- Copy contents of /site directory to your website git repo.
- web-hook will automatically trigger pipeline build process.

Check s3 website url.
http://your-doc-website.s3-website-us-west-2.amazonaws.com

## New Document additions

- New documents are added to the /doc folder in your local mkdocs project folder.
- mkdocs.yml file needs to be modified for navigation
- see below mkdoc.yml

example:

```
site_name: Cloud Ops Document Repository

nav:
    - Home: index.md
    - Markdown Primer: markdown-primer.md
    - Kickass README: Kissass-README.md
    - new doc: newdoc.md
theme: readthedocs
```
- regenerate the site
```
mkdocs build --clean
```
- resync the /site folder with your website git repo
- deployment of new site will be automatic.
