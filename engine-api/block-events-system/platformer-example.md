# Platformer Example

```javascript
import { wait } from "util/time.js";
import { BlockPhysics } from "planet/chunk/physics.js";
import { BLOCK_AIR } from "planet/chunk/builder.js";
import { Vector3, Box2, Vector2 } from "three";
import { NET_SERVER } from "net/ibs/share/const.js";

export const BlocksPlatformer =
{
	name: "BlocksPlatformer",
	assets: ["assets/engine/mods/BlocksPlatformer/tex-blocks-platformer.png"],
	
	blocks:
	[
		{
			name: "bb.block.platformer.checkpoint",
			display: "Checkpoint",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-checkpoint.jpg" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(0, 0), new Vector2(256, 256)) } }]
		},
		{
			name: "bb.block.platformer.death",
			display: "Block of Death",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-death.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(256, 0), new Vector2(512, 256)) } }]
		},
		{
			name: "bb.block.platformer.superjump",
			display: "Super Jump",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-superjump.jpg" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(0, 256), new Vector2(256, 512)) } }]
		},
		{
			name: "bb.block.platformer.superspeed",
			display: "Super Speed",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-superspeed.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(0, 640), new Vector2(64, 704)) } }]
		},
		{
			name: "bb.block.platformer.trapdoor",
			display: "Trapdoor",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-trapdoor.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(256, 256), new Vector2(512, 512)) } }]
		},
		{
			name: "bb.block.platformer.springjumps",
			display: "Spring Jumps",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-spring.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(0, 512), new Vector2(128, 640)) } }]
		},
		{
			name: "bb.block.platformer.nodamage",
			display: "No Damage",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-nodamage.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(128, 512), new Vector2(256, 640)) } }]
		},
		{
			name: "bb.block.platformer.hoverboots",
			display: "Hover Boots",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-hoverboots.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(256, 512), new Vector2(384, 640)) } }]
		},
		{
			name: "bb.block.platformer.tempflying",
			display: "Flying Enabled",
			meta: { material: { default: "assets/engine/mods/BlocksPlatformer/icons/tex-blocks-platformer-canfly.png" } },
			faces: [{ texture: { asset: "tex-blocks-platformer", pos: new Box2(new Vector2(384, 512), new Vector2(512, 640)) } }]
		}
	],
	
	server()
	{
		var getBlock = (name) => DEBUG.BB.planet.scene.blockName2Type.get(name);
		
		getBlock("bb.block.platformer.checkpoint").addEventListener(NET_SERVER, "playerfootenter", function({ player, x, y, z })
		{
			var newSpawn = new Vector3(x + 0.5, y + 1, z + 0.5);
			if(player.spawnPos.equals(newSpawn)) return;
			
			var planet = player.planet;
			player.serverSetSpawn(newSpawn);
			planet.serverSetMessage(planet.net?.peers.get(player.owner), "Checkpoint reached!", 2);
		});
		
		//must be server sided, at least for now until we can create an RBChunk on the client side
		getBlock("bb.block.platformer.trapdoor").addEventListener(NET_SERVER, "playerfootenter", async function({ player, x, y, z })
		{
			var scene = player.planet.scene;
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
	},
	
	/* javascript-obfuscator:disable */
	//obfuscator enable+disable comments required when client script is inside engine source code
	//colon is required here. no shorthand
	client: function()
	{
		var getBlock = (name) => DEBUG.BB.planet.scene.blockName2Type.get(name);
		
		getBlock("bb.block.platformer.death").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			player.addHealth(-player.maxHealth);
		});
		
		getBlock("bb.block.platformer.superjump").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			powerUpBlock(player, "Super Jump!", 23, 10, player.jumpVelocity, (x) => player.jumpVelocity = x);
		});
		
		getBlock("bb.block.platformer.superspeed").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			powerUpBlock(player, "Super Speed!", 15, 10, player.speedWalk, (x) => player.speedWalk = x);
		});
		
		getBlock("bb.block.platformer.springjumps").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			player.planet.serverSetMessage(null, "Spring Coil!", 4);
			player.jump(300, true);
		});
		
		getBlock("bb.block.platformer.nodamage").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			powerUpBlock(player, "Navi - No Damage!", false, 10, player.fallDamage, (x) => player.fallDamage = x);
		});
		
		getBlock("bb.block.platformer.hoverboots").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			powerUpBlock(player, "Hover Boots!", 10, 10, player.coyoteTime, (x) => player.coyoteTime = x);
		});
		
		getBlock("bb.block.platformer.tempflying").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player })
		{
			powerUpBlock(player, "Flying Enabled - 10 Seconds", true, 10, player.canFly, (x) => player.setCanFly(x));
		});
		
		//make trapdoor block disappear instantly on client side to prevent host advantage
		getBlock("bb.block.platformer.trapdoor").addEventListener(DEBUG.NET_CLIENT, "playerfootenter", function({ player, x, y, z })
		{
			var planet = player.planet;
			if(!planet.isHosting())
				planet.scene.setBlock(x, y, z, 0, "bb.block.platformer.trapdoor", false);
		});
		
		//changes a player property to [newVal] for [time] seconds
		//still need to add a listener for player death that removes powerup
		async function powerUpBlock(player, name, newVal, time, prvVal, cb)
		{
			var planet = player.planet;
			
			var metadata;
			if(player.metadata.has("powerUpData"))
			{
				metadata = player.metadata.get("powerUpData");
			}
			else
			{
				metadata = {};
				player.metadata.set("powerUpData", metadata);
			}
			
			var powerUpData = metadata[name] ??= {};
			
			var prv;
			if(powerUpData.clearTimeout)
			{
				//boost the powerup the player already has
				prv = powerUpData.prv;
				powerUpData.clearTimeout();
			}
			else
			{
				//create new powerup
				prv = prvVal;
				powerUpData.prv = prv;
			}
			
			cb(newVal);
			planet.serverSetMessage(null, name, time); //null for client sided message
			
			var promise = DEBUG.wait(time);
			powerUpData.clearTimeout = promise.clearTimeout; //save the timeout in case it needs to be cancelled by a newer powerup
			await promise;
			
			delete metadata[name];
			cb(prv);
		}
	}
	/* javascript-obfuscator:enable */
};

```
