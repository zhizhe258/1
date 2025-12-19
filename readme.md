
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

### 4.1 Add Robot Asset to the Scene

Load the scene and create an `Xform` prim.  
Add the SO101 Follower USD as a reference under this `Xform`, then drag the robot to the desired pose.

Record the final transform:
- Translation `(x, y, z)`
- Orientation: quaternion **(w, x, y, z)**

Then run the following script:

```bash
python scripts/tutorials/marble_compose.py \
  --task your_task \
  --background path/of/your/scene.usd \
  --output path/of/your/output.usd \
  --assets-base /path/to/assets \
  --target-pos X Y Z \
  --target-quat W X Y Z
````

<details>
<summary><strong>Parameter descriptions for marble_compose.py</strong></summary>

* `--task`: Task type. Supported values: `toys`, `orange`, `cloth`, `cube`.

* `--background`: Path to the background scene USD.

* `--output`: Output path of the composed USD scene.

* `--assets-base`: Base directory of asset USD files.

* `--target-pos`: Target robot position `(x, y, z)`.

* `--target-quat`: Target robot orientation quaternion `(w, x, y, z)`.

* `--include-table`: Include a task-specific table in the composed scene.

* `--dual-arm`: Enable dual-arm configuration.
  Only supported for `toys` and `cloth` tasks; the **left arm** is used as the reference.

</details>



### 4.2 Table Replacement for Cloth and Toyroom Tasks (Optional)

For **cloth** and **toyroom** tasks, an alternative configuration is provided that replaces the default table.

1. **Create a new `Xform`**
   - Add a new `Xform` prim for the table.

2. **Add the task-specific table**
   - Reference the appropriate table USD based on the task type:
     - `cloth`
     - `toyroom`

3. **Remove original table physics**
   - Disable or remove the physics properties of the original table in the scene.

4. **Add physics to the new table**
   - Add a **collider** and necessary physics properties to the newly created table `Xform`.

5. **Adjust table placement**
   - Drag the table to the desired position.
   - For precise placement:
     - Click the **Play** button to let the table settle and firmly contact the ground.

6. **Record the transformation**
   - Record the table’s:
     - Translation `(x, y, z)`
     - Orientation (Quaternion **WXYZ**)

7. **Generate the updated scene**
   - Run the provided script using the recorded table transformation.
   - A new USD scene with the replaced table will be generated.

---

### 4.3 Dual-Arm Task Configuration

For **dual-arm tasks**, the workflow remains largely the same with one important constraint:

- When adding the robot:
  - **Always drag and place the left arm**
  - The left arm is used as the **reference arm** for the task setup

All other steps (creating `Xform`, recording transforms, generating the scene, and updating asset paths) follow the same procedure as described above.

---

### Notes & Best Practices

- Always verify that the **asset base path** is correctly set before running any script.
- Double-check quaternion order: **WXYZ**, not XYZW.
- Use teleoperation scripts as the final validation step before running task logic.
- Keep a record of all transformation parameters for reproducibility.

