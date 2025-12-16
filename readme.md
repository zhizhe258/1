# Add a Custom Scene in LeIsaac

This tutorial walks you through how to add a **custom scene** in **LeIsaac**, enabling you to build and evaluate a variety of tasks based on your own environments.

---

## Step 1: Prepare the USD Scene

To add a custom scene in LeIsaac, you first need to prepare a USD-compatible scene using **Marble**.

### 1.1 Create a World in Marble

Navigate to the **[Marble platform](https://marble.worldlabs.ai/)**.

Follow the instructions in the **[Marble documentation](https://docs.worldlabs.ai/)** to create your custom world model. Once you are satisfied with the result, download the following files:


- **Splats file** (`.ply`)
- **High-quality mesh** (`.glb`)

> **Tips:**  
> For best results, please use high-resolution images or videos.  
> It is recommended to refine and finalize the **panorama** before generating the full world.  

---

### 1.2 Convert Splats (PLY) to USDZ

After obtaining the splats file (`.ply`), convert it into **USDZ** format using **NVIDIA 3DGrut**.

#### Install 3DGrut
Download and install the **[3DGrut](https://github.com/nv-tlabs/3dgrut)**.

Follow the installation instructions provided in the repository.

> **Note (RTX 50-Series GPUs):**  
> If you encounter installation issues on RTX 50-series GPUs, here might be helpful:  
> https://github.com/nv-tlabs/3dgrut/issues/167

#### Convert PLY to USDZ

If you have existing Gaussian splat data in **PLY format**, run the following command:

```bash
python -m threedgrut.export.scripts.ply_to_usd path/to/your/splats.ply \
    --output_file path/to/output.usdz
