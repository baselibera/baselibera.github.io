---
layout: post
title: "Octopress: first customizations"
date: 2015-01-04 21:53:13 +0100
comments: true
categories: 
- Octopress 
- configuration
- template
- layout

---

## Configuration files

|Filename     |role    |
|-------------|--------|
| _config.yml | Main config file, here there Title, Subtitle, email, date format and other frontend settings|
| Rakefile    | Deployment configuration, need to modifiy especially with rsync |
| config.rb   |  |
| config.ru   |  |


### Rakefile properties

|Property|Default value|Description|
|------------|----------|-----------|
|**public_dir**      | "public"    | compiled site directory|
|**source_dir**      | "source"    | source file directory|
|blog_index_dir  | 'source'    | directory for your blog's index page (if you put your index in source/blog/index.html, set this to 'source/blog')|
|**deploy_dir**      | "_deploy"   | deploy directory (for Github pages deployment)|
|stash_dir       | "_stash"    | directory to stash posts for speedy generation|
|**posts_dir**       | "_posts"    | directory for blog files|
|**themes_dir**      | ".themes"   | directory for blog files|
|new_post_ext    | "markdown"  | default new post file extension when using the new_post task|
|new_page_ext    | "markdown"  | default new page file extension when using the new_page task|
|**server_port**     | "4000"      | port for preview server eg. localhost:4000|

Here are also defined **tasks** for **Jekyll**.
	
	rake list
or

	rake --tasks
	
to show all tasks


## Header, Navigation, Footer

`/source/_includes/custom/`

At this path you can find customizable files that preserve contents against update.



## Styles & Color

In `/sass/base/_theme.scss¡ are are defined all colors.

In `/sass/custom/` directory we can find files to override default settings. Changing these files we can obtain portable styles and color customization:

|File|Comment|
|----|-------|
|`_colors.scss`     | Override colors in `base/_theme.scss` to change color schemes|
|`_styles.scss`     | It's empty and easily override any style (last in the cascade)|

For example: to change code solarized schema from dark (default) and light, in the `_color.scs` modifiy:

	$solarized: light;

[Here](http://blog.alestanis.com/2013/02/04/octopress-and-the-twilight-color-scheme/) an article for the twilight code color schema.

To help with colors some styles are defined relatively to some main color, for example we have:
	
	$nav-bg: #ccc !default;
	...
	$nav-bg-back: linear-gradient(lighten($nav-bg, 8), $nav-bg, darken($nav-bg, 11)) !default;
	$nav-color: darken($nav-bg, 38) !default;
	
So if we modify `$nav-bg` color value in customization file, others are automagically calculated with sass functions. This amazing functions behave too SASS and we can find API definition [here](http://sass-lang.com/documentation/Sass/Script/Functions.html). Or from beginning [here](http://sass-lang.com/documentation/). Enjoy!


This [link](http://hslpicker.com/) for an online color chooser tool.


## Fonts

In this directory there's main customization files: `/octopress/source/_includes/custom`:
Here there is `head.html`, it contains font definition from [Google](http://www.google.com/fonts/) (something very special to choose a font). Defualt is:

	<!--Fonts from Google"s Web font directory at http://google.com/webfonts -->
	<link href="//fonts.googleapis.com/css?family=PT+Serif:regular,italic,bold,bolditalic" rel="stylesheet" type="text/css">
	<link href="//fonts.googleapis.com/css?family=PT+Sans:regular,italic,bold,bolditalic" rel="stylesheet" type="text/css">

I have chose a font and I have added to HEAD definitio. Because all defined fonts are loaded with page its better to remove fonts unused. I added this:

	<link href='//fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,400,300,700' rel='stylesheet' type='text/css'>

Now you must modify CSSs in /sass/custom/_fonts.scss.

<http://octopress.org/docs/theme/template/>

## Layout
All concern layout is resumed in 
In `/sass/base/_layout.scss` are defined Responsive layouts defaults.

In `/sass/custom/_layout.scss - We can change settings for easy customization, overriding settings for base/_layout.scss and to change the layout.

Here for example we can indent correctly lists items, that by default have text aligned with content text (wrong IMHO), setting to true:

	$indented-lists: true; 


