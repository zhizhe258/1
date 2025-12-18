
---

## 3. Integrate Visuals and Collisions

In this step, we perform **"Visual-Physics Pairing"**: combining the **Gaussian Splats** (visuals) with the **Mesh Geometry** (physics) inside Isaac Sim to create a simulation-ready scene.

### Step 1: Load and Align Assets

1. **Load Visuals**: Extract your generated `.usdz` file, locate `default.usda`, and drag it into the **Isaac Sim Viewport**. This creates a prim at `/World/gauss`.
2. **Import Collision Mesh**: In the **Stage** panel, create an Xform at `/World/Xform`. Add a **Reference** to your `texture_mesh.glb` file using an **absolute file path**.
3. **Spatial Alignment**: The two assets must overlap perfectly.
* **Common Fix**: Rotate `/World/Xform` by **180° on the Z-axis**.
* **Scaling**: Some scenes may require a scale adjustment (e.g., **100x**).
* *Verification*: Use the wireframe mode to ensure the mesh aligns with the Gaussian splat visual boundaries.



https://www.google.com/search?q=https://github.com/user-attachments/assets/9ab50828-8de1-4d55-b243-c320a7c91cac

### Step 2: Configure Physics and Colliders

To make the mesh interactable while keeping it static:

1. **Add Physics Preset**: Select `/World/Xform` and apply **Add > Physics > Rigid Body with Colliders Preset**.
2. **Set to Kinematic**: In the **Rigid Body** settings, enable **Kinematic**. This ensures the environment doesn't fall due to gravity.
3. **Optimize Collider**: Select `/World/Xform/decimated_mesh`. Under **Physics > Collider**, set **Approximation** to `meshSimplification`.

https://www.google.com/search?q=https://github.com/user-attachments/assets/ab391d89-e228-4476-b55c-cec093ab25f4

### Step 3: Visual Optimization and Export

1. **Refine Visibility**: Click the eye icon for `/World/Xform` to hide the mesh geometry. This keeps only the beautiful Gaussian splats visible while preserving underlying collisions.
2. **Final Export**: Save the combined stage as a single USD file (e.g., `scene.usd`). This will be your primary scene entry point.

https://www.google.com/search?q=https://github.com/user-attachments/assets/59b924ad-2d7c-48b4-b4d4-875af7268438

---

## 4. Add Asset Configuration

Here is the process of adding the assets must be used within the task. Here again use the previous scene we had. create an Xform and add the robot arm as the reference. Then drag the robot to the ideal place you want. Here record the tanformation info, here the tranlation and ori, rememeber here use the quaternion WXYZ format.
Then run the following script with the previuos ideal palce info.
Here would generate a new scene,usd with the assets in it. Then please replace the asset path in  task here. RUN the teleoperation script to check the success.

Here please make sure use the right assetbase path.

For cloth and toyroom task. we offer another choice including the table replacement. Here please create an Xform and add the relavent table usd according to the  task type. here remove the physics property of the original table and add the physics of collider to the new created Xform. drag the table to the ideal place, for exact tranform, ypu can use click the play button to let the table firmly contact with the ground. then record the tranformation info as before. Then run the following code.

And for dual arm tasks, here the process is the same, but the robot you drag make sure it is the left arm, we would use it as a reference.

