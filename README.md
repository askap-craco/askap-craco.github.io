## Website Maintainer Notes

This website is developed using [jekyll](https://jekyllrb.com/), and [minimal mistakes theme](https://mmistakes.github.io/minimal-mistakes/)

### Website Basic Configuration

All website configurations are stored under `_config.yml`. Generally, you don't need to change anything there. 

### General Syntax

You can create a new webpage using either `HTML` file or `MarkDown` file. Each file contains two part
```
---
<!-- defining page variable  -->
layout: single
classes: wide 

author_profile: false

<!-- you can define your variable here  -->
---

<!-- code for the webpage itself  -->
```
All webpage files are stored under two directories - `_pages/` and `_posts/`. Webpages under `_pages/` are typically the ones that don't change often, while those under `_posts/` are usually used for posting news etc.

### List of useful layout, include and data files

- `_includes/footer.html`: The footer for all webpages
- `_data/navigation.yml`: breadcrumb navigation on the top right

### List of pages

Andy created the following pages as a starting point

<table>
  <tr>
    <thead>
      <th>page</th>
      <th>description</th>
    </thead>
  </tr>
  <tr>
    <td>survey.md</td>
    <td>Detailed scientific description of our two main surveys - CRAFT/ICS and CRACO</td>
  </tr>
  <tr>
    <td>publication.md</td>
    <td>Place where we put our latest results and also a full list of publications (compiled using <a href="https://github.com/andycasey/ads">ADS python package</a>)</td>
  </tr>
  <tr>
    <td>news.md</td>
    <td>Place where we can put any news. It will also show a list of three (user-defined) latest posts grouped by different tags as well</td>
  </tr>
  <tr>
    <td>discovery.md</td>
    <td>Place where we can put a list of our discoveries - might also be useful to have a google sheet link there.</td>
  </tr>
  <tr>
    <td>media.md</td>
    <td>All outreach, media releases our collaboration have made</td>
  </tr>
  <tr>
    <td>team.html</td>
    <td>Our collaboration members (you can change to markdown, which is easy to have a table of content on the right automatically)</td>
  </tr>
  <tr>
    <td>search.md</td>
    <td>This is a super useful function provided by minimal mistakes theme, which allows us to search all posts</td>
  </tr>
</table>

#### How to edit them?

##### `publication.md`

I suggest using <a href="https://github.com/adsabs/ads-examples/">ADS Examples</a> and <a href="https://github.com/andycasey/ads">ADS</a> to compile it automatically.

##### `news.md`

The following codes are used for generating the three latest posts from different tags, usually, we don't need to change it
```
{% for tag in site.tags %}
  <h1 class="archive__subtitle">{{ tag[0] }}</h1>
  <font size="4">
  <ul>
    {% for post in tag[1] limit:3 %}
      {% include archive-single.html type=entries_layout %}
    {% endfor %}
  </ul>
  </font>
{% endfor %}
```

If you want to include some exciting news, you can put it before this block of code (using `markdown`)

To include videos, you can use the normal html `iframe` tag. Or for some popular platforms, you can use something like
```
{% include video id="<YOUTUBE_VIDEO_ID>" provider="youtube" %}
{% include video id="<VIMEO_ID>" provider="vimeo" %}
```

##### `media.md`

Add or change the `feature_conversation` variable on the top.
```
  - image_path: # path to the image (might be useful to change the image aspect ratio manually so that the page looks nicer)
    alt: # not super needed
    title: # the title of the text (sometimes I set it to nothing)
    url: # the URL for the button
    excerpt: # message shown below the title (for a linebreak, you can use `<br>`)
    btn_label: # text on the button
    btn_class:  # This just controls the style of the button
```
The following code is how we put them in the page
```
<div style="margin-left: 8%; margin-right: 8%;">
    {% include feature_row id="feature_conversation" %}
</div>
```
You can also define other variables as well.

##### `team.html`

Similar to `media.md`, define variable called, for example, `team_swin` on the top. Here are some examples
```
 - image_path: assets/images/team/example_photo1.png
   excerpt: AAAA BBBBB CCCC <br> I am interested in finding FRBs
   url: "https://www.swinburne.edu.au/"
   btn_label: "Personal Webpage"
 - image_path: assets/images/team/example_photo1.png
   excerpt: DDDD EEEEE FFFF <br> You can check my [personal webpage](https://www.swinburne.edu.au/)
 - image_path: assets/images/team/example_photo1.png
   excerpt: Swinburne
```

### Posts

All posts are under `_posts` folder - you can create as many levels of folders as you like, just make sure that all posts have unique names (even though they are under different folders)
The format of the post follows `YYYY-MM-DD-TITLE.md` or `YYYY-MM-DD-TITLE.html`

An example template for this is
```
---
layout: newspost
title:  "ASKAP Detection of a repeating FRB"
tags: "FRBs" # if you want to put multiple tags, use space to separate them, for example, "FRBs HostGalaxies"

author: "Keith Bannister (CSIRO Space & Astronomy) on behalf of the ASKAP/CRAFT collaboration"
---

Your main text here (just use markdown or html to edit it)

```
