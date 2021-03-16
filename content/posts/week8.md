---
title: "Week 8"
date: 2021-03-02T17:56:51-04:00
draft: false
---
Time: 12 hours

I forgot to write something up for this exercise so I'm going back retroactively. I was ill for most of lask week (got tested and it wasn't COVID, so it must have just been a horrible cold or the flu--my roommate works at a hospital so who knows) but luckily had started working on this assignment the day after it was introduced. I've worked with Hugo successfully in the past but not without difficulties and assumed (correctly) that Jekyll would be just as difficult.

Installation was a mess and took me several hours and several attempts. I found that my computer was apparently too old to download Chocolatey (something I'd learned in the past but must have forgotten) and had to find a work around to download Ruby Gems. After finding a work around (and ensuring that it wouldn't crash my computer or secretly deliver any viruses), I was able to get Ruby Gems to work so that I could install and deploy Jekyll.

On my first attempt, I ended up with a GitHub Pages website that just would not connect with Jekyll. Also, for that site, I really didn't want the blog format that Jekyll loves to use so much, so, in the end, I abandonned it. 

I tried a second time in my class GitHub repository. I ran into the same error and learned that I needed access to my repo settings in order to deploy Jekyll. I am just now realizing that this is when the illness kicked in and I never attempted to try this again on a repo I could control (although I could control the repo I used for my first attempt). I created the repo and must have fallen asleep. More to come soon!

EDIT:

Coming back later to add some more. This took me a *long* time and it was incredibly stressful. Try as I might--over the course of two weeks--I could not figure out how to get the Jekyll site to connect to my GitHub pages site, so I decided to switch to Hugo. I've used it in the past (unsuccessfully) and figured I'd give it a try. I spent nearly a week figuring out how to create a Hugo site, install a theme, populate the site with content, and then host it on Netlify. The Netlify part was the most difficult.

I figured out that there were several steps missing from all of the tutorials. I figured I would recount some of the necessary steps here for myself and others:

1. After you are satisfied with your Hugo site, navigate to the directory that it's hosted in. For me, that was ```C:\Hugo\cm21```. From there, run the command ```hugo``` to create a ```\public``` folder.
2. Move the ```\public``` folder as well as the ```\content``` folder into the GitHub repo (make sure it's public). Also copy the ```config.toml``` file into the main GitHub repo folder. For me, that was ```C:\Users\Suzi\Documents\GitHub\cm21```. Now, that folder contains the ```config.toml``` file, the ```\content``` folder, and the ```\public``` folder all copied from the main Hugo site folder.
3. Commit these changes to the GitHub repo. Using a submodule command, clone the git of the theme into your GitHub reposity. The command should be in the documentation for the theme you're using. For me, it was ```git submodule add https://github.com/jacobsun/edidor```
4. Make sure the site runs on your local server. If so, deploy a build in Netlify with the build-command ```hugo``` and the directory set to ```public```. Make sure to update the version of Hugo you're using and set the correct base URL in the config.toml file.

Hopefully all of that should work. For me, it created [the site I'm using for this class](https://cm21.netlify.app) and I also made [a site to host the samples produced by SAIGE](https://saige.netlify.app).