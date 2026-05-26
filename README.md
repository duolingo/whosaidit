# WhoSaidIt

**WhoSaidIt** is a multilingual dataset for text-based speaker-attribute classification. Given a short text (a sentence or dialogue), the task is to predict binary labels indicating speaker characteristics, such as gender, age group, parental status, dietary preference, and personality traits.

This is a public subset of the dataset introduced in:

> [**WhoSaidIt: Human-LLM Collaborative Annotation for Text-Based Multilingual Speaker-Attribute Classification**](https://arxiv.org/abs/2605.26070)
> Lingyu Gao, Will Monroe, David Smith, Meghan Jemison, Jackie Lee (Duolingo)

---

## Dataset Overview

| Property | Value |
|---|---|
| Languages | English, Spanish, Italian, Korean, Chinese |
| Labels | 9 binary attributes |
| Examples per label | 400 |
| Total examples | 3,600 |
| Format | CSV (one file per label) |

The dataset is sampled separately for each label, so the same text may appear in multiple files, but the files are not aligned to a common set of texts.

---

## Labels

| File | Label | General Definition |
|---|---|---|
| `male.csv` | male | The speaker self-identifies as male. |
| `female.csv` | female | The speaker self-identifies as female. |
| `child.csv` | child | The speaker is a child or teenager. |
| `adult.csv` | adult | The speaker is an adult, or the sentence involves adult themes (e.g., alcoholic or caffeinated beverage consumption). |
| `elderly.csv` | elderly | The speaker is elderly or identified as a grandparent. |
| `parent.csv` | parent | The speaker states or is implied to have children, but does not indicate that the speaker is elderly or a grandparent (to avoid overlap with the elderly label). |
| `meat-eater.csv` | meat-eater | The speaker eats meat, poultry, seafood, or eggs (dairy products excluded). |
| `vegetarian.csv` | vegetarian | The sentence specifically states or implies the speaker is vegetarian. |
| `serious.csv` | serious | The sentence deals with serious or negative themes, such as death, illness, crime, or sadness. |

These are high-level label definitions. In practice, each label is operationalized with additional label-specific requirements, boundary cases, and precision-recall trade-offs, as specified in the released prompts and rationales. These operational rules may go beyond the short definitions shown here. 

Note: certain label dependencies exist by design. For example, `parent` and `elderly` co-occur with `adult`. Mutually exclusive pairs should not both be labeled 1 for the same instance, such as `male`/`female`, `meat-eater`/`vegetarian`, `parent`/`elderly` (see `parent` definition).

---

## Data Format

Each CSV file has three columns:

| Column | Type | Description |
|---|---|---|
| `language` | string | Language of the text (`English`, `Spanish`, `Italian`, `Korean`, `Chinese`) |
| `text` | string | Short input text to classify |
| `true_label` | int | Binary label: `1` (attribute present) or `0` (attribute absent) |

---

## Prompts

The `prompts/` directory contains the LLM classification prompts used in the paper, one JSON file per label. Each file represents the chat-style prompt used for benchmarking, including the system instruction and, where applicable, manually written in-context demonstration turns. The final query uses `{{language}}` and `{{text}}` as placeholders for the input language and text.

Prompt formats may differ slightly across labels because each label was operationalized with its own rationale, boundary cases, output format, and precision-recall trade-off.

---

## Data Statistics

Label distributions in this release (5 public languages):

| Label | Positive (1) | Negative (0) | Total |
|---|---|---|---|
| male | 96 | 304 | 400 |
| female | 69 | 331 | 400 |
| child | 116 | 284 | 400 |
| adult | 199 | 201 | 400 |
| elderly | 93 | 307 | 400 |
| parent | 171 | 229 | 400 |
| meat-eater | 194 | 206 | 400 |
| vegetarian | 91 | 309 | 400 |
| serious | 200 | 200 | 400 |

---

## License

Copyright (c) 2026 Duolingo, Inc.

The dataset files and prompt files in this repository are released under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).

---

## Citation
```
@misc{gao2026whosaidithumanllmcollaborativeannotation,
      title={WhoSaidIt: Human-LLM Collaborative Annotation for Text-Based Multilingual Speaker-Attribute Classification}, 
      author={Lingyu Gao and Will Monroe and David Smith and Meghan Jemison and Jackie Lee},
      year={2026},
      eprint={2605.26070},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2605.26070}, 
}
```