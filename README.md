# InstructuDrag-Move125

A collection of **125 image samples** for point-guided image editing. Each sample includes an image, a mask, point annotations, and text prompts. Sample folders retain their original names.

## Structure

```text
<sample_id>/
├── original.jpg   # Input image
├── mask.npy       # NumPy mask array
├── points.json    # Two annotated points and a text description
└── prompt.json    # initializer_token, prompt, and prompt_t
```

- `points.json` contains the fields `points` and `prompt`.
- `prompt.json` preserves the original text fields without rewriting them.
- Masks are `uint8` arrays with three channels: 123 are `512 × 512 × 3`, one is `768 × 768 × 3`, and one is `1536 × 1536 × 3`.
- The dataset contains 500 data files, approximately 106 MiB in total. Generated `dragflow/` results are excluded.

## Download

```bash
git clone https://github.com/hrann-YU/instructudrag-move125.git
cd instructudrag-move125
```

The files are stored directly in Git; Git LFS is not required.

## Load a sample

```python
import json
from pathlib import Path

import numpy as np
from PIL import Image

sample = Path("cat_0")
image = Image.open(sample / "original.jpg")
mask = np.load(sample / "mask.npy", allow_pickle=False)
points = json.loads((sample / "points.json").read_text(encoding="utf-8"))
prompts = json.loads((sample / "prompt.json").read_text(encoding="utf-8"))
```
