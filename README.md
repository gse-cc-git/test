# Tiddlywiki-NodeJS-Github-Template

Default wiki template for [TidGi-Desktop](https://github.com/tiddly-gittly/TidGi-Desktop), an App that can generate template wiki on one-click.

Knowledge base Template, with advanced filter search and faceted data aggregation.

[onetwo.ren/wiki](https://onetwo.ren/wiki) is an example of this template. And [tiddly-gittly.github.io/Tiddlywiki-NodeJS-Github-Template/](https://tiddly-gittly.github.io/Tiddlywiki-NodeJS-Github-Template/) is deployed example of this repo. (There are some optimization to make this demo readonly, and being not downloadable, so its size is almost as small as a GIF picture.)

Downloadable HTML is at [tiddly-gittly.github.io/Tiddlywiki-NodeJS-Github-Template/index-full.html](https://tiddly-gittly.github.io/Tiddlywiki-NodeJS-Github-Template/index-full.html), which contains edit related plugins, and will be slightly bigger (a size of a tiktok video.)

This repo used to contains the wiki backup data and script to start a local wiki server on MacOS on start up. It is now deprecated, and no money to maintain, now [TiddlyGit-Desktop](https://github.com/tiddly-gittly/TiddlyGit-Desktop) is preferred. Old version can be found at the [feat/auto-start branch](https://github.com/tiddly-gittly/Tiddlywiki-NodeJS-Github-Template/tree/feat/auto-start). Contribution to it is welcome.

## Setup

### Replacing Notion and EverNote with TiddlyWiki as a personal knowledge management system
Note: I'm working on a zero-configuration TiddlyWiki desktop APP [tiddly-gittly/TiddlyGit-Desktop](https://github.com/tiddly-gittly/TiddlyGit-Desktop), feel free to star and watch (click Watch Release Only to get a push alert on Github when I release a new version)

If you have any questions, you can join the TiddlyWiki Enthusiasts QQ group 946052860, or use Bing to search the WeChat group Attention and Knowledge Management to join my knowledge management community.

I used to use Impressions for many years, filled with bits and pieces of content collected from all over the place, such as [what is a "Communist Chinese accent"?](http://www.zhihu.com/question/19687065) - I also used Notion for a few years to write down to-do lists and memo biographies of people I knew. I also used Anki for a long time to put bits of knowledge into my head, such as English words, mathematical formulas, algorithm routines, etc. I also learned about Roam Research, which increases the discoverability of notes through two-way links.

But none of these tools seem to focus on two concepts that are key to me: 'meta-information' and 'automation'. In my view, only an automated knowledge management system that adequately preserves meta-information can be called 'good to use'.

In this way, there seems to be an impossible triangle of personal knowledge management systems: free - good - good looking, and only two of these can be had. Notion costs money, impressions are not good, systems such as Quip and FeiBook are not for individuals ......

[TiddlyWiki](https://tiddlywiki.com/), however, seems to break this impossible triangle by introducing a fourth element: it's free, it works well, it looks good, and the only downside is that you need to be able to put the blocks together to make it look the way you want. For those with the ability to work with their hands, it's perfect.

Let me start by talking briefly about what I think is beautiful, free and powerful about TiddlyWiki.

### The beautiful TiddlyWiki

One of the main reasons I liked Notion before was its beautiful design, so when I configured my own wiki, I opened the notion web version and copied its stylesheets using the developer tools, choosing the best ones.
Adding custom styles

Adding a `$:/tags/Stylesheet` tag to a Tiddler allows it to be added to the wiki's stylesheet when the wiki is launched. For example, I've pasted in a custom link style to fit Notion's link style, which changes colour discreetly when the mouse hovers, giving it a minimalist look.

I've also added a `backdrop-filter` to add a glassy effect to various places. I'll redesign it myself to look the most popular when it's not.

### Free TiddlyWiki

When you drag a lot of images into TiddlyWiki, the blog you post via now.sh can get bigger and bigger. So I reduced the size of the generated HTML by changing the link to the image file to point to an image on Github.

This is the equivalent of using Github as a free, unlimited image bed, and as long as you don't get too many views, you won't get a banning email.

### Owning the data

When you open my wiki, you can edit it as much as you like. This will only change the cached wiki content in your browser and will not affect the local content on my computer or my backups on Github.

How does TiddlyWiki persist content elsewhere after it's changed in the browser cache? Saver (a coarse-grained saver) and SyncAdaptor (a fine-grained synchroniser).

There is an official GitHubSaver plugin that allows you to save a modified wiki directly to Github as an HTML file backup on mobile and desktop web pages after filling in a Github Token. After launching the NodeJS version of the wiki on the desktop, a TiddlyWebSyncAdaptor is synchronising the modified Tiddler to the filesystem.

In the future, we can use custom syncadaptors such as [solid-tiddlywiki-syncadaptor (WIP)](https://github.com/linonetwo/solid-tiddlywiki-syncadaptor) to save data wherever we want, without being tied to a big company or having to buy a membership service like we do with Impressions. We are free to customise how and where the data is stored.

### The powerful TiddlyWiki

I focus on what a piece of information is, where it comes from and where it is going to ...... aka information about the information: labels, source spectrum, associations. Our brains hold a lot of other information related to a piece of information, and if a knowledge management system also holds this meta-information, it can store knowledge in a form that is very close to our brains, making it easier to find and use it.

Automation would reduce much of the effort of copying and pasting text, and would also allow information to be aggregated in a variety of ways, appearing in more places and being more easily found.

#### Non-linear writing

As I conceive a piece of writing, my mind often wanders through a web of memory, piecing together many pieces related to the topic into the article in my head. However, the brain and the knowledge management system are out of sync, and much of the fragmented content does not exist in the machine, but only in the brain. If you enter the fragments into the computer first and then go back and continue to roam through your memory, you risk interrupting the roaming thoughts and eliminating the inspiration that has just come to you.

A better approach would be to first take up the pit with a link

Once the entire article is framed, go back and click on the "Allow automatic code sync with git-sync script" button to create this fragmented note, enter the details into it, and then TiddlyWiki will automatically fill the fragmented content into the pit you just occupied.

### Refactoring: improving the design of existing documents

The benefits of content fragmentation are many.

*    There may be multiple notes that refer to the same content, refactor this out and then automatically fill in multiple pits using Transclusion rather than filling in the pits by copying and pasting. This way, if you want to make changes later, you can change one place instead of looking for all the places to change, and you won't miss any changes.
*    You can add paragraph-level meta-information, e.g. you can put a paragraph from an article on topic A into the folder for topic B because it talks about topic B. This makes it easy to find this fragment as a reference when writing an article on topic B in the future.
*    When searching for references via full-text search, you don't have to read large passages, you can just look at the smaller passages to see if they are of value to you at the moment

Since the benefits of content fragmentation are so great, we would certainly like to break it down a bit when copying and pasting content from elsewhere into TiddlyWiki.

This simple refactoring can be done automatically using the text fragmentation plugin, or manually by selecting the parts that you might use later and adding the appropriate tags (equivalent to putting them in a folder with the same name).

## Deployed to Github Pages

Automatically.

## NPM Scripts

`npm build`: pack tiddlywiki data to a HTML file

## Shell Scripts

[scripts/build-wiki.js](scripts/build-wiki.js) will actually pack tiddlywiki data to a HTML file

## Credit

Scripts are inspired by [DiamondYuan/wiki](https://github.com/DiamondYuan/wiki)
