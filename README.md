# THIS IS A FORKED REP FOR FONT IMPLEMENTATION, ALL CREDIT GOES TO THE AUTHOR reynevan24

# Anarchist Overlay

Module for the Foundry VTT, allowing to render arbitrary HTML in a configurable overlay above the canvas for all users simultaneously. It also includes a method for getting HTML for mission briefing-like text crawl.

Additionally, this version can render custom fonts uploaded to your foundry instance by calling the fontfamily inside a line object. By default it is set to 'monospace'

## Installation

Install using a manifest link:
```
https://github.com/Mizarul/anarchist-overlay/releases/latest/download/module.json
```

## Example usage:

Macro:
```js

const overlayConfig = {
  positionX: 'start',
  positionY: 'center'
}

const textConfig = {
  offsetX: '20px',
  offsetY: '0',
  typingTime: 2,
  delay: 1,
  blackBars: true,
  lines: [{
      text: 'MISSION 1: BUG HUNT',
      fontSize: '52px',
      fontFamily: 'monospace'
    },
    {
      text: 'COMBAT: TRAPDOOR SPIDER',
      fontSize: '38px',
    },
    {
      text: 'OBJECTIVE: SEARCH AND DESTROY',
      fontSize: '34px'
    },
    {
      text: 'EARLY SPRING, 5014U | HERCYNIA',
      fontSize: '20px'
    },
    {
      text: 'FOREST NEAR EVERGREEN | WEATHER: EXTREME HUMIDITY',
      fontSize: '20px'
    },
  ]
}


const anarchistOverlay = game.modules.get('anarchist-overlay');
textHtml = await anarchistOverlay.createTextCrawlHtml(textConfig);


anarchistOverlay.createOverlay(overlayConfig, textHtml);

```
Effect:

![Animation](https://user-images.githubusercontent.com/10486394/233835406-5a02eaf6-3374-491b-97ba-813512fab075.gif)

### Glitch Effect:

```js
const overlayConfig = {
    positionX: 'center',
    positionY: 'center',
    closeTime: 18,
    blockInteractions: false
}

const textConfig = {
    offsetX: '20px',
    offsetY: '0',
    typingTime: 1.5,
    delay: 0.5,
    blackBars: false,
    aboveUi: false,
    glitchEffect: { time: 0.5 },
    lines: [
      {
        text: '>//CC: FORCOMM X-X DESG:: “BROADCAST”',
        fontSize: '30px',
        fontFamily: 'monospace'
      },
      {
        text: '>//if:::HOSTILE=TRUE then:::',
        fontSize: '30px',
        fontFamily: 'monospace'
      },
      {
        text: '>//WIPE THEM ALL AWAY',
        fontSize: '30px'
      },
      {
        text: '>//EVERY SINGLE ONE OF THEM',
        fontSize: '30px'
      },
      {
        text: '>//KILL THEM WITH PREJUDICE LEAVE NO GROUND UNBURNED',
        fontSize: '30px'
      },
      {
        text: '>//if:::CINDERS ASH DARK SMOKE=TRUE then:::',
        fontSize: '30px'
      },
      {
        text: '>//AWAIT FURTHER TASKING',
        fontSize: '30px'
      },
    ]
  }


const anarchistOverlay = game.modules.get('anarchist-overlay');
textHtml = await anarchistOverlay.createTextCrawlHtml(textConfig);


anarchistOverlay.createOverlay(overlayConfig, textHtml);
```
![Animation-4](https://github.com/Mizarul/anarchist-overlay/assets/10486394/7a0c55be-2a1b-4bb2-b987-df6e6fc78b7d)

## Config
```js
//Overlay config
export type OverlayConfig = {
  positionX?: string; // 'start', 'center' or 'end'
  positionY?: string; // 'start', 'center' or 'end'
  fadeOnClose?: boolean; // should overlay fade out after closeTime
  closeTime?: number; // how long overlay should stay open, in seconds
  closeAllWindows?: boolean; // should all windows (character sheets etc.) be closed before overlay initialization
  aboveUi?: boolean; // should it render above or under UI (above blocks interactivity until overlay closes,
  blockInteractions?: boolean; // should it block interactions with canvas and/or UI (defaults to true)
}
//Text config
export type TextCrawlConfig = {
  offsetX?: string; // for example '15px'
  offsetY?: string; // for example '15px'
  typingTime?: number, // how long (in seconds) does the typing animation take per one line
  delay?: number, // how long (in seconds) does the typing animation pause before next line is typed
  blackBars?: boolean, // should black bars on top and bottom be rendered
  lines: { text: string, fontSize?: string, fontFamily?: string }[], // list of lines to be rendered
  glitchEffect?: { time: number } | false; // adds a glitch effect. Should contain object with information how long should animation loop take
};
```
