# 💡 Light (defLight)

| Name      | Description                 | Required | Type   | Default   |
| --------- | --------------------------- | -------- | ------ | --------- |
| type      | directional, point, or spot | Yes      | String |           |
| pos       |                             | No       | Vec3   | \[0,0,0]  |
| dir       |                             | No       | Vec3   | \[0,0,-1] |
| color     |                             | No       | Color  | "white"   |
| intensity | DirectionalLight            | No       | Number | 1         |
| distance  | PointLight and SpotLight    | No       | Number | 32        |
| decay     | PointLight and SpotLight    | No       | Number | 1         |
| power     | PointLight and SpotLight    | No       | Number | PI        |
| angle     | SpotLight, in radians       | No       | Number | 30        |
| penumbra  | SpotLight                   | No       | Number | 0.5       |

```
/**
 * See three.js docs for more info
 * https://threejs.org/docs/?q=object3d#api/en/lights/Light
 * https://threejs.org/docs/?q=object3d#api/en/lights/DirectionalLight
 * https://threejs.org/docs/?q=object3d#api/en/lights/PointLight
 * https://threejs.org/docs/?q=object3d#api/en/lights/SpotLight
 * 
 * REQ String type - directional, point, or spot
 * OPT Vector3 pos [0, 0, 0]
 * OPT Vector3 dir [0, 0, -1]
 * OPT Color color ["white"]
 * OPT Number intensity [1] - DirectionalLight
 * OPT Number distance [32] - PointLight and SpotLight
 * OPT Number decay [1] - PointLight and SpotLight
 * OPT Number power [PI] - PointLight and SpotLight
 * OPT Number angle [30 degrees] - SpotLight, in radians
 * OPT Number penumbra [0.5] - SpotLight
 */
```
