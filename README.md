# Home-Assistant-Dashboard
My Home Assistant Dashboard

***This page is still under construction!!!***


![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Home.jpg)

First of all, I would like to thank the whole awesome HA-community. I've found so much inspiration from other awesome setups and handy tools for setting up my dashboard. Will also post these in her.

I'm not the CSS expert or any kind. I've challenged myself to make everything in Lovelace dashboard with custom cards. There are some workarounds for some problems that I created myself(workarounds but also problems). Maybe there are better solutions.. You can always let me know.

If you would like a setup like this, it would be handy if you already have HACS installed.

More information: https://hacs.xyz/docs/basic/getting_started

## Overview <!-- omit in toc -->
- [Theme](#theme)
- [Cards](#cards)
  - [Info](#info)
  - [Install](#install)
- [Setup](#setup)
- [Sidebar](#sidebar)
  - [Intro](#setup)
  - [Editing](#editing)
  - [Code-](#ed)
- [Button-card](#button-card)
  - [Intro](#editing)
  - [Editing](#editing)
  - [Code-](#ed)
- [Examples](#examples)



***Just want to copy some code? Go to examples***



<hr style="border:4px solid gray"> </hr>


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

<hr style="border:4px solid gray"> </hr>

## Cards
### Info

As we set the theme already now we can switch over to the interface. But before with do that we need to have some frontend lovelace cards from HACS.

***Sometimes it is possible that you can't find for example the sidebar-card on HACS. This is because you have to add it manually to HACS***

A little tip: 

- Open HACS
              
- Open Frontend
              
- Top-right corner click on the 3 dots

- Adjusted Repositories

- Copy link (like sidebar card below)

- Category: Lovelace

- Add
              
Now you can find the sidebard-card in your frontend section off HACS.

<hr style="border:2px solid gray"> </hr>

### Install

These are cards I've used with HACS:

- Weather Card

  Link: https://github.com/bramkragten/weather-card

- Power-distribution-card

  Link: https://github.com/JonahKr/power-distribution-card

- Vacuum Card

  Link: https://github.com/denysdovhan/vacuum-card

- Mini Media Player

  Link: https://github.com/kalkih/mini-media-player

- Kiosk Mode

  Link: https://github.com/maykar/kiosk-mode

- Alarmo Card

  Link: https://github.com/nielsfaber/alarmo-card

- Button Card

  Link: https://github.com/custom-cards/button-card

- Layout card

  Link: https://github.com/thomasloven/lovelace-layout-card

- Sidebar Card

  Link: https://github.com/DBuit/sidebar-card
  
<hr style="border:4px solid gray"> </hr>


## Setup

If you like my dashboard it is important to know how I've set this up. I like to use a lot of views/pages/tabs or whatever you like to call it.
This is an example below, I only added music and my robovacuum cleaner. So I use the bottom row with the buttons to navigate through my dashboard. And on the left side the home button that always will navigate home.

![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/overview.JPG)

When you add a new view/page/tab I always change the setting to a grid layout.

![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/settings.JPG)

Below you find how I always setup a view/page/tab

![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/setup2.jpg)


<hr style="border:4px solid gray"> </hr>


## Sidebar
### Setup
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

First have a look of the **code

So what do we see here?
Everything that is above "views" is the overall "setting" of your dashboard. Here is where we put the background and also the sidebar.
Because these 2 things are fixed.


```yaml
All above this
views:
```

### Code
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
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Home.jpg)
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
<hr style="border:4px solid gray"> </hr>

## Music Main
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Music.jpg)

```yaml
- title: '4-Muziek '
    path: muziek
    type: custom:grid-layout
    badges: []
    cards:
      - type: custom:layout-card
        layout_type: horizontal
        layout: {}
        cards:
          - type: custom:mini-media-player
            entity: media_player.eetplaats_speaker
            hide:
              name: true
              icon: true
              power: true
              source: true
              controls: true
              volume: true
            artwork: full-cover
            toggle_power: false
            scale: '1.5'
          - type: vertical-stack
            cards:
              - type: custom:mini-media-player
                hide:
                  name: false
                  icon: true
                  power: true
                  source: true
                  controls: true
                  info: true
                name: Eetplaats Speaker (Master)
                entity: media_player.eetplaats_speaker
              - type: custom:mini-media-player
                hide:
                  name: false
                  icon: true
                  power: true
                  source: true
                  controls: true
                  info: true
                name: Keuken Speaker
                entity: media_player.keuken_speaker
              - type: custom:mini-media-player
                hide:
                  name: false
                  icon: true
                  power: true
                  source: true
                  controls: true
                  info: true
                name: Televisie Speaker
                entity: media_player.televisie_speaker
              - type: entities
                entities:
                  - entity: input_boolean.sonos_join_keuken
                    icon: mdi:speaker
                    name: Keuken speaker joinen
                  - entity: input_boolean.sonos_join_televisie
                    name: Televisie speaker joinen
                    icon: mdi:speaker
                title: Speakergroep
            title: Volume Speakers
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 0px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:radio
                name: Zenders
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/zenders
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:spotify
                name: Spotify
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/spotify
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 37px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:skip-previous
                name: Vorige
                tap_action:
                  action: call-service
                  service: media_player.media_previous_track
                  service_data:
                    entity_id: media_player.eetplaats_speaker
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:skip-next
                name: Volgende
                tap_action:
                  action: call-service
                  service: media_player.media_next_track
                  service_data:
                    entity_id: media_player.eetplaats_speaker
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:volume-minus
                name: Stiller
                tap_action:
                  action: call-service
                  service: script.turn_on
                  service_data:
                    entity_id: script.muziek_volume_omlaag
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:volume-plus
                name: Luider
                tap_action:
                  action: call-service
                  service: script.turn_on
                  service_data:
                    entity_id: script.muziek_volume_omhoog
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:play-pause
                name: Play/Pause
                tap_action:
                  action: call-service
                  service: media_player.media_play_pause
                  service_data:
                    entity_id: media_player.eetplaats_speaker
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:stop
                name: Stop
                tap_action:
                  action: call-service
                  service: media_player.media_stop
                  service_data:
                    entity_id: media_player.eetplaats_speaker
```
<hr style="border:4px solid gray"> </hr>


## Music Channels
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Music-channels.jpg)

```yaml
- title: 4A-Zenders
    path: zenders
    icon: ''
    type: custom:grid-layout
    badges: []
    cards:
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 0px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/zenders/stubru.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Studio Brussel
                show_entity_picture: true
                entity: input_boolean.muziek_stubru
              - type: custom:button-card
                entity_picture: /local/zenders/radio1.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Radio 1
                show_entity_picture: true
                entity: input_boolean.muziek_radio_1
              - type: custom:button-card
                entity_picture: /local/zenders/radio2.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Radio 2
                show_entity_picture: true
                entity: input_boolean.muziek_radio_2
              - type: custom:button-card
                entity_picture: /local/zenders/klara.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Klara
                show_entity_picture: true
                entity: input_boolean.muziek_klara
              - type: custom:button-card
                entity_picture: /local/zenders/mnm.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: MNM
                show_entity_picture: true
                entity: input_boolean.muziek_mnm
              - type: custom:button-card
                entity_picture: /local/zenders/qmusic.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Q-music
                show_entity_picture: true
                entity: input_boolean.muziek_qmusic
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 0px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/zenders/radio1classics.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Radio 1 Classics
                show_entity_picture: true
                entity: input_boolean.muziek_radio_1_classics
              - type: custom:button-card
                entity_picture: /local/zenders/nostalgie.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Nostalgie
                show_entity_picture: true
                entity: input_boolean.muziek_nostalgie
              - type: custom:button-card
                entity_picture: /local/zenders/willy.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Radio Willy
                show_entity_picture: true
                entity: input_boolean.muziek_willy_radio
              - type: custom:button-card
                entity_picture: /local/zenders/joe.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Joe Fm
                show_entity_picture: true
                entity: input_boolean.muziek_joe_fm
              - type: custom:button-card
                entity_picture: /local/zenders/lage landen.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Lage Landenlijst
                show_entity_picture: true
                entity: input_boolean.muziek_lage_landen
              - type: custom:button-card
                entity_picture: /local/zenders/bene.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Bene Bene
                show_entity_picture: true
                entity: input_boolean.muziek_bene
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 0px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/zenders/tijdloze.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: De Tijdloze
                show_entity_picture: true
                entity: input_boolean.muziek_tijdloze
              - type: custom:button-card
                entity_picture: /local/zenders/untz.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: UNTZ
                show_entity_picture: true
                entity: input_boolean.muziek_untz
              - type: custom:button-card
                entity_picture: /local/zenders/bruut.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Bruut
                show_entity_picture: true
                entity: input_boolean.muziek_bruut
              - type: custom:button-card
                entity_picture: /local/zenders/hooray.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Hooray
                show_entity_picture: true
                entity: input_boolean.muziek_hooray
              - type: custom:button-card
                entity_picture: /local/zenders/90's.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: MNM 90's & 00's
                show_entity_picture: true
                entity: input_boolean.muziek_mnm_90_en_00
              - type: custom:button-card
                entity_picture: /local/zenders/mnmhits.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: MNMN Hits
                show_entity_picture: true
                entity: input_boolean.muziek_mnm_hits
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 0px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/zenders/nws.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: VRT NIEUWS
                show_entity_picture: true
                entity: input_boolean.muziek_tijdloze
              - type: custom:button-card
                entity_picture: /local/zenders/classic21.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Classic 21
                show_entity_picture: true
                entity: input_boolean.muziek_untz
              - type: custom:button-card
                entity_picture: /local/zenders/goldies.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Goldies
                show_entity_picture: true
                entity: input_boolean.muziek_klara_continuo
              - type: custom:button-card
                entity_picture: /local/zenders/klara.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Klara Continuo
                show_entity_picture: true
                entity: input_boolean.muziek_klara_continuo
              - type: custom:button-card
                entity_picture: /local/zenders/kcrw.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: KCRW
                show_entity_picture: true
                entity: input_boolean.muziek_mnm_hits
              - type: custom:button-card
                entity_picture: /local/zenders/kexp.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: KEXP
                show_entity_picture: true
                entity: input_boolean.muziek_mnm_hits
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 0px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/zenders/jazz24.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Jazz 24
                show_entity_picture: true
                entity: input_boolean.muziek_tijdloze
              - type: custom:button-card
                entity_picture: /local/zenders/latin.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Latin Jazz
                show_entity_picture: true
                entity: input_boolean.muziek_untz
              - type: custom:button-card
                entity_picture: /local/zenders/blues.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Blues Jazz
                show_entity_picture: true
                entity: input_boolean.muziek_klara_continuo
              - type: custom:button-card
                entity_picture: /local/zenders/jazz.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Jazz
                show_entity_picture: true
                entity: input_boolean.muziek_klara_continuo
              - type: custom:button-card
                entity_picture: /local/zenders/klassiek.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Klassiek Jazz
                show_entity_picture: true
                entity: input_boolean.muziek_mnm_hits
              - type: custom:button-card
                entity_picture: /local/zenders/piano.png
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                name: Piano Jazz
                show_entity_picture: true
                entity: input_boolean.muziek_mnm_hits
      - type: vertical-stack
        cards:
          - type: custom:button-card
            color_type: blank-card
            color: rgba(0, 0, 0, 0)
            styles:
              card:
                - height: 40px
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: card
                color: rgba(10, 10, 10, 0.4)
                icon: mdi:arrow-left
                name: Terug
                tap_action:
                  action: navigate
                  navigation_path: /scherm-beneden/muziek
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
              - type: custom:button-card
                color_type: blank-card
                color: rgba(0, 0, 0, 0)
```

## Vacuum Main (Choose floor)
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Vacuum.jpg)
## Vacuum 0 (Groundfloor)
![change_background](https://github.com/GiJaLo/Home-Assistant-Dashboard/blob/main/Pictures%20Dashboard/Vacuum-0.jpg)
