---
description: The block events system allow for a user to add custom logic to a BB block.
---

# ⌛ Block Events System

## Event Inputs

Callback functions can be added to objects using the `NetEventDispatcher` class. The function is called by the engine when a specific type of event occurs in-game. Events can either be server-sided or client-sided. The “side” of an event determines who runs the callback function: either the client who triggered the event, or the server when any client triggers an event. Prefer to use server-sided events when possible, because the server host is able to automatically synchronise information between all players. Client-sided events are usually only needed when split-second timing is required, for example jump blocks in a platform game or firing a weapon.

```javascript
NetEventDispatcher.prototype.addEventListener(NET_SERVER or NET_CLIENT, "eventname", function(e)
{
	//callback
	console.log(e);
});
```

BlockType extends NetEventDispatcher

| Event           | Description                                                                                                                                                      | Parameters                                           |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| playerfootenter | Triggered when a player steps on top of a block.                                                                                                                 | player, x, y, z                                      |
| playerfootleave | Triggered when a player stops standing on a block.                                                                                                               | player, x, y, z                                      |
| build           | Block’s shape was set to something other than air. If a block's type instantly changes (without breaking it first), both break and build will fire in that order | container: either ChunkScene **or** RBChunk, x, y, z |
| break           | Block’s shape was set to something other than air. If a block's type instantly changes (without breaking it first), both break and build will fire in that order | container: either ChunkScene **or** RBChunk, x, y, z |
| sculpt          | Block’s shape was set to air. If a block's type instantly changes (without breaking it first), both break and build will fire in that order                      | container: either ChunkScene **or** RBChunk, x, y, z |

Planet extends NetEventDispatcher

| Event | Description                                                                                             |   |
| ----- | ------------------------------------------------------------------------------------------------------- | - |
| frame | Fires at the end of each frame. Only use this as a last case resort if you can’t find a better solution |   |

### Adding an event to a block

NET\_SERVER = Run event only on server side. Benefit of synchronisation (and anti-cheat) for all players in server.\
NET\_CLIENT = Run event only on client. Faster response time for player.\
\
_For events that triggered by planet, use the following syntax_

```javascript
planet.addEventListener(NET_SERVER, "frame", function(){})
```

_For events that are triggered by blockType, use the following syntax._

```javascript
getBlock("bb.block.platformer.trapdoor").addEventListener(NET_SERVER, "playerfootenter", async function({ player, x, y, z }){});
```

### Code Example&#x20;

Here is an example of an event that kills the player on touch.

```javascript
client: function()
	getBlock("bb.block.platformer.death").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
	{
		player.addHealth(-player.maxHealth);
	});
}	
```

## Event Outputs

| Event                                                               | Description                                                                                                                  |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| player.addHealth(amount)                                            | Add or subtract health from player.                                                                                          |
| player.serverSetSpeedSprint(speedSprint)                            | Set sprint speed of player.                                                                                                  |
| player.serverSetJumpVelocity(jumpVelocity)                          | Set jump velocity of player. Sets how high a player can jump.                                                                |
| player.serverJump(velocity, force)                                  | Makes a player jump. If force is true then player can jump while not on the ground.                                          |
| player.serverSetCoyoteTime(coyoteTime)                              | Sets coyote time for player.                                                                                                 |
| player.serverSetFallDamage(fallDamage)                              | Sets fall damage for player.                                                                                                 |
| player.serverSetCanFly(bool)                                        | Sets whether a player can fly or not.                                                                                        |
| planet.createEntity(def, nameplate, x, y, z, angle, id, except)     | Creates entity and adds to scene.                                                                                            |
| planet.serverSetMessage(peer, msg, duration)                        | Sets message at top of screen for given peer.                                                                                |
| Entity: setPosition(x, y, z, angle, resetCamera)                    | Set position of entity.                                                                                                      |
| Entity: serverSetPosition(x, y, z, angle, resetCamera)              | Set position of entity.                                                                                                      |
| Entity: serverRespawn()                                             | Respawn method for entities like vehicles and players.                                                                       |
| Entity: mount(ownershipCheck, child, toggle, index)                 | Mounts/dismount an entity to another entities mount point. For example, a player sits in mount point of a vehicle.           |
| scene.setBlock(ax, ay, az, shape, type, triggerEvents, isNet)       | Places a block of a certain block type at a given coordinate.                                                                |
| BlockPhysics.unsnapSingle(container, x, y, z, isExplosion, type)    | Breaks a single block & turns into a physics block.                                                                          |
| BlockPhysics.unsnapChain(container, x, y, z, split)                 | Breaks a block as well as attached blocks & turns into a single physics chunk. Split should be set to false for this effect. |
| BlockPhysics.explosion(container, pos, centerBlock, radius, impact) | Causes an explosion by applying an impulse of magnitude "impact" at a given position and radius.                             |

