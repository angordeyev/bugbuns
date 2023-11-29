# Brave

## context.reverso.net

Ctrl-Alt-T - translate using Context.Reverso

## Plugins

  * [Tampermonkey](https://www.tampermonkey.net/)
    `open('https://google.com', '_self').close();`

## PWA

```shell
brave --app=http://<some-site>.com
```

## Surfing Keys

[Open url in current tab](https://github.com/brookhong/Surfingkeys/issues/68)

```javascript
mapkey('o','#8Open an URL in current tab', function() {Front.openOmnibar({type: "URLs", extra: "getTopSites", tabbed: false});});
```

## Resources

[Command line option to open a URL in the same tab. Bugs Chromium.](https://bugs.chromium.org/p/chromium/issues/detail?id=141942)
