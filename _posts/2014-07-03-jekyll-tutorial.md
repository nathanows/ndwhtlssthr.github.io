---
layout: post
title: A Beginner's Jekyll Tutorial
---

This blog is based on the Jekyll framework and hosted on GitHub Pages. As I was going through the process of choosing a platform I came across Jekyll and was intrigued by the concept of hosting directly on GitHub, which, as someone trying to immerse myself in the development ecosystem, is intimidating, but seemed like a great opportunity to force myself to get aquainted with GitHub. Still, functionality is obviously number one, and beyond being a platform I'm purely interested in, Jekyll is known to be fast and flexible. Oh yeah, and it's free! 

This tutorial covers step by step how to setup and publish a very simple Jekyll blog and publish it to GitHub Pages:

- [**Audience**](#audience): Who this tutorial is written for
- [**Goal**](#goal): What will be accomplished in this tutorial
- [**Setup**](#setup): Setting up the necessary development environment to install and run Jekyll
- [**Jekyll/Hyde**](#jekyllhyde): Getting up and running using Jekyll and getting started with the Hyde theme
- [**GitHub Pages**](#githubpages): Loading your page to GitHub Pages
- [**Custom Domain**](#customdomain): Linking your newly created site to your personal domain
- [**Next Steps**](#nextsteps): You've got a generic site online, now what?

---


##<a name="audience"></a>Audience
I'll preface this post by saying that I'm no expert on most any of this, and therefore not really the standard Jekyll user. This means that there may be elements I won't (read: can't) fully explain. If you're starting at a higher level, everything should still work, but may not have the meaty context you desire (mmm... meaty context...). 

That said, I'm writing this because this is what I wished I could find as I was going through this process. It also starts from scratch, literally. I recently updated to new computer so I was starting from nothing. This isn't likely to be the case for most of you, meaning you can skip some of the initial setup, but if you're brand new this is the tutorial for you. 

The other plus if you're a beginner is that I'm going to explain things in a way that I, another beginner, understand them. One of the problems that I ran in to going through this process was the really quick dropoff in a lot of the instructions I found along the way. They start you off wading through the shallow end of the pool and about half way across you quickly realize it's not a steady decline as you fall off the 10 foot ledge directly in to the deep end. No lifeguards, nothing, and you're just left floating there in your waterwings... not here. (yeah, I know, this also means it's possible I'm giving you bad information... the process worked for me, take it or leave it)

---

##<a name="goal"></a>Goal
This tutorial will walk you step by step through setting up the development environment to install [Jekyll](http://jekyllrb.com/), creating a Jekyll blog using the [Hyde](http://hyde.getpoole.com/), hosting your site on [GitHub Pages](https://pages.github.com/), and adding a domain alias so that you can link your GitHub Pages site to your own domain. 

This tutorial will not cover customizing the site or creating/managing posts, but if you want to go further, stay tuned, that's coming up next. You'll learn alongside me. 

---

##<a name="setup"></a>Setup
Before we can start using Jekyll we need to install the correct components of our development environment. Remember, I'm starting from scratch, so you may be able to skip most of this if you've done any sort of Ruby development in the past. I'll also note that it's possible not every step in this is necessary, I ran in to errors as I was trying to get Jekyll installed and these are the components that I needed to install before it worked. You can try installing Jekyll right away by typing the following command at the terminal prompt:

```
sudo gem install jekyll
```

NOTE: This entire setup process was performed on a Mac running OSX 10.9, though everything should still work correctly on earlier versions of Macs. If you're running linux the same process I outline below should work for you. If you're on Windows, you've got an uphill battle as Jekyll doesn't officially support Windows, but tutorials exist, like [this one](https://github.com/juthilo/run-jekyll-on-windows).

If you got errors when you tried the install, follow along.


####1. Install Xcode
If you don't have it installed already, go the App Store and **install Xcode**. (Xcode is an integrate development environment that contains a suite of software development tools developed by Apple for developing software for OS X and iOS)

* After you've downloaded and installed Xcode, you need to accept the Xcode license terms. Go to Spotlight and search for and open Terminal.
* At the terminal prompt run the following:

	```
	sudo xcodebuild -license
	```
* Press 'q' then type 'agree' to accept the license agreement 

####2. Install Homebrew
Sold as 'the missing package manager for OS X', [Homebrew](http://brew.sh/) makes it easy to install frequently used packages that Apple doesn't include in OS X. 

To install Homebrew, paste the following at a Terminal prompt:

```
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

####3. Install GCC
This is a piece that I ran across on StackOverflow while troubleshooting an error, I'm not 100% if this was necessary for the Jekyll install, but is one of the things that I installed along the way. GCC stands for the GNU Compiler Collection and is a part of the standard GNU toolchain. Here's the install process I followed for the GCC install:

```
brew update
```
```
brew tap homebrew/dupes
``` 
```
brew install apple-gcc42
``` 
Make sure you don't receive any error when running:

```
which gcc-4.2
``` 
####4. Install MacPorts
Go [here](https://www.macports.org/install.php) and click on your version of OS X (we've already installed Xcode and accepted the license agreement).

####5. Install Ruby Version Manager [RVM]
[Ruby Version Manager [RVM]](https://rvm.io/) allows you to easily install, manage, and work with multiple Ruby environments. While we'll only be using the latest stable version of Ruby right now, the pay come in handy if you continue usine Ruby for different projects going forward. So first install RVM by pasting the following in to Terminal:

```
\curl -sSL https://get.rvm.io | bash -s stable
``` 
Once this has completed restart your Terminal.

####5. Install Ruby 2.1.2
If you're running on a UNIX system (Mac/Linux), and I'll assume you are since it would make no sense for you to be at this point in the tutorial if you were running Windows, Ruby comes pre-installed with your OS. You can see this by typing `ruby -v` at a Terminal prompt. If you're not already using the 2.1.2, let's install this latest stable version to RVM. At your Terminal prompt run:

```
rvm requirements
``` 
then:

```
rvm install 2.1.2
``` 
Finally, let's set this version of Ruby to be the default ruby when you open a new terminal shell, we'll use the `--default` tag:

```
rvm --default use 2.1.2
``` 
To verify that this worked you can check the current Ruby version again by typing:

```
ruby -v
``` 
And that's it, we're all setup! We should be ready to install Jekyll and get started on actually getting our site ready to go. Continue on to the next section where we'll walk through installing Jekyll, getting our page template downloaded and setup, and at the end see our page running in a browser (locally).

---

##<a name="jekyllpoole"></a>Jekyll / Hyde
Assuming you've completed the setup above, you're ready to get started with Jekyll itself, and it should be really easy!

####1.Install Jekyll
To install Jekyll we're going to use RubyGems which is software (it comes packaged with all Ruby versions > 1.9) that allows you to easily download, install, and use ruby software packages, one of which is Jekyll. To install open a terminal window and run:

```
sudo gem install jekyll
``` 
The install will take a few mins, and when it's done you should see something similar to the following:

``` 
Done installing documentation for blankslate, celluloid, classifier, coffee-script, coffee-script-source, colorator, execjs, fast-stemmer, ffi, hitimes, jekyll, jekyll-coffeescript, jekyll-gist, jekyll-paginate, jekyll-sass-converter, jekyll-watch, kramdown, liquid, listen, mercenary, parslet, posix-spawn, pygments.rb, rb-fsevent, rb-inotify, redcarpet, safe_yaml, sass, timers, toml, yajl-ruby after 24 seconds
31 gems installed
``` 
You'll see that in additional to the `jekyll` gem itself, it also installed, in my case, 30 additional dependent gems that Jekyll uses. 

We're going to hold off on testing out Jekyll on anything right now and move on to getting our template set up so we've got something to display when we fire it up. 

####2. Download Poole > Hyde Theme
For this site I chose to use a Jekyll theme called [Hyde](http://hyde.getpoole.com/) which is based on an underlying theme, [Poole](http://getpoole.com/). While a theme isn't completely necessary and we could create our own templates, we're going to use this as a foundation to build off of (a little instant gratification...). 

Go to the [Hyde Website](http://hyde.getpoole.com) and on the left sidebar click on Download. Unzip this file and move it to a new directory where you want to house this site (the live site will live on GitHub, but this is where you'll edit it from). For now I recommend moving it in to your Documents folder as this is where the rest of the tutorial will work from. Rename this directory as you'd like (for the purposes of this tutorial I'll call the directory `hyde-blog`). 

####3. It lives!
Alright, we've got a site. Let's fire up Jekyll and take a look at in the browser. Right now this will just be an exact replica of what's on the Hyde website, but it's a start. Open up a Terminal window and navigate to the project directory. 

I'm assuming most people will be to navigate to the project directory, but just to be thorough, type `pwd` to see your current location. Type `ls` to list the files in the current directory, to navigate to the Documents directory type `cd Documents`, then if you're using the naming I used above type `cd hyde-blog` (or whatever you named your project directory).

Once you're in the project directory we'll start up Jekyll's built in development server so we can view the site locally. Start the server by running:

```
jekyll serve
```
With this we've got a live version of the site running locally. 

####4. Check out the site
To access the site, open a new browser window and navigate to `localhost:4000`. And there's the site! After you've looked around, let's stop the server for now. go back to the Terminal window where you started the server and press `CTRL+C`.

####5. Minor edits
That's cool and all, but let's make a couple of quick edits just so it's clear that this is our site and not just the stock template. In Finder, navigate to your project folder and open `_config.yml` in your favorite text editor (I'm using [Sublime Text](http://www.sublimetext.com/)). 	It looks like this:

```
# Dependencies
markdown:         redcarpet
pygments:         true

# Permalinks
permalink:        pretty

# Setup
title:            Hyde
tagline:          'A Jekyll theme'
description:      'A brazen two-column <a href="http://jekyllrb.com" target="_blank">Jekyll</a> theme that pairs a prominent sidebar with uncomplicated content. Made by <a href="https://twitter.com/mdo" target="_blank">@mdo</a>.'
url:              http://hyde.getpoole.com

author:
  name:           'Mark Otto'
  url:            https://twitter.com/mdo

paginate:         5

# Custom vars
version:          2.0.0

github:
  repo:           https://github.com/poole/hyde
```

For the sake of this test run, 	let's update the `#setup` section (update all sections except for url). After you've updated save the file and close out. Go back to your Terminal window and restart the dev server:

```
jekyll serve
```
In your browser window refresh the `localhost:4000` page. It's nothing big... but it's something! But what good is a local-only website? Next we'll get this site up and running on GitHub pages.

---

##<a name="githubpages"></a>GitHub Pages
Now we've got a local site (OK, we've downloaded a template...), so let's get this online so we can share this out to the world. I mean, what if the main Hyde site goes down! To do this we're going to use GitHub Pages. GitHub Pages are public webpages freely hosted and easily published through the GitHub site. 

####1. Create GitHub Account
The first thing you'll need to do, if you don't have one already, is to create a GitHub account by going to the [GitHub Website](https://github.com/). While the last part of this tutorial will walk through the process of assigning a custom domain name to the page, but if you don't have or don't plan on using a personal domain name pay attention to the GitHub username that you select because your website URL will be `username.github.io`.

####2. Set up Git
a. [Download and install the latest version of Git](http://git-scm.com/downloads).
b. Open Terminal and tell Git your *name* so that your commits will be properly labeled by typing:


```
git config --global user.name "YOUR NAME"
```
c. Next tell Git the *email address* that should be associated with your Git commits. This email needs to be the same one that you used to setup your GitHub account.

```
git config --global user.email "YOUR EMAIL ADDRESS"
```
	
####3. Authenticating to GitHub from Git
When you commit to or clone a GitHub repository from Git, you'll need to authenticate to GitHub using either HTTPS or SSH. GitHub recommends using SSH so that's what will be used for this tutorial. 

Follow the process outlined on the GitHub website to [generate the necessary SSH keys](https://help.github.com/articles/generating-ssh-keys). 

SSH keys are a way to identify trusted computers, without involving passwords. The steps on the GitHub site will walk you through generating an SSH key and then adding the public key to your GitHub account. 

####4. Create a New GitHub Repository
Now that your account is all set up, we need to create the Repository (this is the GitHub project directory) that we will load this site to. 

a. Log in to your GitHub account
b. On the home page, in the bottom right portion of the screen in the 'Your Repositories' section click on `+ New repository`
c. Enter your `Repository name`. IMPORTANT: This needs to be `username.github.io` (replacing 'username' with your GitHub account user name). The site will not work if this repository is not named correctly. 
d. Enter a brief site `Description`
e. Leave this as a `Public` repository
f. Don't select to initialize a README file
g. Click `Create repository`

We're getting close. You've now setup the landing zone for your future site.

####5. .gitignore
One of the directories that Jekyll generates when serving up the site locally is a _site directory. This file contains all of the necessary static files to view the site. For the purposes of our GitHub Page we don't actually want to upload this, so we're going to create a .gitignore file in our directory which will tell Git to ignore the files listed in it.

a. Create our `.gitignore` file by navigating to the project directory in Terminal, and running:

	```
	touch .gitignore
	```

b. Because this file starts with a '.', the OS will hide this file by default. There are a few ways to show this file, so choose one of the following and open the newly created file in your text editor:
	- I use a Finder replacement called [Path Finder](http://cocoatech.com/pathfinder/) in which I can just go to the view menu and select 'Show Invisible Files'.
	- Path Finder costs money, so a free solution is to download a small freeware app called [Funter](http://nektony.com/products/funter) that adds an icon to your menubar allowing you to quickly show and hide invisible files.
	- Finally, if you want something free that you don't have to install, you can follow the [tutorial here](http://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/)  
	
c. Once you've opened the `.gitignore` file, we're going to add two new portions. In the first line of the document let's take care of the `_site` directory. Type:

	```
	_site/
	```
That takes care of the first directory. Next we're going to ignore any OS generated files that we wont need (when you un-hid files you shound also have seen a .DS_Store file show up, this is one of those OS generated files that we don't need). To hide this, and others, below the _site entry we added, copy and paste:

	```
	# OS generated files #
	######################
	.DS_Store
	.DS_Store?
	._*
	.Spotlight-V100
	.Trashes
	ehthumbs.db
	Thumbs.db 
	```
And that's it. You can save and close out of this file. We're ready to get everything we didn't just exclude hosted on GitHub.



####6. Initialize your New Repository
It's time to load our files to this new repository. Open up a Terminal window and navigate to your project folder. Once you're in this directory we first need to clone this blank repository we just created (we're basically referencing this GitHub location on our local computer). To do this run:

```
git clone https://github.com/username/username.github.io
```
Next we're going to tell Git that the directory we're in should be tracked by Git. Do this with:

```
git init
```
Now that Git knows what this location is, we need to add all of our files in to the Git management system by using: 

```
git add -A
```
This will add all the files in our directory to Git except those listed in our .gitignore file. Now that we've added the files we're going to *commit* these files to the main project. Run:

```
git commit -m "initial commit"
```
The portion in quotes explains what was changed in this commit. In this case, we're using the description 'initial commit' as this is the initial file load. So we've saved our changes, but this is just on your local computer, the last step is to *push* these changes up to GitHub. We do this using:

```
git push
```
With that your files have been uploaded to GitHub and we've got a site up and running. 

####7. Check Out your New Site
Open a browser and navigate to your newly created site at `username.github.io`. Cool, right?


---

##<a name="customdomain"></a>OPTIONAL: Custom Domain
Alright, so we've got a page that's live online, but wouldn't it be nice to link to this to a domain we already own. It's actually a pretty easy process. Let's do that.

####1. Edit CNAME File
The first think we'll want to do is edit one of the files that came with our site template. Open up your project directory in Finder and open up the `CNAME` file in your text editor. You'll see that this file already contains a domain name, you'll want to delete out what's in there and add your own domain name here. 

####2. Edit _config.yml File
Remember that the one field we didn't update in the config file earlier is the URL line, let's go back in to that file and update that with this new URL.

####3. Set Alias with your Domain Registrar
This part will vary based on your domain registrar, so I'm just going to post the official [GitHub instructions on setting up a custom domain](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages). 

####4. Commit changes to GitHub
Make sure these two files you edited are saved, then we're going to commit these changes to our GitHub repository. Run the following in order (this is almost the same process we ran earler to do the initial commit minus cloning the repository and initializing the directory):

```
git add -A
git commit -m "set up custom domain"
git push
```
####5. Check Out your New Site
Open a browser window and navigate to the domain that you just setup and you should see your new site. If you don't see it right away give it a few mins, GitHub warns that this may take 10 mins to take affect. Everything working? Good. 

---
##<a name="nextsteps"></a>Next Steps
If you made it this far, you now have a fully functional website live online, possibly using your own custom domain name. From here you need to build out the site itself. And remember, I'm at the same place you are, so here's what I'm thinking of next steps:

- Start posting! This is really the first post I've written. I'm deciding to start focusing on content now, and build along the way. I'm a chronic tweaker, so I know that if I start re-designing and building things out first I'll never get around to actually writing. 
- Delete out the stock filler posts.
- Modify the About page to reflect you.
- Create a Contact page.
- Create a Portfolio page.
- Update the other sidebar links (Download, GitHub Link).
- Add post categories or tags.
- Modify/rebuild website template (it's no fun to just use a stock template).
- Tweak posts template.

My goal is to continue to post tutorials similar to this as I continue to build out this site, but they'll probably be a little spaced out as I'm also currently working through the course materials that Epicodus provides free online at www.learnhowtoprogram.com and need to balance the two. If you're a beginner, from what I've see so far I highly recommend it. I'll also be posting about my experiences in that process so if that's interesting to you, stay tuned.

I know the odds are good that no one ends up reading this, but if anyone found there way here, hope this was helpful!



---