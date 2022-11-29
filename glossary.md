# 📘 Glossary

## World

**World** is another name for a game. Each game is its own "world".

**Maps** store the block data of a world - where each block is, its shape, type, and any other data each block may have. They do _NOT_ save entities. A world can have multiple maps, but only one can be loaded at a time.

**Chunks** are cube-shaped regions of the map that contain blocks. By default, the size of a chunk is 16x16x16 blocks.

**Blocks** are static (non-moving) map geometry that live inside chunks. Creators build games using blocks. I like to build brown blocks with Minecrap.

**Props** are 3D models that can be placed in the world. They are a special type of block.

## Entity

**Entities** are objects that are free to move around the world.

**Rigid bodies** are physics objects that can tumble around and react to forces and impulses (such as gravity or a car crash).

**RBChunks** (rigid body chunks) are the result of normal blocks unsnapping from the map grid and becoming rigid bodies. To put it simply, they are physics blocks.

**Vehicles** go vroom vroom skeet skeet.

**Items** are a type of entity you can hold in your hand and use. When used, an item might allow you to place blocks, shoot other players, or do something really epic.

**Projectiles** are typically bullets shot from ranged weapon items.

**Players** need no explanation.

## Mods

**Mods** are pieces of code that are modular and separate from the engine. They can be enabled by importing or including them in the world script.

**World scripts** are the source code of games made within the engine. The script serves as the entry point to the game server, meaning that the host machine (and _only_ the host) will execute it upon loading the world. The world script can contain mods and custom game logic.

**Generators** are scripts that procedurally generate maps. They compute which blocks are in any given chunk.&#x20;

**Defs** (short for definitions) are used to define extra content that can be added to the game, such as blocks or entities.



#### &#x20; 
