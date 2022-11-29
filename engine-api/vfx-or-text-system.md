---
description: Allows a user to add text to the game that can be used for labels, signs etc
---

# VFX | Text System

<figure><img src="../.gitbook/assets/Screenshot 2022-11-23 at 11.11.11.png" alt=""><figcaption></figcaption></figure>

### Parameters

| Name            | Description                                                                                                                                                                                                                        | Default                                             |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| font            | CSS font name \["ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'"] |                                                     |
| fontSize        | Size of font                                                                                                                                                                                                                       | 32                                                  |
| backgroundColor | CSS color, supports transparency                                                                                                                                                                                                   | "#00000000"                                         |
| fontColor       | "white"                                                                                                                                                                                                                            | CSS color, supports transparency                    |
| margin          | 6                                                                                                                                                                                                                                  | Amount of padding around the background border      |
| linePadding     | 4                                                                                                                                                                                                                                  | Amount of extra vertical padding inbetween lines    |
| radius          | 0                                                                                                                                                                                                                                  | Radius of rounded background rectangle corners      |
| faceCamera      | false                                                                                                                                                                                                                              | Optionally always angle the text towards the camera |
| transform       | [defTransform](defs/utilities/transform-deftransform.md)                                                                                                                                                                           | defTransform options for obj                        |

### Adding Text

After adding text, the text VFX id will be returned.

```javascript
DEBUG.BB.planet.vfx.serverAdd("text", "all",
	{
		font: "'Arial', sans-serif",
		fontSize: 50,
		backgroundColor: "#FF0000FF",
		fontColor: "#00FF01",
		margin: 30,
		linePadding: 10,
		radius: 10,
		faceCamera: true,
		transform:
		{
			pos: DEBUG.BB.planet.player.position,
			rot: new DEBUG.Euler(0, Math.PI, 0)
		}
	},
	"Oh, you think darkness is your ally.\n But you merely adopted the dark;\n I was born in it"
); // returns text id
```

### Removing Text

Remove all text

```javascript
DEBUG.BB.planet.vfx.serverRemoveAll()
```

Remove text by ID

```javascript
DEBUG.BB.planet.vfx.serverRemove(id);
```