## Event Examples

#### BlockPhysics.unsnapSingle & scene.setBlock

unsnapSingle is used to turn a block into a physics block. When the player touches the block, the block will be converted to a physics block and will fall to the ground.\
\
After 3 seconds, as long as the initial position of the trapdoor block is still unoccupied, a new trapdoor block will be placed in the original position using scene.setBlock.

```javascript
//must be server sided, at least for now until we can create an RBChunk on the client side
getBlock("bb.block.platformer.trapdoor").addEventListener(NET_SERVER, "playerfootenter", async function({ player, x, y, z })
{
	var scene = player.world.scene;
	var prvShape = scene.getShape(x, y, z);
	
	//"this" refers to the engine's BlockType class instance for trapdoors
	//block's unsnapAnimation must be set to ragdoll in order to get RBChunk
	var rbchunk = BlockPhysics.unsnapSingle(scene, x, y, z, false, this);
	
	//make block spin randomly. clients will not see this!
	rbchunk.phys.setAngularVelocity((Math.random() - 0.5) * 10, (Math.random() - 0.5) * 10, (Math.random() - 0.5) * 10);
	
	await wait(3);
	
	//only build a new trapdoor if the spot is still empty
	if(scene.getShape(x, y, z) === BLOCK_AIR)
	{
		if(!rbchunk.disposed)
			rbchunk.dispose();
		
		scene.setBlock(x, y, z, prvShape, this.name, true);
	}
});
```

#### BlockPhysics.unsnapChain

Will convert all attached physics enabled blocks to physics objects that will fall with gravity.

```javascript
//must be server sided, at least for now until we can create an RBChunk on the client side
getBlock("bb.block.platformer.chaintrapdoor").addEventListener(NET_SERVER, "playerfootenter", async function({ player, x, y, z })
{
	var scene = player.world.scene;
	var prvShape = scene.getShape(x, y, z);
	
	var rbchunk = BlockPhysics.unsnapChain(scene, x, y, z, false);
				
	await wait(3);
	
	//only build a new trapdoor if the spot is still empty
	if(scene.getShape(x, y, z) === BLOCK_AIR)
	{
		if(!rbchunk.disposed)
			rbchunk.dispose();
		
		scene.setBlock(x, y, z, prvShape, this.name, true);
	}
});
```

#### BlockPhyics.explosion

```javascript
getBlock("bb.block.platformer.landmine").addEventListener(NET_SERVER, "playerfootenter", async function({ player, x, y, z })
{
	var radius = 5; // radius of explosion
	var impact = 100000; // each block has a maxImpact property, the explosion must be greater in order to destroy the block
	var explosionPos = new Vector3(x,y,z); // position of explosion

	var scene = player.world.scene;			
	
	player.world.hudPopup.set(null, 'BOOM!', 2);
	player.addHealth(-(player.health/2)); // do damage to player

	BlockPhysics.explosion(scene, explosionPos, explosionPos, 5, impact);
	// second explosion makes blocks go flying
	BlockPhysics.explosion(scene, explosionPos, explosionPos, 5, impact);
});
```

#### planet.createEntity

example found in _src/mods/defs/BlocksSpawners.js_

```javascript
getBlock("bb.block.spawner.ketchupkar").addEventListener(NET_SERVER, "build", async function({ container, x, y, z })
{
	container.world.createEntity("VehicleBroncoRed", null, x + 0.5, y + 6, z + 0.5);
});
```

