---
configs:
- config_name: train_49frames_realistic_bg_change
  data_files:
  - split: train
    path: vera-train-set/49-frames/realistic-set1-bg-change.jsonl
- config_name: train_49frames_realistic_obj_add
  data_files:
  - split: train
    path: vera-train-set/49-frames/realistic-set1-obj-add.jsonl
- config_name: train_49frames_realistic_set2_obj_add
  data_files:
  - split: train
    path: vera-train-set/49-frames/realistic-set2-obj-add.jsonl
- config_name: train_49frames_synthetic_bg_change
  data_files:
  - split: train
    path: vera-train-set/49-frames/synthetic-bg-change.jsonl
- config_name: train_49frames_synthetic_obj_add
  data_files:
  - split: train
    path: vera-train-set/49-frames/synthetic-obj-add.jsonl
- config_name: train_81frames_realistic_bg_change
  data_files:
  - split: train
    path: vera-train-set/81-frames/realistic-set1-bg-change.jsonl
- config_name: train_81frames_realistic_obj_add
  data_files:
  - split: train
    path: vera-train-set/81-frames/realistic-set1-obj-add.jsonl
- config_name: train_81frames_realistic_set2_obj_add
  data_files:
  - split: train
    path: vera-train-set/81-frames/realistic-set2-obj-add.jsonl
- config_name: train_81frames_synthetic_bg_change
  data_files:
  - split: train
    path: vera-train-set/81-frames/synthetic-bg-change.jsonl
- config_name: train_81frames_synthetic_obj_add
  data_files:
  - split: train
    path: vera-train-set/81-frames/synthetic-obj-add.jsonl
- config_name: test_bg_change
  data_files:
  - split: test
    path: vera-test-set/bg-change/bg-change.jsonl
- config_name: test_obj_add
  data_files:
  - split: test
    path: vera-test-set/obj-add/obj-add.jsonl
language:
- en
task_categories:
- text-to-video
- image-to-video
tags:
- video
- video-editing
- layered-video
- background-replacement
- object-addition
- alpha-matting
---

# Dataset Card for Vera 

---

## Dataset Description

