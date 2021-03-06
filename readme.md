### Status
[![Build Status](https://travis-ci.org/mohamed-aziz/simplegen.png)](https://travis-ci.org/mohamed-aziz/simplegen)

## simpleGen

simpleGen *is a simple static website/blog generator* that just does what it is supposed to do no more and no less.

### The philosophy behind simpleGen

I built simpleGen beceause I needed something dead simple to make my static sites, I could have used something like pelican or jekyll but I think they are bloated so hacking on the code will be some much harder, simpleGen is about 400 lines of python code.

simpleGen does not do things it not intended to do, instead it does just what a sane person wants from a site generator, TO GENERATE THE DAMN MARKDOWN (or whatever markup language you use), simpleGen does not provide solutions to deploy the static content, or providing a development server, that is another problem that I think does not overlap with the basic functioning of a static website generator.

### Installing simplegen.

You can install simpleGen from the Python package index using pip (I maintain this package).

	$ pip install simplegen

or you could get it from github using (using the https protocol) using

	$ pip install git+https://github.com/mohamed-aziz/simplegen.git

you also can install the development version from the development branch using

	$ pip install git+https://github.com/mohamed-aziz/simplegen.git@development

Grab a coffee (or two if you have slow connection).

And then you want to initialize the site config, so use:

	$ initsite input_dir output_dir

A config file with name sconfig.py will be generated, edit that with what suits you and your theme
you are using or planning to make.

then you can write you content in markdown in the input_dir, then run:

	$ makesite

to actually generate your content.

deploying your website is up to you, I myself use git submodules and github pages.


### Config options

You can define any option really to use in your template, but these are the ones that simplegen knows.

Option name | Type | Default Value | Description
--- | --- | --- | ---
CONTENT_DIR | String | "content/" | From where to get the input
OUTPUT_DIR | String | "output/" | Where to save the output
PAGINATOR_MAX | Int | 20 | How many articles per page
MINIFY_HTML | Boolean | False | Minify the ouptput HTML
ASSETS_PATH | String | None | The path of the user assets


### Making themes

simpleGen uses [jinja2](http://jinja.pocoo.org/) as its templating language so making themes should be fairly easy.

[This is the theme I made for my technical blog](https://github.com/mohamed-aziz/simplegen-hyde)

and this is my sconfig.py file:

	CONTENT_DIR = 'content/'
	OUTPUT_DIR = 'output'
	PAGINATOR_MAX = 5
	SITE_URL = 'https://mohamed-aziz.github.io/technical-blog'
	DESCRIPTION = 'Mohamed Aziz Knani techincal blog, follow me @moonflock.'
	SITE_TITLE = 'Mohamed\'s blog'
	LINKS = [
		('Home Page', 'https://mohamed-aziz.github.io/'),
		('<i class="fa fa-github" aria-hidden="true"></i> Github', 'https://github.com/mohamed-aziz'),
		('<i class="fa fa-google-plus" aria-hidden="true"></i> Google plus', 'https://plus.google.com/+mohamedazizknani'),
		('<i class="fa fa-envelope" aria-hidden="true"></i> medazizknani@gmail.com', 'mailto:medazizknani@gmail.com')
	]


### Deploying

Many people like to use the github pages service mainly because it's free and it uses git.

I also do that for my personal website.

So for deploying I have written this shell script:

	#!/bin/sh

	makesite
	cd output
	git add .
	git commit -m "New deploy"
	git push origin master
	cd ..
	cd content
	git add .
	git commit -m "New version"
	git push origin master
	cd /home/mohamed/programming/mohamed-aziz.github.io/technical-blog
	git pull
	cd ..
	git add technical-blog
	git commit -m "New deploy"
	git push origin master

My folder looks like this:

	.
	├── build.sh
	├── content
	│   ├── somefile.md
	│   └── someotherfile.md
	├── output
	│   ├── somefile.html
	│   ├── someotherfile.html
	│   └── index.html
	└── sconfig.py


I also version control my markdown files which is also nice.

If you don't like git (or versioning) just write some fabric file to do the deploy for your site.

### Testing

You can test the code using:

	$ mktmpenv
	$ git clone --recursive https://github.com/mohamed-aziz/simplegen.git
	$ cd simplegen
	$ python setup.py test


### Get in touch

If you like simpleGen and use it for your website, I would be pleased if you let me know, also pull requests are welcome :)


### License
[![GNU GPLv3 Image](https://www.gnu.org/graphics/gplv3-127x51.png)](http://www.gnu.org/licenses/gpl-3.0.en.html)

SimpleGen is Free Software: You can use, study share and improve it at your
will. Specifically you can redistribute and/or modify it under the terms of the
[GNU General Public License](https://www.gnu.org/licenses/gpl.html) as
published by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.


### Todo

- [X] Write tests.
- [X] Make a paging system.
- [X] Transform it into a package.
  - [X] Upload it to pypi.
  - [X] Use armin's click.
- [X] Support Python3.
- [X] Add tags support.
