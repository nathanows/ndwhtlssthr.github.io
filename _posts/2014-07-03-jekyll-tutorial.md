As I mentioned in my last post, this blog is based on the Jekyll framework and hosted on GitHub Pages. As I was going through the process of choosing a platform I came across Jekyll and was intrigued by the concept of hosting directly on GitHub, which, as someone trying to immerse myself in the development ecosystem, is intimidating, but seemed like a great opportunity to force myself to get aquainted with GitHub. Still, functionality is obviously number one, and beyond being a platform I'm purely interested in, Jekyll is known to be fast and flexible. Oh yeah, and it's free! 

This tutorial covers step by step how to setup and publish a very simple Jekyll blog and publish it to GitHub Pages:

- [**Audience**](#audience): Who this tutorial is written for
- [**Goal**](#goal): What will be accomplished in this tutorial
- [**Setup**](#setup): Setting up the necessary development environment to install and run Jekyll
- [**Jekyll/Poole**](#jekyllpoole): Getting up and running using Jekyll and getting started with the Poole theme
- [**GitHub Pages**](#githubpages): Loading your page to GitHub Pages
- [**Custom Domain**](#customdomain): Linking your newly created site to your personal domain

---


##<a name="audience"></a>Audience
I'll preface this post by saying that I'm a total amateur, and therefore not really the standard Jekyll user. This means that there may be elements I won't (read: can't) fully explain. If you're starting at a higher level, everything should still work, but may not have the meaty context you desire (mmm... meaty context...). 

That said, I'm writing this because this is what I wished I could find as I was going through this process. It also starts from scratch, literally. I recently updated to new computer so I was starting from nothing. This isn't likely to be the case for most of you, meaning you can skip some of the initial setup, but if you're brand new this is the tutorial for you. 

The other plus if you're a beginner is that I'm going to explain things in a way that I, another beginner, understand them. One of the problems that I ran in to going through this process was the really quick dropoff in a lot of the instructions I found along the way. They start you off wading through the shallow end of the pool and about half way across you quickly realize it's not a steady decline as you fall off the 10 foot ledge directly in to the deep end. No lifeguards, nothing, and you're just left floating there in your waterwings... not here. (yeah, I know, this also means it's possible I'm giving you bad information... the process worked for me, take it or leave it)

---

##<a name="goal"></a>Goal
This tutorial will walk you step by step through setting up the development environment to install [Jekyll](http://jekyllrb.com/), creating a Jekyll blog using the [Poole](http://getpoole.com/), hosting your site on [GitHub Pages](https://pages.github.com/), and adding a domain alias so that you can link your GitHub Pages site to your own domain. 

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

##<a name="jekyllpoole"></a>Jekyll / Poole
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

---

##<a name="githubpages"></a>GitHub Pages

---

##<a name="customdomain"></a>Custom Domain


---