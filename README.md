#### CI/CD GitHub Actions workflow to turn off an Amazon Web Services EC2 instance.

What is GitHub actions?
GitHub Actions are an automated process that allows us to build, test, release and deploy any code project on GitHub, but we can also use it to automate any step of our workflow such as merging pull requests, assigning levels, triaging issues etc. In short: GitHub Actions are a custom software development workflow automation tool

**Prerequisites**

- [AWS account](https://portal.aws.amazon.com/billing/signup?refid=09863622-0e2a-4080-9bba-12d378e294ba&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start/email) [Free Tier]
- [GitHub account](https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home)


Go to AWS Account and Launch an EC2 instance, t2.micro is enough. Now, Click on Review and launch. You need nothing like Security Group for this. Proceed without a key pair.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/il6af7eb81vxnqegbe9l.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gd7kxqfim4fk1gwd907l.png)

---

Create GitHub [Repository](https://github.com/rishavmehra/GithubActions-EC2) make it Public
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/itolqy5aw1fzcyi6thyc.png)

**Creating your first workflow**
1. Create a .github/workflows directory in your repository on GitHub if this directory does not already exist.

2. In the .github/workflows directory, create a file named shutdown.yml. For more information, see "Creating new files."

3. Copy the following YAML contents into the shutdown.yml file:

```
name: shutdown
on:
  push:
  # branches: [ main ]
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Stop AWS EC2
        run: |
          aws ec2 stop-instances --instance-ids ${{secrets.AWS_EC2_INSTANCE_ID }}
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: ${{ secrets.AWS_REGION }}
```

**Create AWS Keys**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ua1kvf1i41v7s8ayjoh6.png)
- Click on _Security credentials_
- then, click on _Create access key_
Download Security credentials

Now, Add this Security credentials in GitHub _Secrets_ 
[Actions]. Create new repository secret now add this secret like this 

```
AWS_EC2_INSTANCE_ID = i-xxxxxxxx
AWS_ACCESS_KEY_ID = xxxxxxxxxxxxxx
AWS_SECRET_ACCESS_KEY= xxxxxxxxxxxx
AWS_REGION = us-east-1
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gudjidyo4p1x0v4966g9.png)
For AWS_Region add your running ec2 instance regions for me [us-east-1]

Now, final stage. Go to Actions tab GitHub Repo and select your workflow under your workflow _Run workflow_

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/evmvbrhgqwqs0wi1fsg7.png)

---

Socials [Website](https://rishavmehra.ml/) [Twitter](https://twitter.com/Rishavmehraa) [GitHub](https://github.com/rishavmehra) [LinkedIn](https://www.linkedin.com/in/rishavmehra/)


