title: Setup Blog Environment (GitHub+Hexo+Hexo Admin)
author: Chen Pan
tags:
  - Blog
categories: []
date: 2017-11-06 16:26:00
---
> 不积跬步，无以至千里；不积小流，无以成江海

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