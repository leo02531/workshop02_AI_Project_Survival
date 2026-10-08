# Workshop02 Reproducibility Test — GFPGAN Inference
## Project
Repository: https://github.com/leo02531/MLMPworkshop
Inference task: Face restoration using pretrained GFPGANv1.3 model, restore low-quality face images to high resolution.

## Repo map
- Environment: Python 3.8, managed by uv virtual environment
- Entry point: GFPGAN/inference_gfpgan.py
- Model: GFPGANv1.3.pth (pretrained weight)
- Input: evidence/input.jpg (low-quality face photo)
- Output: evidence/output.jpg (restored comparison image)

## Environment setup
Run these uv commands line by line in a fresh clone folder:
```bash
# Create new virtual environment with Python3.8
uv venv --python 3.8 .venv
source .venv/bin/activate

# Install torch and fixed torchvision version
uv pip install torch torchvision==0.15.2

# Install project dependencies
uv pip install -r GFPGAN/requirements.txt

# Install missing dependency RealESRGAN
uv pip install realesrgan

# Editable install GFPGAN package
uv pip install -e GFPGAN/.

## Inference

Exact command to run inference:
python GFPGAN/inference_gfpgan.py -i GFPGAN/inputs/whole_imgs -o GFPGAN/results -v 1.3 -s 2

The pretrained GFPGAN model checkpoint will be automatically downloaded on the first run of the inference script. No manual model download is required.
The final comparison image will be generated in `GFPGAN/results/cmp/`.
Copy the comparison image to `evidence/output.jpg`.

## One real failure

Category: Python module import error
Root cause: Missing `realesrgan` package. GFPGAN relies on RealESRGAN for super-resolution, the default requirements.txt did not automatically install this dependency.
Minimal fix: Run `uv pip install realesrgan` in activated virtual environment.

## AI agent check

Which AI coding agent did you use?: Doubao
What advice did it give?: Guide to rebuild the whole environment from fresh clone, fix torchvision version to avoid functional_tensor warning, diagnose missing module error.
What command or fix did you choose to run yourself?: `uv pip install realesrgan`
How did you verify the result?: Run inference command, check terminal output shows "Results are in the [results] folder", view generated comparison image.

## Part 2 — Peer Reproduction

Reviewer: [Fill student name here]
Reproduction result: PASS / FAIL
If FAIL:
Failed step:
Missing information:
Suggested fix:
