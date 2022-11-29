# 🚗 Vehicle

Options for RigidBody are passed in here as well. They become the options for the chassis. The mesh should NOT have the wheels as descendant nodes

| Name             | Description                                                                                                                                                       | Required | Type    | Default    |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------- | ---------- |
| inertiaTensor    | https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxRigidBody.html#a755d0c8a8d1dd8b29e59d50a6dfda5fd                                   | No       | Vec3    | \[0,0,0]   |
| maxSteering      | Maximum steering angle in radians                                                                                                                                 | No       | Number  | 35 degrees |
| steeringSpeed    | How fast the steering angle changes in response to keyboard, in radians/second                                                                                    | No       | Number  | 5          |
| chassisMass      |                                                                                                                                                                   | No       | Number  | 1500       |
| centerOfMass     | Relative to origin of chassisPxGeom                                                                                                                               | No       | Vec3    | \[0,0,0]   |
| hitsPerWheel     | nbHitsPerQuery https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/group\_\_vehicle.html#ga609c26d70a0e7452c313ebe8c58d9da5                   | No       | Number  | 8          |
| sweepWidthScale  | See hitsPerWheel URL                                                                                                                                              | No       | Number  |            |
| sweepRadiusScale | See hitsPerWheel URL                                                                                                                                              | No       | Number  |            |
| driverIndex      | Index of the mount point of the driver's seat                                                                                                                     | No       | Integer | 0          |
| drivableSurfaces | List of drivable surfaces to be added using addDrivableSurface. Default drivable surface type for "bb.default" is required, or else vehicles will slide all over! | No       | Array   |            |
| wheels           | List of wheels to be added using addWheel(). Wheels are recommended                                                                                               | No       | Array   |            |
| lights           | Array of defLight options                                                                                                                                         | No       | Array   |            |

```
/**
 * Options for RigidBody are passed in here as well. They become the options for the chassis. The mesh should NOT have the wheels as descendant nodes
 * OPT Vector3 inertiaTensor [0, 0, 0] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxRigidBody.html#a755d0c8a8d1dd8b29e59d50a6dfda5fd
 * OPT Number maxSteering [35 degrees] - Maximum steering angle in radians
 * OPT Number steeringSpeed [5] - How fast the steering angle changes in response to keyboard, in radians/second
 * OPT Number chassisMass [1500]
 * OPT Vector3 centerOfMass [0, 0, 0] - Relative to origin of chassisPxGeom
 * OPT Number hitsPerWheel [8] - nbHitsPerQuery https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/group__vehicle.html#ga609c26d70a0e7452c313ebe8c58d9da5
 * OPT Number sweepWidthScale [1] - See hitsPerWheel URL
 * OPT Number sweepRadiusScale [1] - See hitsPerWheel URL
 * OPT Integer driverIndex [0] - Index of the mount point of the driver's seat
 * OPT Array drivableSurfaces - List of drivable surfaces to be added using addDrivableSurface. Default drivable surface type for "bb.default" is required, or else vehicles will slide all over!
 *     REQ Object friction - By default, all tire types have a friction value of 1 when in contact with this drivable surface
 *         REQ Number [name of tire type] - Amount of friction between this drivable surface and this type of tire. You may add as many tire types as needed.
 *         REQ Number [name of tire type] - More tire types, until you have a friction value for each type of tire...
 * REQ String material - This is the name of a block type (ie. "bb.block.world.grass")
 * OPT Array wheels - List of wheels to be added using addWheel(). Wheels are recommended
 *     REQ Number radius
 *     REQ Number width
 *     REQ Vector3 pos - Physics position of the center of the wheel, relative to the entity position. x cannot be 0
 *     REQ String type - Name of tire type, associated with drivable surfaces
 *     OPT Object mesh - defMesh options. Animation is ignored/unused
 *     OPT Boolean canSteer [false] - Usually the front wheels are for steering
 *     OPT Number maxSpeed [35]
 *     OPT Number driveTorque [5500] - Controls acceleration. You can make a FWD/RWD vehicle by setting 2 of the wheels' driveTorque to 0
 *     OPT Number brakeTorque [2000]
 *     OPT Number mass [20]
 *     OPT Number maxCompression [0.3] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#a41931d05cc3610c523139d4f975cced6
 *     OPT Number maxDroop [0.1] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#a41931d05cc3610c523139d4f975cced6
 *     OPT Number springStrength [35000] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#ad6c229a583ec71fa2f3192de790528a7
 *     OPT Number springDamperRate [4500] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#abd5b02e608d8d8e06ec7932ccbe514de
 *     OPT Number camberAngleAtRest [0] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#a009eee43a101ae543e3b1fc551792653
 *     OPT Number camberAngleAtMaxDroop [-0.01] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#a20d5e1ae07792ecf7f0180c3456dd5ce
 *     OPT Number camberAngleAtMaxCompression [0.01] - https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleSuspensionData.html#a41931d05cc3610c523139d4f975cced6
 *     OPT Vector3 suspForceAppPointOffset [0, 0.3, 0] - (Center of mass is automatically added on) https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleWheelsSimData.html#acd51a38c9e5cf37b1c0b5feed7b03c04
 *     OPT Vector3 tireForceAppPointOffset [0, 0.3, 0] - (Center of mass is automatically added on) https://gameworksdocs.nvidia.com/PhysX/4.1/documentation/physxapi/files/classPxVehicleWheelsSimData.html#a7914e9b4cbf6a5bbfce66d46f601b440
 * OPT Array lights - Array of defLight options
 */

```
