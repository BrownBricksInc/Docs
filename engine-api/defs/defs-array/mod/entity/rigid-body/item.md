# ✍ Item

Options for RigidBody are passed in here as well\
\*not implemented

| Name                   | Description                                                                                                                                                                                                                                                                                                                                          | Required | Type    | Default  |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------- | -------- |
| type                   | Can be "melee", "ranged", "collectible", or "block" (internal use only; this is used by the block class to auto generate items for each block)                                                                                                                                                                                                       | Yes      | String  |          |
| assetInventory\*       | Texture that displays in the inventory and shows what the item looks like                                                                                                                                                                                                                                                                            | No       | String  |          |
| assetReticle           | Melee, Ranged & Collectible: Texture that is drawn in the center of the screen for aiming assitance , AKA crosshair                                                                                                                                                                                                                                  | No       | String  |          |
| ejectImpulse           | Melee, Ranged & Collectible: Amount of impulse to apply when player dismounts/ejects the item from inventory                                                                                                                                                                                                                                         | No       | Number  | 5        |
| automatic              | Melee and Ranged: An automatic item continues to deal damage as long as you are holding down left click/tap                                                                                                                                                                                                                                          | No       | Boolean | false    |
| cooldown\*             | Melee and Ranged: Number of seconds it takes to "recharge" the item after using it, before it's back at full strength (melee) or before being able to fire another projectile (ranged). In the case of an automatic item, this is the effective firing rate.                                                                                         | No       | Number  | 0.25     |
| uses\*                 | Melee and Ranged: Number of times you can use the item before it breaks. Set to -1 for infinity.                                                                                                                                                                                                                                                     | No       | Integer | -1       |
| blockHelper\*          | Melee: Optionally changes the time required to break certain types of blocks. If a block def's helperItem is equal to this item def's blockHelper, the block will be faster or slower to break.                                                                                                                                                      | No       | String  |          |
| blockHelperRate\*      | Melee: The amount to multiply a block's time to break by. Only applies when the block def's helperItem is equal to this item def's blockHelper. A blockHelperRate of 0.5 would break blocks twice as fast, while a rate of 2 would require twice as much time.                                                                                       | No       | Number  | 1        |
| impact\*               | Melee: The amount of impact damage to inflict upon entities. The impact will not affect blocks.                                                                                                                                                                                                                                                      | No       | Number  | 0        |
| impactDuringCooldown\* | Melee:  Allows attacking with the item during the cooldown period. The impact amount will be multiplied by the charge percentage, so less damage will be dealt.                                                                                                                                                                                      | No       | Boolean | true     |
| projectile             | Ranged: Name of the entity def that the ranged item squirts out                                                                                                                                                                                                                                                                                      | No       | String  |          |
| projectilePos          | Ranged: Where to spawn the projectile, typically at the end of the barrel furthest from the item's mountOffset                                                                                                                                                                                                                                       | No       | Vec3    | \[0,0,0] |
| charged\*              | Ranged: Whether this item fires projectiles with greater velocity+impact after holding down left click/tap for a length of time. Incompatible with automatic                                                                                                                                                                                         | No       | Boolean | false    |
| maxCharge\*            | Ranged: Number of seconds of holding left click/tap before the item is fully charged and the projectile is at maximum strength. The projectile's velocity and impact is multiplied by the charge percentage n\* OPT String assetSight - An additional texture to overlay on the center of the HUD while looking down the barrel or through the sight | No       | Number  | 1        |
| clipSize\*             | Ranged: Maximum amount of ammo/bursts inside the item at any time n\* OPT Number reloadTime \[1] - Time to reload the clip, in seconds                                                                                                                                                                                                               | No       | Integer | 1        |
| burstAmount\*          | Ranged: Number of projectiles fired simultaneously n\* OPT                                                                                                                                                                                                                                                                                           | No       | Integer | 1        |
| sprayRadius\*          | Ranged: Decrease the accuracy, measured in radians.                                                                                                                                                                                                                                                                                                  | No       | Number  |          |
| stackSize\*            | Collectibles: How many of the same item can fit in each inventory space                                                                                                                                                                                                                                                                              | No       | Integer | 1        |

```
/**
 * Options for RigidBody are passed in here as well
 * REQ String type - Can be "melee", "ranged", "collectible", or "block" (internal use only; this is used by the block class to auto generate items for each block)
 * 
 * Shared options between melee, ranged, and collectible item types:
n* OPT String assetInventory - Texture that displays in the inventory and shows what the item looks like
 * OPT String assetReticle - Texture that is drawn in the center of the screen for aiming assitance	, AKA crosshair
 * OPT Number ejectImpulse [5] - Amount of impulse to apply when player dismounts/ejects the item from inventory
 * 
 * Shared options between melee and ranged items:
 * OPT Boolean automatic [false] - An automatic item continues to deal damage as long as you are holding down left click/tap
n* OPT Number cooldown [0.25] - Number of seconds it takes to "recharge" the item after using it, before it's back at full strength (melee) or before being able to fire another projectile (ranged). In the case of an automatic item, this is the effective firing rate.
n* OPT Integer uses [-1] - Number of times you can use the item before it breaks. Set to -1 for infinity.
 * 
 * Melee options:
n* OPT String blockHelper - Optionally changes the time required to break certain types of blocks. If a block def's helperItem is equal to this item def's blockHelper, the block will be faster or slower to break.
n* OPT Number blockHelperRate [1] - The amount to multiply a block's time to break by. Only applies when the block def's helperItem is equal to this item def's blockHelper. A blockHelperRate of 0.5 would break blocks twice as fast, while a rate of 2 would require twice as much time.
n* OPT Number impact [0] - The amount of impact damage to inflict upon entities. The impact will not affect blocks.
n* OPT Boolean impactDuringCooldown [true] - Allows attacking with the item during the cooldown period. The impact amount will be multiplied by the charge percentage, so less damage will be dealt.
 * 
 * Ranged options:
 * OPT String projectile - Name of the entity def that the ranged item squirts out
 * OPT Vetor3 projectilePos [0, 0, 0] - Where to spawn the projectile, typically at the end of the barrel furthest from the item's mountOffset
n* OPT Boolean charged [false] - Whether this item fires projectiles with greater velocity+impact after holding down left click/tap for a length of time. Incompatible with automatic
n* OPT Number maxCharge [1] - Number of seconds of holding left click/tap before the item is fully charged and the projectile is at maximum strength. The projectile's velocity and impact is multiplied by the charge percentage
n* OPT String assetSight - An additional texture to overlay on the center of the HUD while looking down the barrel or through the sight
n* OPT Integer clipSize [1] - Maximum amount of ammo/bursts inside the item at any time
n* OPT Number reloadTime [1] - Time to reload the clip, in seconds
n* OPT Integer burstAmount [1] - Number of projectiles fired simultaneously
n* OPT Number sprayRadius [0] - Decrease the accuracy, measured in radians.
 * 
 * Collectible options:
n* OPT Integer stackSize [1] - How many of the same item can fit in each inventory space
 */
```
