Wekan uses GFM (Github Flavored Markdown).
We use the following project that ports GFM to meteor: https://github.com/wekan/markdown with updated newest markdown, that is fork of https://github.com/perak/markdown where parser implements only gfm v0.28 (current is 0.29). It's appears that the parser uses v0.3.1 of marked.js and its changelog in that version is not documented. Therefore It's also possible that only gfm 0.27 is supported. This issue will be addressed in the next Wekan release.

## List of guides (from web archive):
* [GFM 0.28 list of features](https://web.archive.org/web/20190405063005/https://github.github.com/gfm/).
* [GFM 0.27 list of features](https://web.archive.org/web/20170314184131/https://github.github.com/gfm/).

## Where can I use the markdown?
* Card name.
* Board name - Works on board view only. 
* Card description, list and task list.