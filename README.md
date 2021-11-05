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
        - [Intro](#editing)
        - [Editing](#editing)
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
background: var(--background-image)
sidebar:
  hideHassSidebar: false
  digitalClock: true
  clock: false
  hideTopMenu: false
  showTopMenuOnMobile: false
  date: true
  dateFormat: dddd, DD MMMM
  title: null
  style: |
    :host {
       --sidebar-background: transparent!important;
       --sidebar-text-color: #EEE;
       --face-color: #333;
       --face-border-color: #EEE;
       --clock-hands-color: #FFF;
       --clock-seconds-hand-color: #FF4B3E;
       --clock-middle-background: transparent!important;
       --clock-middle-border: #EEE;
     }
  width:
    mobile: 0
    tablet: 15
    desktop: 18
  breakpoints:
    mobile: 768
    tablet: 1024
  template: >


    <li>__________________________</li> <li>Afval:</li> {% if "Geen" in
    states('sensor.recycleapp_afval_morgen') %} <li>Morgen geen
    afvalophaling</li> {% endif %}

    {% if "Morgen" in states('sensor.blink_papier') %} <li>Morgen oudpapier aan
    de straat</li> {% endif %}

    {% if "Morgen" in states('sensor.blink_pmd') %} <li>Morgen plastic aan de
    straat</li> {% endif %}

    {% if "Morgen" in states('sensor.blink_restafval') %} <li>Morgen grijzebak
    aan de straat</li> {% endif %}

    {% if states('sensor.current_lights_on') | float > 0 %}
    <li>{{states('sensor.current_lights_on')}} lampen aan</li> {% endif %}

    {% if states('sensor.current_media_players_on') | float > 0 %}
    <li>{{states('sensor.current_media_players_on')}} speakers aan</li> {% endif
    %}  <li>__________________________</li> <li>Kalender:</li> <li>Geen jarigen
    deze week</li>
  bottomCard:
    type: horizontal-stack
    cardOptions:
      cards:
        - type: custom:button-card
          color_type: label-card
          color: rgb(255, 255, 255)
          icon: mdi:home
          styles:
            card:
              - height: 79px
              - width: 200px
          tap_action:
            action: navigate
            navigation_path: /scherm-beneden/0
```

