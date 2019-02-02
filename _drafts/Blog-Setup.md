title: Setup Blog Environment (GitHub+Hexo+Hexo Admin)
author: Chen Pan
tags:
  - Blog
categories: []
date: 2017-11-06 16:26:00
---
1. Hexo is a blog framwork basing on Nodejs. Less dependencies and easy to use.
2. We use github to put our blog data.<BR>About how to build a blog with Github and Hexo, [refer this](https://gist.github.com/btfak/18938572f5df000ebe06fbd1872e4e39)
3. Hexo Admin is an admin UI for the Hexo blog engine, also a *NICE* online editor of markdown. [[website](https://github.com/jaredly/hexo-admin)]
4. Use the NEXT theme, with [website](https://github.com/iissnan/hexo-theme-next)

Possible problems when setting up:
+ After installing HexoAdmin plugin, generate the hexo project, it will have errors: 
  	ERROR Plugin load failed: hexo-admin SyntaxError: Unexpected token ILLEGAL
 Solution: Use a latest version of hexo-admin instead of the default version: 
 	 npm install hexo-admin@2.1.0 --registry=https://github.com/jaredly/hexo-admin/

+ After using theme: Next, it will cause a problem when generatation:
    
  	ERROR Script load failed: themes/hexo-theme-next/scripts/tags/exturl.js  
  	Error: Cannot find module 'hexo-util'  
  U need to install hexo-util package. Try this command: 
  	 npm config set registry https://registry.npm.taobao.org
     
Editing Blog:
1. Use Hexo admin:  command **hexo s** in the root folder.
2. About multi-pc synchronization:   [refer link](https://juejin.im/post/5acf22e6f265da23994eeac9).  However, i don't think cost so much time in the synchronization is worth.

Updating: Possible problem:
* repeat inputting the username and passwd when deploy:  [refer this](http://www.voidcn.com/article/p-whsmqfbx-vm.html)