---
layout: post
title: "New theme 'Material' in RStudio v1.0"
description: "Instruction for creating a new editor theme"
tag:
  - rstats
  - rstudio
---

RStudio has recently released version 1.0 of their product. Among [several other changes](https://blog.rstudio.org/2016/11/01/announcing-rstudio-v1-0/), this release also contains a new editor theme called "Material". RStudio guys were kind enough to accept my [pull request](https://github.com/rstudio/rstudio/pull/748) for this theme. I based this theme off of the [vim-hybrid-material colorscheme](https://github.com/kristijanhusak/vim-hybrid-material), which I use as my default theme in GVim.

A screenshot of the way this theme looks: (click to view the image in larger size)
<a href="/images/screenshot-material-theme.png" target="_blank"><img src="/images/screenshot-material-theme.png" alt="image"></a>

The process of creating a new theme wasn't very difficult. The first step is to gather a set of colors and the functions (comment, variable, etc) that these colors represent. In my case, I gathered the list of colors from [vim-hybrid-material/colors/hybrid_material.vim](https://github.com/kristijanhusak/vim-hybrid-material/blob/master/colors/hybrid_material.vim).

 Once the color set is defined, the next step is to create an RStudio theme file with these colors. A quick way to iterate with different variations is to modify an existing theme. The installed theme files are generally located at `<rstudio-install-location>/www/rstudio/`. In my case, this is `/usr/local/lib/rstudio/www/rstudio`. The names of these files can be cryptic (something like `05A30280557A652FA5BA36FB6B4C18F3.cache.css`). Choose one file and edit the file to your liking. The next time you open the RStudio, select the theme corresponding to the css file, and analyse the various elements in the RStudio UI. After a bit of back and forth, we can arrive at the final version of the theme, ready for sharing with the wider world.

 There are few more things that need to be done, before making a pull request. After forking the [RStudio repo](https://github.com/rstudio/rstudio), the final modified css file can be copied over to the `rstudio/src/gwt/src/org/rstudio/studio/client/workbench/views/source/editors/text/themes/` location, with a suitable name for the theme. Few lines need to added to `AceThemes.java` and the `AceThemeResources.java` files, which are present in the same folder as the theme css files. One can follow the changes I made to these files in [my pull request](https://github.com/rstudio/rstudio/pull/748/files). After making a pull request, you also need to sign the [contributor agreement](https://github.com/rstudio/rstudio/blob/master/CONTRIBUTING.md), and send the soft copy to the RStudio. Once the pull request is merged, expect your theme to be present in the next [preview release!](https://www.rstudio.com/products/rstudio/download/preview/), and later in the stable version.
