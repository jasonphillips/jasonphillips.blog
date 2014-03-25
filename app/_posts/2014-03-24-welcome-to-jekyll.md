---
layout: post
title:  "Jekyll via Yeoman"
date:   2014-03-24 17:40:56
categories: jekyll update
comments: true
---

I've been using [Yeoman][yeoman] lately for SPA projects in [Angular.js][angular], but have typically favored [Middleman][middleman] for the generation of static sites that contain multiple pages. Middlman's simple integration of the `Data` folder and `proxy` declarations offers a compellingly clean way to build a set of pages from a **YAML** table of contents, which has allowed non-technical users in my office to broaden their scope from editing basic markdown content to now updating sitemap and navigation trees easily. It's remarkable how quickly a markup-free syntax can overcome the usual barriers that prevent turning over the keys to our content to the right hands. 

But for my own blogging purposes, I'm finally jumping into [Jekyll][jekyll] for its more blog-centric features, and Yeoman has made the process a pleasure with a host of convenient grunt tasks ready to go. 

But the combination of these generator tools was admittedly not an intuitive match. Isn't Yeoman a generator all of its own that should be categorized alongside Middleman and Jekyll, and isn't it therefore a bit odd to wrap one generator (Jekyll in this case) with another? 

That being said, the great benefits of Yeoman in this case are the quicker start enabled by scaffolding and the generation of a Gruntfile that contains the vast majority of handy functions you'd end up handling by other means. And with a bit of [grunt-bower-install][gruntbower] thrown into the mix, I can finally add front-end packages in seconds on the command line and see them automatically populated into my templates. Very convenient. 

The Gruntfile additions required in order to add bower to your standard Yeoman-scaffolded Jekyll blog are quick. In your `config` section: 

{% highlight ruby %}
    bowerInstall: {
      target: {
        src: '<%= yeoman.app %>/_layouts/default.html',
        ignorePath: '<%= yeoman.app %>/'
      }
    },
{% endhighlight %}

Then be sure to add `bowerInstall` to your relevant grunt tasks (serve, build) near the top of the list. Lastly, just insert the wrapping comments into your chosen location in the main template.

{% highlight html %}
<!-- somewhere in <head> -->
    <!-- bower:css -->
    <!-- endbower -->
  
    <!-- bower:js -->
    <!-- endbower -->
{% endhighlight %}

These will be filled with the relevant pieces of any bower packages installed. Having worked with Middleman and its Ruby-based methods of automating asset management (Sprockets-based) at length, I'm somewhat pleasantly surprised by how easily Grunt tasks can be made to accomplish the same goal, leaving the Ruby site generator to stick to what it handles best, and avoiding the need for complex interaction with Rake.


[jekyll]:    http://jekyllrb.com
[angular]:   http://angularjs.org/
[yeoman]:    http://yeoman.io/
[middleman]: http://middlemanapp.com/
[gruntbower]: https://github.com/stephenplusplus/grunt-bower-install
