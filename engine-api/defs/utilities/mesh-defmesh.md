# 📐 Mesh (defMesh)

| Name          | Description                                             | Required | Type    | Default |
| ------------- | ------------------------------------------------------- | -------- | ------- | ------- |
| asset         | Asset name                                              | Yes      | String  |         |
| node          | Child node name, or leave undefined for the entire mesh | No       | String  |         |
| animated      | Whether to import animations                            | No       | Boolean | false   |
| frustumCulled |                                                         | No       | Boolean | true    |
| transform     | defTransform options                                    | No       | Object  |         |

```
/**
 * REQ String asset - Asset name
 * OPT String node - Child node name, or leave undefined for the entire mesh
 * OPT Boolean animated [false] - Whether to import animations. Also disables three.js automatic frustum culling
 * OPT Boolean frustumSpherePos [true]
 * OPT Object transform - defTransform options
*/
```
