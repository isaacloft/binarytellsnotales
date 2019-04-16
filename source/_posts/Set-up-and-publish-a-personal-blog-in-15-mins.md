---
title: Set up and publish a personal blog in 15 mins
date: 2019-04-15 20:00:59
tags: hexo
categories: tools
---

## First blog isn't about a touching tale
I'd just like to share the steps I've taken to set up this simple but very handy personal blog. 

There is going to be three main sections of this blog
1. Set up blog with [Hexo](https://hexo.io/) on your machine's local environment
2. Publish and host your blog to free github [page](https://pages.github.com/)
3. Add custom domain to your github io page, e.g. [goDaddy](https://au.godaddy.com/) and [nameCheap](https://www.namecheap.com/)

<!--more-->

### Build blog with Hexo
Hexo has a very no BS [documentation](https://hexo.io/docs/), but maybe I just make it simpler for you.

1. Install Node.js and Git if you have not, and make sure the version of the node is later than v6.9
2. Run this command to install Hexo command line tool
```bash
npm install -g hexo-cli
```
3. Use command line initialize the blog project
```
//Use terminal go to the folder you'd like to create the project and then run followings:

$hexo init NAME-OF-YOUR-BLOG
$cd NAME-OF-YOUR-BLOG
$npm install
```
4. Run it with local server
```bash
$ hexo server
```
And open localhost:4000 inside your browser, and you will see your blog up and running.
You should see at the index page, there is one blog existed and named Helloworld. It's generated for you as an example.

5. More terminal commands, please check this [document](https://hexo.io/docs/commands.html).
------------------------------------
### Publish to github page

1. Go to github and log in with your account
2. Confirm your github account name, for example, mine is "isaacloft". Reason for confirming this is that
we can only create one free github page and the name of the repo has to be YOUR-GITHUB-NAME.github.io
3. Create a new repo like the screenshot below:
{% asset_img create-github-io.jpg This is an example image %}
4. Go back to teriminal and navigate into your project folder, install this helper package
```bash
npm install hexo-deployer-git --save
```
5. Go to your project top level and open _config.yml file, at the end of that file add following lines
```bash
deploy:
 type: git
 repo: https://github.com/YOURGITHUBREPO/YOURGITHUBNAME.github.io.git
 branch: master
```
6. Everytime before publishing, we need to run generate command.
```bash
$ hexo generate
```
    I normally run the command below quite often just to clean up and generate final files
```bash
$ hexo clean && hexo g && hexo s 
```
7. Second last step, publish to github.io

    Before we proceed, you may want to check your git command line config.

```bash
$ git config --global user.name
$ git config --global user.email
```
    make sure the outputs are same as your github account info

    If you haven't set it up properly, please see [this](https://help.github.com/en/articles/setting-your-commit-email-address-in-git)

    Code to deploy
```bash
$ hexo deploy
```
    The deployment may take a few seconds or minutes

8. Check your repo settings to make your github.io page live
    Go to your repo setting page
{% asset_img io-setting.jpg This is an example image %}
    scroll down to this section
{% asset_img io-domain.jpg This is an example image %}
    If you see something similar, great, it should be done. Just click on the link and go to your own blog.


----------
### Use your custom domain name with github.io
Using custom domain name with github got a lot easier now, and github.io even enforces https for us and no charge.
What we need to do is below
1. Go to your domain provider, in my case, nameCheap.com
2. Go to DNS management section (name can vary from provides), on nameCheap.com it's called Advanced DNS...really?
3. Add below four A records and one CNAME record
{% asset_img custom-domain.jpg This is an example image %}
#### Note: Double check if there is any other A or CNAME record, which may affect your github-domain name binding
4. Go back to your github.io setting, and add your custom domain name
    For example: binarytellsnotales.com

{% asset_img add-domain-to-io.jpg This is an example image %}

If you see any error messages, it's possibly caused by DNS delay, which may take up to 24 hours to be reflected.

<b>Update!!</b>
The github page custom domain would be reset after each deployment, the solution is to include a CNAME file <b>inside</b>
your <b>soruce</b> folder.

github [issue](https://github.com/hexojs/hexo-deployer-git/issues/87)
## I guess this is it for now, if any question or feedback, please feel free to leave a comment.
    