---
title: "Creating your Hugo website"
date: 2023-02-05T08:39:27-07:00
description: "Setting up your first Hugo website with the aether theme"
categories: [web]
toc: false
dropCap: true
displayInMenu: false
displayInList: true
draft: false
resources:
- name: featuredImage
  src: ""
  params:
    description: ""
    attribution:
      name: ""
      link: ""
---
Though I have created web pages for fun for a long time, I have not kept up with the pace of modern web development. The last time I updated my blog, I used Jekyll. Jekyll is still out there, but my blog was starting to look dated.

I wanted something modern looking without a lot of effort on my part. I decided to give [Hugo](https://gohugo.io/getting-started/quick-start/) a shot. I spent several months in decision paralysis trying to pick [a theme](https://themes.gohugo.io/). Though I am happy to include some photos, my blog is not going to be dominated by pictures. 

Eventually, I landed on [aether](https://www.joehutch.com/posts/aether-theme/). It looks clean, and it has some photos without being dominated by them. The theme is also responsive so it should look okay on phones.

## Getting Started

I followed the [quick start instructions](https://gohugo.io/getting-started/quick-start/) on the Hugo website.   

```shell
hugo new site website
cd website
git init
git submodule add https://github.com/josephhutch/aether themes/aether
echo "theme = 'aether'" >> config.toml
``` 

Instead of following the normal rules for starting the development server, I used 
```shell
cd ~/website 
hugo server -F -b "http://[internal ip address]" --bind=[internal ip address]
```
and then I set up a shell alias for this command so I would not have to remember it ever again.

I was underwhelmed. The sides of the giant blob at the top of my Hugo site were cut off. I wondered if I had downloaded an old theme that was broken.

## Setting up your site

I began editing my `config.toml` as [Joe Hutchinson](https://www.joehutch.com/posts/aether-theme/) specified on his site. I set the title to my name. In the params section of the file, I added: 
```shell
headdshotimg = "img/stellars_jay.jpg" 
headshotalt = "A picture of a stellar's jay from a hike to Hanging Lake" 
```

The top blob was still not complete. I tried to add a new post to fix that.  

```shell
hugo new posts/firstpost/index.md
```

Inside my index.md file, I updated the title to be something really long. That fixed the layout so the sides of the blob were not cut off. However, the stellar's jay was floating towards the center of the blob and not off to the right as you see it on Joe's site.

Inside my posts directory, I needed an `_index.md` This is the index page for the main site.

In that file, I wrote:   
```yaml
title: "I am Sepideh Miller"
date: 2023-02-05T09:25:39-07:00
description: "An Android developer and crocheter learning about new technology."
```

This set up the title and description inside the blob on the main page of the site.

I finally had the bones of my first site set up. 

One thing that I wanted to do that another person in the issues section of the GitHub for this theme also wanted to do was change the color of the blob. I poked around in the theme and learned that the blob was saved as an SVG. I was able to go in and mess with the color of the blob, but messing with the theme like that is not recommended because updates to the theme will lose these customizations. 

If you want to do ill advised things like I do, if you are at a terminal prompt in some flavor of unix, you can run this shell command:  
```
find . -name \*.svg
```

You will see two files with the word "blob" in their names like:
```shell
./themes/aether/static/img/home-blob-flip.svg
./themes/aether/static/img/home-blob.svg
```

In the files, you will find lines that say `fill="[HEX COLOR CODE]"` You can simply change the colors of those codes, and your blobs will be a different color.

A less hacky way to do this is to move copies of the SVGs to your own `static/img` directory outside the theme. Those won't be overwritten by theme updates. 
