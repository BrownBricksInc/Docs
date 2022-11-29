# 🎅 Entity

Cannot instantiate a new Entity directly. Cannot call new Entity(), must make a new subclass like new Player().

| Name                      | Description                                                                                                                                                                                            | Required | Type           | Default             |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------------- | ------------------- |
| health                    | Maximum amount of health entity can have. -1 for invincibility                                                                                                                                         | No       | Number         | -1                  |
| mesh                      | defMesh options                                                                                                                                                                                        | No       | Object         |                     |
| camera                    | Modifies camera settings when camera's target is this entity                                                                                                                                           | No       | Object         |                     |
| camera::offset            | Offset from the target's position                                                                                                                                                                      | No       | Vec3           | \[0,0,0]            |
| camera::minPitch          | Minimum pitch angle, in radians (0 is looking straight down, PI is straight up)                                                                                                                        | No       | Number         | 0                   |
| camera::maxPitch          | Maximum pitch angle, in radians (0 is looking straight down, PI is straight up)                                                                                                                        | No       | Number         | PI                  |
| camera::minDst            | Minimum orbit distance/zoom                                                                                                                                                                            | No       | Number         | 0                   |
| camera::maxDst            | Maximum orbit distance/zoom, -1 for no limit                                                                                                                                                           | No       | Number         | -1                  |
| camera::defaultDst        | Default orbit distance after calling targetEntity()                                                                                                                                                    | No       | Number         | minDst              |
| camera::flingDeceleration | Amount of deceleration when flinging the camera dir around on touchscreen (Infinity = immediate stop, 0 = never stop)                                                                                  | No       | Number         | 180                 |
| camera::fov               | Field of view Y, in radians                                                                                                                                                                            | No       | Number         | CAM\_FOV_\__DEFAULT |
| mountPoints               | Array of mount point objects. The order of the mount point array determines in what order the mount points fill up when the index is not specified in mount()                                          | No       | Array          |                     |
| mountPoints::mount        | Moint point position, relative to the entity's current position                                                                                                                                        | Yes      | Vec3           |                     |
| mountPoints::dismount     | Position relative to the mount point, where the entity dismounts at. Recommend not having this at ground level or else you might fall through the ground if vehicle is tilted left or right on a slope | No       | Vec3           | \[0,0,0]            |
| mountOffset               | Offsets this entity while it's mounted                                                                                                                                                                 | No       | Object         |                     |
| mountOffset::pos          |                                                                                                                                                                                                        | No       | Vec3           |                     |
| mountOffset::rot          |                                                                                                                                                                                                        | No       | Euler          |                     |
| mountOffset::scl          | Use number type for \[number, number, number]                                                                                                                                                          | No       | Vector3/Number |                     |
| frameCounterLimit         | With enforce333 enabled, the maximum number of successive frames that chunks are allowed to be forcibly built/downloaded before killing this entity                                                    | No       | Integer        | 2                   |
| chunkCounterLimit         | With enforce333 enabled, the maximum number of chunks per successive frame that are allowed to be forcibly built/downloaded before killing this entity                                                 | No       | Integer        | 6                   |
| tmpDef                    | Reserved                                                                                                                                                                                               |          |                |                     |

```
/**
 * Options for Mod are passed in here as well
 * OPT Number health [-1] - Maximum amount of health entity can have. -1 for invincibility
 * OPT Object mesh - defMesh options
 * OPT Object camera - Modifies camera settings when camera's target is this entity
 *     OPT Vector3 offset [0, 0, 0] - Offset from the target's position
 *     OPT Number minPitch [0] - Minimum pitch angle, in radians (0 is looking straight down, PI is straight up)
 *     OPT Number maxPitch [PI] - Maximum pitch angle, in radians (0 is looking straight down, PI is straight up)
 *     OPT Number minDst [0] - Minimum orbit distance/zoom
 *     OPT Number maxDst [-1] - Maximum orbit distance/zoom, -1 for no limit
 *     OPT Number defaultDst [minDst] - Default orbit distance after calling targetEntity()
 *     OPT Number flingDeceleration [180] - Amount of deceleration when flinging the camera dir around on touchscreen (Infinity = immediate stop, 0 = never stop)
 *     OPT Number fov [CAM_FOV_DEFAULT] - Field of view Y, in radians
 * OPT Array mountPoints - Array of mount point objects. The order of the mount point array determines in what order the mount points fill up when the index is not specified in mount()
 *     REQ Vector3 mount - Moint point position, relative to the entity's current position
 *     OPT Vector3 dismount [0, 0, 0] - Position relative to the mount point, where the entity dismounts at. Recommend not having this at ground level or else you might fall through the ground if vehicle is tilted left or right on a slope
 * OPT Object mountOffset - Offsets this entity while it's mounted
 *     OPT Vector3 pos
 *     OPT Euler rot
 *     OPT Vector3/Number scl - Use number type for [number, number, number]
 * OPT Integer frameCounterLimit [2] - With enforce333 enabled, the maximum number of successive frames that chunks are allowed to be forcibly built/downloaded before killing this entity
 * OPT Integer chunkCounterLimit [6] - With enforce333 enabled, the maximum number of chunks per successive frame that are allowed to be forcibly built/downloaded before killing this entity
 * RES tmpDef
 */
```
