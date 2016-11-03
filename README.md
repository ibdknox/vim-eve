# Vim syntax highlighting and more for use [with Eve](http://witheve.com/).

This is a plugin to try and make writing programs [with
Eve](http://witheve.com/) more comfortable in (neo)vim. It's currently hosted
[on Github](https://github.com/frankier/vim-eve). Currently it has the
following features:

 * Syntax hightlighting;
 * Indentation;
 * Folding;
 * Automatic insertion of code fences.

Only syntax hightlighting and indentation are enabled by default. All other
features are configurable and opt-in. I highly recommend taking a look at the
options in this document to make sure you get the most out of this plugin.

## Installation

It's easiest if you use a plugin manager. My favourite is
[vim-plug](https://github.com/junegunn/vim-plug). If you're also using
vim-plug, just add:

    Plug 'frankier/vim-eve'

to ~/.vimrc or ~/.config/nvim/init.vim, restart (neo)vim and run :PlugInstall

## Highlighting

There is one option for configuring highlighting currently:
`g:eve_highlight_markdown`. By default Markdown sections will be highlighted as
comments. You can set this option to highlight them as Markdown. This isn't the
default because it provides poor contrast between the comments and the code.

If someone knows a good way to get the best of both worlds then I'm interested.
See the issues on Github.

## Folds

This plugin can fold your code in a few ways.

For people, like myself, who don't usually fold code, there is a mode which
only folds the empty Markdown blocks which tend to appear in Eve programs which
don't use literate programming. These folds are no indended to be interacted
with, but are rather just intended to save vertical space. This mode is enabled
by setting `g:eve_fold_empty` to 1.

The other options are to generate folds for code blocks so that only Markdown
is visible by default. This can be enabled by setting `g:eve_fold_code` to 1.

## Automatic insertion of code fences

This plugin can try and insert code fences, `\`\`\``, the characters which
delimit Eve and markdown blocks automatically for you as you type. Since this
behaviour can be quite invasive, it's opt-in. You can enable it by setting
`g:eve_insert_code_fence` to 1. There are 3 types of code fence insertions
possible.

 1) Eve block => Markdown block (abbreviated e2m)
 2) Markdown block => Eve block (abbreviated m2e)
 3) Eve block => New Eve block (adds an empty Markdown block, abbreviated e2e)

(The last type, when combined with `g:eve_fold_empty` is particularly nice for
writing non-literate Eve.)

Each type of fence is only inserted if your current line is preceeded by a
certain number of blank lines. An m2e or e2e fence is inserted when you finish
typing `search`, `bind` or `commit` in a Markdown block or in an Eve block
respectively. An e2m fence is inserted when you start a line with something
other than `search` in an Eve block.

The number of blank lines for each fence is configurable with
`g:eve_TYPE_blanks` where TYPE is one of the abbreviations above. For Eve to
Eve fences, new Eve blocks starting with `search` can be special cased to
require a different number of blank lines using `g:eve_e2e_blanks_search`. The
minimum values which make writing Eve code viable are:

    let g:eve_e2m_blanks = 1
    let g:eve_m2e_blanks = 0
    let g:eve_e2e_blanks = 1
    let g:eve_e2e_blanks_search = 0

The default values are chosen more conservatively to help prevent incorrect
insertions and are equivalent to:

    let g:eve_e2m_blanks = 2
    let g:eve_m2e_blanks = 2
    let g:eve_e2e_blanks = 2
    let g:eve_e2e_blanks_search = g:eve_e2e_blanks

My personal customisation of these defauls is to set

    let g:eve_e2e_blanks = 1
    let g:eve_e2e_blanks_search = 0

You can also disable a particular type of fence insertion altogether by setting
`g:eve_TYPE_blanks = -1`

## Contributing

This is my first Vim plugin and may be rough around the edges. If you run into
any problems, please file an issue. Suggestions and advice in the issues is
also humbly solicited, especially if you have any experience with vimscript and
can see better ways of doing things. If you want to fix any problems or add new
features, pull requests are very welcome.

## License

Copyright 2016 Frankie Robertson

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
