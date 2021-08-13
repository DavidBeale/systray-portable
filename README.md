# systray-portable

A portable version of [go systray](https://github.com/getlantern/systray), using stdin/stdout to communicate with other language.

A fork from https://github.com/felixhao28/systray-portable, which in turn forked from https://github.com/zaaack/systray-portable.

## Protocol

Each line is a json string.

tray binary =>  
=> ready  `{"type": "ready"}`  

<= init menu
```json
{
  "icon": "<base64 string of image>",
  "title": "Title",
  "tooltip": "Tooltip",
  "items":[{
    "title": "aa",
    "tooltip":"bb",
    "checked": true,
    "enabled": true,
    "hidden": false,
    "__id": 0
  }, {
    "title": "<SEPARATOR>",
    "tooltip":"",
    "checked": true,
    "enabled": true,
    "hidden": false,
    "__id": 1
  }, {
    "title": "aa2",
    "tooltip":"bb",
    "checked": false,
    "enabled": true,
    "hidden": false,
    "__id": 2
  }]}
```

=> clicked  
```json
{
  "type":"clicked",
  "__id":0
}
```

<= update-item / update-menu / update-item-and-menu
```json
{
  "type": "update-item",
  "item": {"title":"aa3","tooltip":"bb","enabled":true,"checked":true,"__id":0},
}
```

<= exit gracefully
```json
{
  "type": "exit"
}
```

## Binary
`go build -ldflags "-s -w" tray.go` (-s -w strips symbol table and debug info, optional)
