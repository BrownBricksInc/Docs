# 🎳 Rigid body

| Name       | Description                                                                                                                                                                                             | Required | Type    | Default |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------- | ------- |
| geom       | Array of defPxGeometry options                                                                                                                                                                          | No       | Array   |         |
| density    | Ratio of mass to volume (density = mass / volume)                                                                                                                                                       | No       | Number  | 1       |
| motionLock | Higher number progressively constrains movement and rotation. 0 for no constraint, 1 to constrain to the axis/axes of the planet's gravity (useful for stacking rigid bodies), 2 for no movement at all | No       | Integer | o       |
| pushable   | Whether player can push the rigid body around by walking into it                                                                                                                                        | No       | Boolean | false   |

```
/**
 * Options for Entity are passed in here as well
 * OPT Array geom - Array of defPxGeometry options
 * OPT Number density [1] - Ratio of mass to volume (density = mass / volume)
 * OPT Integer motionLock [0] - Higher number progressively constrains movement and rotation. 0 for no constraint, 1 to constrain to the axis/axes of the planet's gravity (useful for stacking rigid bodies), 2 for no movement at all
 * opt Boolean pushable [false] - Whether player can push the rigid body around by walking into it
 */
```
