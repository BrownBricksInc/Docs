# 🎯 Projectile

\*not implemented

| Name         | Description                                                                                                                                                                                         | Required | Type    | Default |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------- | ------- |
| velocity     | How fast projectile moves in blocks/sec                                                                                                                                                             | Yes      | Number  |         |
| impact       | Amount of damage the projectile deals to blocks, also the amount of impulse to apply to rigid bodies                                                                                                | No       | Number  | 0       |
| entityDamage | Amount of health damage the projectile deals to entities n\* OPT String consumable - The name of the item def that this projectile consumes from the inventory. Leave unset to not consume anything | No       | Number  | 0       |
| consumable\* | The name of the item def that this projectile consumes from the inventory. Leave unset to not consume anything                                                                                      | No       | String  |         |
| radius       | Optionally add a "blast radius" that deals damage to all nearby entities and blocks, measured in blocks. The impact amount will be multiplied by percent distance from the center.                  | No       | Number  | 0       |
| distance     | Amount of distance to travel before the projectile loses its impact strength, in blocks. -1 for unlimited distance                                                                                  | No       | Number  | -1      |
| damageFade   | Multiply both types of damage by percentage of the distance traveled                                                                                                                                | No       | Boolean | false   |
| reusable\*   | Whether the projectile can be picked back up and reused after settling                                                                                                                              | No       | Boolean | false   |
| gravity\*    | If true, gravity will pull the projectile downward                                                                                                                                                  | No       | Boolean | false   |

```
/**
 * Options for Entity are passed in here as well
 * REQ Number velocity - How fast projectile moves in blocks/sec
 * OPT Number impact [0] - Amount of damage the projectile deals to blocks, also the amount of impulse to apply to rigid bodies
 * OPT Number entityDamage [0] - Amount of health damage the projectile deals to entities
n* OPT String consumable - The name of the item def that this projectile consumes from the inventory. Leave unset to not consume anything
 * OPT Number radius [0] - Optionally add a "blast radius" that deals damage to all nearby entities and blocks, measured in blocks. The impact amount will be multiplied by percent distance from the center.
 * OPT Number distance [-1] - Amount of distance to travel before the projectile loses its impact strength, in blocks. -1 for unlimited distance
 * OPT Boolean damageFade [false] - Multiply both types of damage by percentage of the distance traveled 
n* OPT Boolean reusable [false] - Whether the projectile can be picked back up and reused after settling
n* OPT Boolean gravity [false] - If true, gravity will pull the projectile downward
 */
```
