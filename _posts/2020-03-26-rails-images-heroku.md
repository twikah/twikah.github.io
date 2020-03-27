---
postHero: /images/rails.jpg
title: Rails, images and Heroku
categories: work
tags: [web-development, ruby, heroku, asset-pipeline]
---

Having finished the bootcamp and while looking for a new junior web dev job, I'm
keeping myself busy with code challenges and a pet project.

<img class="pull-left" src="/images/heroku-meme-asset-pipeline.jpg"
     alt="Heroku meme" style="width: 170px;">

I recently came across an issue when I added an image in my stylesheet (scss).

I added a background-image with a relative path, indicating a file in my
/app/assets/images directory.

This was good and well, until I deployed and then my image disappeared!

<br>

The below 👇 worked out fine on my localhost but NOT on Heroku:

<br>

```css
.callout {
  background-image: url("footer-callout.jpg");
  background-size: cover;
  background-position: center;
  height: 200px;
}
```

<br>

It took me some time to figure out how to get the image to display in production.
For an image located in /app/assets/images/footer-callout.jpg, assuming that it
is a CSS background image, you want to reference it as:

<br>

```css
.callout {
  background-image: asset-url("footer-callout.jpg");
  background-size: cover;
  background-position: center;
  height: 200px;
}
```

<br>

I looked this up on [Rails guides](https://guides.rubyonrails.org/asset_pipeline.html#css-and-sass).
I'm just posting it here to have a clearer example and also for future reference.
And who knows, maybe this helps someone else!

I recently also heard from a friend and fellow Le Wagon alumni that we should
replace any images with the ```.jpeg``` extension with ```.jpg``` as Heroku
won't display the former.

<br>

What can I take from this? Deploying to Heroku can be tricky, so do it as often
as possible. This way, any issues will be sorted more easily.











