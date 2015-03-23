---
layout: post
title: "Vim as an IDE"
excerpt: "Vim as an IDE with Groovy & Grails"
tags: [vim,grails,groovy,ide]
comments: true
---

GGTS or STS or Eclipse or any other IDE for that matter is too bulky and slows your machine. But more importantly if you
are someone like me who would rather use a keyboard than a mouse then using vim instead of an IDE is going to be even
more fun. The speed with which I can manipulate files, check for syntax, format code and use information from git version
history is pretty slick.

## Some of the features that are absolutely fabulous within GGTS or STS include
1. Content Assistant: suggests auto-completions as we type.
1. Get declaration/implementation of variable/method in a single click (ctrl + click)
2. Auto import and fix imports
3. Git compare/commit files
4. Searching within a project
5. Renaming files, methods
6. Project specific settings

## Let us look at the alternatives available for each of these and how well one can do these things in Vim

### Get declaration/implementation of variable/method in a single click (ctrl + click) and code completion
This can be done using Ctags, Tagbar and few .vimrc configurations.

#### Ctags
For Mac OS X
`brew install ctags`

For Debian-based systems 
`sudo apt-get install exuberant-ctags`

For Red Hat based systems
`sudo yum install ctags`

#### Tagbar
Add the following to your .vimrc (Installing using [vundle](https://github.com/gmarik/Vundle.vim))
`Bundle majutsushi/tagbar`

#### Keyboard shortcuts to find function and class definitions
Ctrl+] - go to definition
Ctrl+T - Jump back from the definition.
Ctrl+W Ctrl+] - Open the definition in a horizontal split

Add the following to .vimrc

	map <C-\> :tab split<CR>:exec("tag ".expand("<cword>"))<CR>
	map <A-]> :vsp <CR>:exec("tag ".expand("<cword>"))<CR>

Read more about ctags [at](http://andrew.stwrt.ca/posts/vim-ctags/).

### Git compare/commit files.
Git support is pretty neat and the author of the plugin is not wrong in claiming this to be the best git wrapper of all 
time. Git grep, move, rename, checkout, diff and more. More info at [github](https://github.com/tpope/vim-fugitive).

### Searching within the project and optionally replace what matched or perform other operation
You can use git grep using fugitive again

	:Ggrep [args]

The search results are listed in the quickfix list. Any operations can be performed on this list using Qdo command
available in a neatly packaged plugin [Qargs](https://github.com/henrik/vim-qargs), inspired by a 
[stackoverflow answer](http://stackoverflow.com/questions/5686206/search-replace-using-quickfix-list-in-vim/5686810#5686810).

	:Ggrep findme
	:Qdo %s/findme/baz | update

This does require you to type the search string twice but does the job. The raw speed you get with vim for searching and
other tasks is totally worth it.

### Renaming a file
Find and open a file

	:CtrlP
	<filename>

Locate the file in [NerdTree](https://github.com/scrooloose/nerdtree) a file browser plugin

	:NerdTreeFind

Once you located the file, press `m` to modify the filename

### Auto import and fix imports
Again using vundle install the [grails import plugin](https://github.com/sjurgemeyer/vim-grails-import)
	
	Bundle 'sjurgemeyer/vim-grails-import

### Project specific vim config

`set exrc` at the top of your .vimrc
`set secure` at the very end of your .vimrc

[More about project specific settings](http://andrew.stwrt.ca/posts/project-specific-vimrc/)


