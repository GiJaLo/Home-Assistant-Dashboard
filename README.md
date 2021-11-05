# Home-Assistant-Dashboard
My Home Assistant Dashboard


![change_background](https://github.com/lorwel/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Home.jpg)

First of all, I would like to thank the whole awesome HA-community. I've found so much inspiration from other awesome setups and handy tools for setting up my dashboard. Will also post these in her.

If you would like a setup like this, it would be handy if you already have HACS installed.

More information: https://hacs.xyz/docs/basic/getting_started

## Overview <!-- omit in toc -->

- [Theme](#theme)
- [HACS](#hacs)
  - [Sidebar](#sidebar)
  - [Button-card](#button-card)
  - [Mini-mediaplayer](#mini-mediaplayer)
- [Code](#code)
  - [Sidebar](#sidebar)
  - [Button-card](#button-card)
  - [Mini-mediaplayer](#mini-mediaplayer)
- [Examples](#examples)






## Theme
IMPORTANT: To use themes from HACS you'll have to add some code to your configuration file.

Add this to your configuration.yaml
```yaml
frontend:  themes: !include_dir_merge_named themes
```
More information: https://hacs.xyz/docs/categories/themes


<br />


For my GUI I've used the ios Dark theme (installed with HACS)

More information: https://github.com/basnijholt/lovelace-ios-dark-mode-theme

To have the shiny greeny background like mine, you have to add the background to your "Raw Configuration Editor". Don't know what this is? Will have a look at this in the sidebar chapter.
You should place this on top of the editor.
```yaml
background: var(--background-image)
```


## HACS
### Sidebar
As we set the theme already now we can switch over to the interface. On the left side I have the sidebard-card. This stays on every page in your dashboard - it's fixed.

Installation is through HACS - fronted 

!!!!!Sometimes it is possible that you can't find for example the sidebar-card on HACS. This is because you have to add it manually to HACS.!!!!

A little tip: 

- Open HACS
              
- Open Frontend
              
- Top-right corner click on the 3 dots

- Adjusted Repositories

- Copy link (like this one below)

- Category: Lovelace

- Add
              
Now you can find the sidebard-card in your frontend section off HACS.

More information: https://github.com/DBuit/sidebar-card


```yaml
frontend:  themes: !include_dir_merge_named themes
```

