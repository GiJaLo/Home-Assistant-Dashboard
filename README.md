# Home-Assistant-Dashboard
My Home Assistant Dashboard


![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Home.jpg)

First of all, I would like to thank the whole awesome HA-community. I've found so much inspiration from other awesome setups and handy tools for setting up my dashboard. Will also post these in her.

If you would like a setup like this, it would be handy if you already have HACS installed.

More information: https://hacs.xyz/docs/basic/getting_started

## Overview <!-- omit in toc -->

- [Theme](#theme)
- [HACS-Frontend](#hacs)
  - [Sidebar](#sidebar)
        - [Intro](#editing)
        - [Editing](#editing)
        - [Code-](#ed)
  - [Button-card](#button-card)
        - [Intro](#editing)
        - [Editing](#editing)
        - [Code-](#ed)
  - [Mini-mediaplayer](#mini-mediaplayer)
- [Code](#code)
  - [Sidebar](#sidebar)
  - [Button-card](#button-card)
  - [Mini-mediaplayer](#mini-mediaplayer)
- [Examples](#examples)



<hr style="border:2px solid gray"> </hr>


## Theme
IMPORTANT: To use themes from HACS you'll have to add some code to your configuration file.

Add this to your configuration.yaml
```yaml
frontend:  themes: !include_dir_merge_named themes
```
Don't forget to restart your HA

More information: https://hacs.xyz/docs/categories/themes


<br />


For my GUI I've used the ios Dark theme (installed with HACS)

More information: https://github.com/basnijholt/lovelace-ios-dark-mode-theme

To have the shiny greeny background like mine, you have to add the background to your "Raw Configuration Editor". Don't know what this is? Will have a look at this in the sidebar chapter.
You should place this on top of the editor.
```yaml
background: var(--background-image)
```

<hr style="border:2px solid gray"> </hr>

## HACS-Frontend
### Sidebar
#### Intro
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

#### Editing
To add the sidebar to your lovelace dashboard. You need to add it to your Raw Configuration Editor.
The what the what?
- Make a new lovelave dashboard/ or use your existing one
- Open 
- Topright corner click on the 3 dots
- Configure UI
- Choose start with an empty dashboard or not
- Click on Take over
- Again go to the Topright corner and click on the 3 dots
- Click on "Raw Configuration Editor" (Could also have an other name, my HA is set to Dutch)
- Here you have the full file of your dashboard.

First have a look of the code below

So what do we see here?
Everything that is above views is the overall "setting" of your dashboard. Here is where we put the background and also the sidebar.
Because these 2 things are fixed.


```yaml
All above this
views:
```

#### Code
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
views:
```
<hr style="border:2px solid gray"> </hr>


### Button-card
#### Intro
This is maybe my absolute favourite lovelace card. I use it for almost everything! Like my example above for the bottom row of buttons, to navigate to other views.

First install this with HACS and go to the github page: https://github.com/custom-cards/button-card
It is a bit of read, but here I will show how I use it.

#### Editing
If the installation worked well we can add for example a simple button card to our new lovelace dashboard.
- Open new dashboard
- Topright corner click on the 3 dots
- Configure UI
- Add new Card
- Scroll down to Manually (add your own adjusted card)
- Past the code below

```yaml
type: custom:button-card
color_type: card
color: rgba(10, 10, 10, 0.4)
icon: mdi:flash
name: Energie
tap_action:
  action: navigate
  navigation_path: /scherm-beneden/energie
```

## Examples
## Home

```yaml
views:
  - title: Home
    type: custom:grid-layout
    badges: []
    cards:
      - type: custom:layout-card
        layout_type: masonry
        layout: {}
        cards:
          - type: custom:alarmo-card
            entity: alarm_control_panel.alarmo
            keep_keypad_visible: false
            name: Alarm
            use_clear_icon: false
            button_scale: 1.3
          - type: custom:power-distribution-card
            title: ''
            entities:
              - decimals: '3'
                display_abs: true
                name: Huis
                unit_of_display: adaptive
                consumer: true
                icon: mdi:home
                entity: sensor.verbruik_huistot
                preset: home
                icon_color:
                  bigger: ''
                  equal: ''
                  smaller: ''
                invert_value: true
              - decimals: '2'
                display_abs: true
                name: Net
                unit_of_display: adaptive
                icon: mdi:transmission-tower
                entity: sensor.verbruik_consumtion
                preset: grid
                icon_color:
                  bigger: ''
                  equal: ''
                  smaller: ''
              - decimals: '2'
                display_abs: true
                name: Zon
                unit_of_display: adaptive
                icon: mdi:solar-power
                producer: true
                entity: sensor.fronius_ac_power
                preset: solar
                icon_color:
                  bigger: ''
                  equal: ''
                  smaller: ''
                invert_value: false
                calc_excluded: false
              - decimals: '2'
                display_abs: true
                name: Net
                unit_of_display: adaptive
                icon: mdi:transmission-tower
                entity: sensor.verbruik_producion
                preset: grid
                icon_color:
                  bigger: ''
                  equal: ''
                  smaller: ''
                invert_value: true
            center:
              type: card
              content:
                type: glance
                entities:
                  - sun.sun
            animation: slide
          - type: entities
            entities:
              - entity: sensor.recycleapp_afval_pmd
                name: PMD
                icon: mdi:bottle-soda-classic
              - entity: sensor.recycleapp_afval_restafval
                icon: mdi:delete-empty
                name: Rest
              - entity: sensor.recycleapp_afval_papier
                icon: mdi:newspaper-variant
                name: Papier/Karton
              - entity: sensor.recycleapp_afval_grofvuil
                name: Grof
                icon: mdi:human-female
          - type: custom:weather-card
            entity: weather.home
            number_of_forecasts: '5'
            details: true
          - type: glance
            entities:
              - entity: person.so
              - entity: person.lo
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:play-pause
                name: Muziek
                tap_action:
                  action: call-service
                  service: media_player.media_play_pause
                  service_data:
                    entity_id: media_player.eetplaats_speaker
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:lightbulb-on
                name: Verlichting
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                entity: input_boolean.stofzuiger_quick
                icon: mdi:robot-vacuum
                name: Gaston
                state:
                  - value: 'off'
                    color: rgba(10, 10, 10, 0.4)
                  - value: 'on'
                    color: auto
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:robot-mower
                name: Jeanine
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 55px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:flash
                name: Energie
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/energie
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:lock
                name: Beveiliging
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/beveiliging
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:lamp
                name: Verlichting
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/verlichting
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:music
                name: Muziek
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/muziek
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:robot-vacuum
                name: Gaston
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/stofzuiger
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:robot-mower
                name: Jeanine
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/maaier
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:calendar-check
                name: Taakjes
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/taken
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:glasses
                name: Nerd
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/temp
```
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Home.jpg)
## Music Main
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Music.jpg)
## Music Channels
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Music-channels.jpg)
## Vacuum Main (Choose floor)
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Vacuum.jpg)
## Vacuum 0 (Groundfloor)
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Vacuum-0.jpg)
