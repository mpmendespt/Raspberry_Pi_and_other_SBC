---
layout: post
title: Using a custom domain with GitHub Pages
category: DNS DynDNS GitHub custom domain
---

Setup custom domain on the user page and then all the project pages of
Github repositories will automatically appear under the same url.

Github provides two types of pages,   
- User pages   
- Project pages

### User pages

It's a Github repository with a special name **username.github.io** and
all the contents of this repository must be in the **master** branch.

By default, the user pages are available under the url,
**http://username.github.io**.

### Project pages

Project pages are project specific files lying in the *gh-pages* branch
of the repository. These pages can be accessed via the url
**username.github.io/repository\_name**.

For example,

*Repository name -&gt; Test2*

*URL -&gt; http://mpmendespt.github.io/Test2*



### Custom domain for user pages

Custom domain can be set for both user and project pages.

**Step 1**   
Create the repository *username.github.io* on Github.

**Step 2**   
Add a CNAME file containing the custom domain name that you want to map.
The [CNAME] file contains, *yourdomain.com*

**Step 3**   
Follow your DNS provider's instructions to create a *CNAME* record that
points from your default pages domain to your
*YOUR-GITHUB-USERNAME.github.io*.

**Step 4**

[Adding a custom domain for your GitHub Pages site] ( see Custom domain for project pages, step 3, next)


Once the propagation is complete, whenever you visit
*YOUR-GITHUB-USERNAME.github.io* you will be redirected to the custom
domain *yourdomain.com*.

## Custom domain for project pages


### Create a gh-pages branch

### create a new repository on the command line

```ruby
echo "\# Test2" >> README.md   
git init   
git add README.md   
git commit -m "first commit"   
git remote add origin https://github.com/mpmendespt/Test2.git   
git push -u origin master
```


you'll need to create the new ***gh-pages*** branch and remove all content
from the working directory and index:

```ruby   
cd *repository*

git checkout --orphan gh-pages   
\# Creates our branch, without any parents (it's an orphan!) Switched to a new branch 'gh-pages'

git rm -rf .   
\# Remove all files from the old working tree

rm '.gitignore'

git branch --set-upstream-to=origin/gh-pages gh-pages   
```

### Add content and push

Now you have an empty working directory. You can create some content in
this branch and push it to GitHub. For example:

```ruby
echo "My Page" > index.html   
git add index.html   
git commit -a -m "First pages commit"    
git push origin gh-pages
```

Your GitHub Pages site should now be available. You'll receive an email
if your build is unsuccessful.

### Load your new GitHub Pages site

After your push to the *gh-pages* branch, your Project Pages site will
be available at
```http(s)://<username>.github.io/<projectname>``` .

<https://mpmendespt.github.io/Test2/>

## Custom domain for project pages

To Setup a custom domain for a gh-pages Project Pages repo that handles
www.yourdomain.com and yourdomain.com:

1.  From your project repo, gh-pages branch. Create a CNAME file with
    the contents *yourdomain.com*. Commit then push.

2.  Follow your DNS provider's instructions to create a *CNAME* record
    that points from your default pages domain to your
    *YOUR-GITHUB-USERNAME.github.io*.
3.  [Adding a custom domain for your GitHub Pages site](https://help.github.com/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site/)   

>  1.  On GitHub, navigate to your GitHub Pages site's repository.   
>  2.  Under your repository name, click **Settings**.    
>  3.  Under "Custom domain", add your custom domain and click **Save**.      



- Wait til the name servers update, and then confirm that the DNS record is set up correctly:

    ```dig www-mpmendespt.ddns.net +nostats +nocomments +nocmd```


```ruby
; <<>> DiG 9.9.5-9+deb8u6-Raspbian <<>> www-mpmendespt.ddns.net +nostats +nocomments +nocmd   
;; global options: +cmd     
;www-mpmendespt.ddns.net.       IN      A   
www-mpmendespt.ddns.net. 60     IN      CNAME   mpmendespt.github.io.   
mpmendespt.github.io.   2045    IN      CNAME   github.map.fastly.net.   
github.map.fastly.net.  10      IN      CNAME   prod.github.map.fastlylb.net.   
prod.github.map.fastlylb.net. 10 IN     A       151.101.12.133   
 
```


### References:

- <https://stackoverflow.com/questions/9082499/custom-domain-for-github-project-pages>   
- <https://pankajparashar.com/posts/custom-domain-github-pages/>   
- <https://help.github.com/articles/creating-project-pages-manually/>   
- <https://help.github.com/articles/setting-up-a-custom-subdomain/>   
- <https://help.github.com/articles/using-a-custom-domain-with-github-pages/>   
- <https://help.github.com/articles/setting-up-an-apex-domain/>   
- <https://stackoverflow.com/questions/23375422/how-to-setup-github-pages-to-redirect-dns-requests-from-subdomain-e-g-www-to>


[CNAME]: https://github.com/pankajparashar/pankajparashar.github.io/blob/master/CNAME
[Adding a custom domain for your GitHub Pages site]: https://help.github.com/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site/
