# 💾 Mod



| Name   | Description                                                                                                                                                                                                                                                                       | Required | Type     |   |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | - |
| name   | Name of the mod. The prefix of the string is used by the engine to determine how to instantiate this mod. Valid instantiable options are "Player", "Projectile", "RigidBody", "RBChunk", "Item", "Vehicle", "Blocks". Anything else is interpreted as an asset download list only | Yes      | String   |   |
| assets | List of string URLs to download as dependencies                                                                                                                                                                                                                                   | No       | Array    |   |
| server | Server-sided init script callback. Runs in the same order that mods are specified in the defs array                                                                                                                                                                               | No       | Function |   |
| client | Client-sided init script callback. Runs in the same order that mods are specified in the defs array. The function runs in the global scope and can't access anything from the server's planet script. Must set this property using : or = (no "client() {}" shorthand)            | No       | Function |   |

```
/**
 * REQ String name - Name of the mod. The prefix of the string is used by the engine to determine how to instantiate this mod. Valid instantiable options are "Player", "Projectile", "RigidBody", "RBChunk", "Item", "Vehicle", "Blocks". Anything else is interpreted as an asset download list only
 * OPT Array assets - List of string URLs to download as dependencies
 * OPT Function server - Server-sided init script callback. Runs in the same order that mods are specified in the defs array
 * OPT Function client - Client-sided init script callback. Runs in the same order that mods are specified in the defs array. The function runs in the global scope and can't access anything from the server's planet script. Must set this property using : or = (no "client() {}" shorthand)
 */
```