- **Curated by:** [Hongkai Zheng](https://devzhk.github.io/), [Ta-Ying Cheng](https://ttchengab.github.io/), [Benjamin Klein](https://scholar.google.com/citations?user=xkX9W9QAAAAJ&hl=en), [Yisong Yue](https://yisongyue.com/), [Zhuoning Yuan](https://zhuoning.cc/)
- **Language(s) (NLP):** English
- **License:** [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
- **Paper:** [Vera: A Layered Diffusion Model for Content-Preserving Video Editing](https://arxiv.org/abs/XXXX.XXXXX)

## Uses

```python
from datasets import load_dataset

# Load training split (49-frame realistic background replacements)
ds = load_dataset("netflix/Vera-Layered-Video", "train_49frames_realistic_bg_change")

# Load test split (background change)
test = load_dataset("netflix/Vera-Layered-Video", "test_bg_change")
```

## Dataset Preview

Sample data and walkthroughs are available at the following links:
- **Project Page:** [Vera Project Page](YOUR_PROJECT_WEBSITE_URL) — visual examples of background replacement and object addition edits
- **Mini Dataset:** [hzzheng/vera-data-mini](https://huggingface.co/datasets/hzzheng/vera-data-mini) — a small downloadable subset for quick inspection
- **Dataset Viewer:** Browse samples directly on the [Hugging Face dataset page](https://huggingface.co/datasets/netflix/Vera-Layered-Video)

---

## Dataset Structure

### Splits

| Split | Edit Type | # Samples |
|---|---|---|
| train / 49-frames / realistic-set1-bg-change | background_replace | 914 |
| train / 49-frames / realistic-set1-obj-add | obj_add | 470 |
| train / 49-frames / realistic-set2-obj-add | obj_add | 770 |
| train / 49-frames / synthetic-bg-change | background_replace | 4,994 |
| train / 49-frames / synthetic-obj-add | obj_add | 4,848 |
| train / 81-frames / realistic-set1-bg-change | background_replace | 457 |
| train / 81-frames / realistic-set1-obj-add | obj_add | 235 |
| train / 81-frames / realistic-set2-obj-add | obj_add | 385 |
| train / 81-frames / synthetic-bg-change | background_replace | 2,497 |
| train / 81-frames / synthetic-obj-add | obj_add | 2,431 |
| **Train Total** | | **18,001** |
| test / bg-change | background_replace | 69 |
| test / obj-add | obj_add | 72 |
| **Test Total** | | **141** |

### Data Fields

#### Training set fields

| Field | Type | Description |
|---|---|---|
| `edit_instruction` | string | Natural-language instruction describing the desired edit |
| `input_video_path` | string | Relative path to the input video (MP4) |
| `edit_rgb_path` | string | Relative path to the RGB edit layer (MP4) |
| `edit_alpha_path` | string | Relative path to the alpha/matte layer (MP4) |
| `mask_path` | string | Relative path to the binary foreground mask video (MP4) |
| `composite_path` | string | Relative path to the final composited output video (MP4) |

#### Test set fields

| Field | Type | Description |
|---|---|---|
| `video_id` | string | Unique video identifier |
| `input_path` | string | Relative path to the input video (MP4) |
| `subject_type` | string | Type of foreground subject (e.g., `person`, `people`, or `null`) |
| `prompt_id` | string | Prompt identifier for multi-prompt videos |
| `prompt` | string | Natural-language edit instruction |
| `target_caption` | string | Detailed caption describing the target edited scene |
| `source_caption` | string | (obj_add only) Caption describing the original scene |
| `edit_type` | string | `background_replace` or `obj_add` |
| `mask_path` | string | Relative path to the foreground mask video (MP4) |
| `alpha_path` | string | Relative path to the alpha layer, if available |

---

## Data Sources

### Training Set

| Source | License |
|---|---|
| [Pexels](https://www.pexels.com/) | [Pexels License](https://www.pexels.com/license/) — Free to use for commercial and non-commercial purposes; no attribution required |
| [Mixkit](https://mixkit.co/) | [Mixkit License](https://mixkit.co/license/) — Free to use for commercial and personal projects; no attribution required |
| [VideoMatte240K](https://grail.cs.washington.edu/projects/background-matting-v2/) | [MIT License](https://github.com/PeterL1n/BackgroundMattingV2/issues/208) — Free to use, modify, and distribute with attribution |

### Test Set

The test set is sourced from the training sources above, plus:

| Source | License |
|---|---|
| [DAVIS](https://davischallenge.org/) | [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) — Non-commercial research use only |
| [VACEBench](https://ali-vilab.github.io/VACE-page/) | [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) — Free to use with attribution |

---

## Layered Video Representation

A key feature of this dataset is the **layered decomposition** of edited videos. Rather than providing only a final composited result, each training sample exposes the full editing pipeline outputs:

1. **Input video** — original unedited footage
2. **Edit RGB layer** — the edited foreground/background element in full color
3. **Edit alpha layer** — a per-pixel transparency matte for the edit layer
4. **Foreground mask** — binary mask isolating the preserved subject
5. **Composite** — the final result blending the edit layer over the original via the alpha matte

This layered format enables models to learn explicit alpha-aware video editing rather than treating editing as a black-box pixel transformation.

---

## Citation

```bibtex
@article{zheng2026vera,
    title     = {Vera: A Layered Diffusion Model for Content-Preserving Video Editing},
    author    = {Zheng, Hongkai and Cheng, Ta-Ying and Klein, Benjamin and Yue, Yisong and Yuan, Zhuoning},
    journal   = {arXiv preprint},
    year      = {2026}
}
```

---

## Dataset Card Contact

[Zhuoning Yuan](mailto:zyuan@netflix.com)
