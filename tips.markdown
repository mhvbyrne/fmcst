Front matter can be written using YAML or JSON
- Date and categories change the URL automatically
- Can also add custom front matter
- Have to include front matter for all

**posts**

- posts are for blog posts
- For each date post you need to assign a date - at the Front, needs to be delineated by hyphens, and use hyphens between words.

**site**

updates automatically, don't need to touch this.

**drafts**

can use jekyll serve -draft to serve up any posts in the draft folder

**pages**

Pages that aren't blogs - put them as a .md file
- YAML layout: page
- they won't normally have a title/date automatically
- you can also store these in folders

**permalinks**

Can use permalinks in YAML
```
permalink: "/my-new-url/test/test2"
```
- can also use categories ± year, month, day to determine the title
```
permalink: /:categories/:year/:month/:day
```
Can also use custom extension e.g. .html .php at the end
- You don't want to change the links otherwise any other links inside the website will break
- You should create a permalink for all posts.

**custom front matter**

Can automatically fill attributes by defining default front matter

can use defaults variable in YAML front matter.

```
defaults:
  -
    scope:
      path: ""
    values:
      layout: "post"
```

This will make all pages the post layout.

```
defaults:
  -
    scope:
      path: "post"
    values:
      layout: "post"
```
This will just make `_post` post layout.


**themes**
rubygems.org search jekyll-theme.
copy paste name of theme
and add it to `gem file`
Need to then ```bundle install``` in terminal
then in `_config.yml` change ```theme:``` to ```theme: "new-theme"```
then ```bundle exec jekyll serve```

There may be some errors
e.g. not having layouts available.
Look in the layouts folder on their github and

Your layouts might break after changing themes.
https://www.youtube.com/watch?v=NoRS2D-cyko

## New layouts

You can create new layouts in `_layouts` folder and it is best to write them in html.

Can use ```{{ content }}``` to put the content of the post in there.

Can rename them however you want.

Have have high level layouts, and lower level layouts. using YAML at the start.

```
---
layout: "higher-level-layout"
---

<h1>{{ page.title }}</h1>
{{ content }}
```
Can be best to keep lower level layouts simple

Can use {{ }} to create custom layouts which is the most powerful way.

Can go to https://www.jekyllrb.com/docs/variables to see all of the variables that you can use.

## Includes
Includes allows you to have separate html files for each part of your website and then add these into the layouts.

https://www.youtube.com/watch?v=HfcJeRby2a8

To include the include you use the code: ```/{% include name-of-file-you-want-to-include.html%}```

Makes it much easier to read, and also stuff to be applied to everything.

## Looping through content - navigation bar

`infex.md` file
```
{% for post in site.posts %}
  <li><a href="{{ post.url }}">{{ post.title }}</a></la> <br>
{% endfor %}
```

```
{% for post in site.pages %}
  <li><a href="{{ page.url }}">{{ page.title }}</a></la> <br>
{% endfor %}
```
Can use a for loop to list For each post in the post folder or pages.

# conditional - IF statements

```
{% if page.title == "My First Post"%}
  This is the first post
{% else %}
  ...
{% endif %}
```
Can also use else, or, and

Can use this to colour link text in navigation bar.

https://www.youtube.com/watch?v=iNZBEki_x6o

Can make a navigation bar using loops
```
{% for post in site.posts %}
  <li><a href="{{ post.url }}">{{ post.title }}</a></li><br>
{% endfor %}

{% for post in site.pages %}
  <li><a href="{{ page.url }}">{{ page.title }}</a></li><br>
{% endfor %}
```

Don't have to use the links though can just cy

## Datafiles
- yaml
- JSON
- CSV

`_data` file

```
{% for person in site.data.people %}
  {{ person.name }} is a {{ person.occupation }} <br>
{% endfor %}
```

Good for keeping front matter cleaner, and to act as a mini database.

## static files
Any file that doesn't have front Matter. e.g. photos, php files.

Can store these in a folder called something like assets.

```
{% for file in site.static_file %}
  {{ file.path }}
{% endfor %}
```

Can also use ```file.extension``` or ```file.basename``` to separate file type (e.g. jpeg) and file name without extension

Can give extensions front matter.

To do this can put images in an image folder, and in `_config.yml` file, can use the following code.

```
defaults:
  - scope:
      path: "assets/images"
    values:
      image: true
```

Whenever changing config need to restart local hosting.

Can then use this to loop through

# custom domain name
Need to put baseurl custom domain name in config file
