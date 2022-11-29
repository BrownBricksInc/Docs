---
description: >-
  Particles are used for visual effects such as smoke, flames and block
  build/break effects.
---

# VFX | Particle System

### Parameters

| Name              | Description                                                                                     |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| position          | \[x,y,z] position of the particle effect.                                                       |
| rotation          | \[x,y,z] rotation of the particle effect.                                                       |
| positionRange     | \[x,y,z] spread of the particles                                                                |
| parent            | Parent entity such as planet.player                                                             |
| name              | Name of particle instance. This can be used to later retrieve the particle instance.            |
| timeRange         |                                                                                                 |
| numParticles      | Number of particles being displayed in the effect.                                              |
| type              | Type of particle effects: 'star', 'round', 'field', 'circle', 'donut', 'cube', 'basic', 'pixel' |
| lifeTime          |                                                                                                 |
| lifeTimeRange     |                                                                                                 |
| startTime         | Time at which particle effect starts                                                            |
| endTime           | Time at which particle effect ends                                                              |
| startSize         | Starting size of the particle                                                                   |
| startSizeRange    |                                                                                                 |
| endSize           | Ending size of the particle                                                                     |
| endSizeRange      |                                                                                                 |
| sizeRange         |                                                                                                 |
| spinSpeedRange    |                                                                                                 |
| radius            |                                                                                                 |
| velocity          | \[x,y,z] speed of particles                                                                     |
| velocityRange     | \[x,y,z] speed of particles. Will alternate +/- each velocity range                             |
| acceleration      |                                                                                                 |
| accelerationRange |                                                                                                 |
| gravity           |                                                                                                 |
| tween             | Tween effect to use                                                                             |
| blending          | 'normal', 'additive', 'multiply', 'subtractive'                                                 |
| alphaTest         |                                                                                                 |
| colors            | array of colors to loop through                                                                 |

### Adding Particles

#### Add

```
planet.particleEngine.add({ particleOptions });
```

Add flames parented to player

<figure><img src="../.gitbook/assets/Screenshot 2022-11-23 at 11.12.56.png" alt=""><figcaption></figcaption></figure>

```
DEBUG.BB.planet.particleEngine.add({
    parent: DEBUG.BB.planet.player,
    name:[0,1,0].toString(),
    type:"star",
    numParticles: 100,
    position: [0,1,0],
    positionRange: [1,0,1],
    colors:[
    1, 1, 0, 0,
    1, 1, 0, 1,
    1, 0, 0, 1,
    1, 0, 0, 1,
    1, 0, 0, 0.5,
    0, 0, 0, 0
    ],
    lifeTime: 5,
    timeRange: 2,
    startSize: 10,
    endSize: 20,
    velocity: [ 0, 2, 0 ], 
    velocityRange: [ 0, 1, 0 ],
    gravity: [ 0, -0.20, 0 ],
    spinSpeedRange: 4
});
```

#### Remove

```
planet.particleEngine.remove( particleName );
```

Remove flames from player

```
DEBUG.BB.planet.particleEngine.remove([0,1,0].toString());
```

### Examples

#### Rain

```javascript
position:[-1.5, 2, -1.5],
colors:[
    0.7, 0.8, 1, 1 
],
numParticles: 800,
lifeTime: 1,
timeRange: 1,
startSize: 0.05,
endSize: 0.05,
positionRange: [ 1, 0, 1 ],
velocity: [ 0, -2.0, 0 ],
blending:"multiply"
```

#### Rain Ripples

```javascript
type:"donut",
numParticles: 200,
position:[-1.5, 0, -1.5],
colors:[
    0.7, 0.8, 1, 1,
    0.7, 0.8, 1, 0
],
lifeTime: 2,
timeRange: 2,
startSize: 0,
endSize: 0.3,
positionRange: [ 1, 0, 1 ],
oriented:true
```

#### Flame

```javascript
type:"star",
numParticles: 20,
position:[0,0,0],
colors:[
    1, 1, 0, 0,
    1, 1, 0, 1,
    1, 0, 0, 1,
    1, 0, 0, 1,
    1, 0, 0, 0.5,
    0, 0, 0, 0
],
lifeTime: 2,
timeRange: 2,
startSize: 0.3,
endSize: 0.9,
velocity: [ 0, 0.8, 0 ], 
velocityRange: [ 0.15, 0.15, 0.15 ],
gravity: [ 0, -0.20, 0 ],
spinSpeedRange: 4
```

#### Gas

```javascript
type:"basic",
numParticles: 20,
position:[-1,0,0],
colors:[
    0.2, 0.2, 1, 0,
    0.2, 0.2, 1, 1,
    0.2, 0.2, 1, 1,
    0, 0, 1, 1,
    0, 0, 1, 0.5,
    0, 0, 1, 0
],
lifeTime: 2,
timeRange: 2,
startSize: 0.5,
endSize: 0.2,
velocity: [ 0, 0.8, 0 ],
gravity: [ 0, -0.20, 0 ],
spinSpeedRange: 4
```
