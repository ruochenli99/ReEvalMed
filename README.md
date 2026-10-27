# ReEvalMed

**Rethinking Medical Report Evaluation by Aligning Metrics with Real-World Clinical Judgment**
*EMNLP 2025 (Main Conference)*

Ruochen Li\*, Jun Li\*, Bailiang Jian, Kun Yuan, Youxiang Zhu  (\*equal contribution)

[![Paper](https://img.shields.io/badge/Paper-EMNLP%202025-blue)](https://aclanthology.org/2025.emnlp-main.598/)
[![arXiv](https://img.shields.io/badge/arXiv-2510.00280-b31b1b)](https://arxiv.org/abs/2510.00280)
[![Dataset](https://img.shields.io/badge/Dataset-PhysioNet-2e7d32)](https://doi.org/10.13026/esap-z328)
[![DOI](https://img.shields.io/badge/DOI-10.13026%2Fesap--z328-lightgrey)](https://doi.org/10.13026/esap-z328)

---

## 📢 News

- **[Oct 2026]** 🎉 The **ReEvalMed dataset (v1.0.0) is now released on PhysioNet**: <https://doi.org/10.13026/esap-z328>
- **[2025]** ReEvalMed is published at the EMNLP 2025 Main Conference.

---

## Overview

**ReEvalMed** is a clinically grounded meta-evaluation framework for assessing the reliability of radiology report generation metrics. Many existing metrics assign high scores to generated reports yet fail to capture clinical semantics. ReEvalMed evaluates metrics against what clinicians actually need, along four criteria:

| Criterion | Question it answers |
|---|---|
| **Clinical alignment** | Does the metric react to the 12 aspects of a report that matter clinically? |
| **Discrimination** | Does it penalize clinically *significant* errors? |
| **Robustness** | Does it tolerate clinically *insignificant* variation (e.g. rephrasing)? |
| **Monotonicity** | Does the score drop consistently as error severity increases? |

We find that no widely used metric (BLEU, ROUGE-L, METEOR, BERTScore, AlignScore, RaTEScore, CheXbert-F1, RadGraph-F1, GREEN) satisfies all of these criteria.

---

## 📊 Dataset

The dataset consists of **400 expert-validated GT–ME pairs**: a ground-truth radiology report (GT) paired with a rewritten "meta-evaluation" report (ME) that contains a targeted, controlled change.

- **Source reports:** 50 reports from MIMIC-CXR and 20 information-rich reports from ReXVal
- **Error types:** Omission, Fabrication, Inaccuracy
- **12 evaluation aspects:** Location, Severity, Description, Negation, Modality, Size/Distance, Comparison/Progression, Internal Contradiction, Uncertainty, Terminology, Noise, Stylistic Variation
- **Labels per pair:** clinical significance (significant / insignificant), error type, and a free-text explanation
- **Monotonicity subset:** rewrites grouped into five severity levels (0 = stylistic variation → 4 = logical contradiction)
- All pairs were reviewed and validated by experienced clinicians.

### Access

The dataset is hosted on PhysioNet: **<https://doi.org/10.13026/esap-z328>**

Because it is derived from MIMIC-CXR and ReXVal, it is distributed under the same terms as its source data. To get access:

1. Create a [PhysioNet](https://physionet.org/) account and complete credentialing.
2. Complete the training required on the dataset page.
3. Sign the data use agreement on the [dataset page](https://doi.org/10.13026/esap-z328).
4. Download the files from the page, or from the command line:

```bash
wget -r -N -c -np --user YOUR_PHYSIONET_USERNAME --ask-password https://physionet.org/files/reevalmed/1.0.0/
```

> Please do **not** redistribute the data or share it with anyone who has not signed the data use agreement. The dataset is intended for research use only and must not be used for clinical decision-making.

---

## 💻 Code

`ehr_metrics_run.zip` contains the scripts we used to score GT–ME pairs with the evaluated metrics:

| File / folder | Purpose |
|---|---|
| `run_data.py` | Batch-scores GT–ME pairs with a metric and saves the results |
| `convert_data.py` | Converts the annotation spreadsheet into JSON |
| `re_group_data.py` | Splits the data into discrimination, robustness and monotonicity subsets |
| `CXRMetric/` | BLEU, BERTScore, CheXbert and RadGraph-based metrics |
| `green.py`, `rate.py` / `run_rate.py`, `run_radfact.py` | GREEN, RaTEScore and RadFact |
| `FineRadScore/`, `RadFact/` | Third-party metric implementations used in our comparison |

---

## 📝 Citation

If you use ReEvalMed, please cite our paper **and** the dataset:

```bibtex
@inproceedings{li2025reevalmed,
  title     = {ReEvalMed: Rethinking Medical Report Evaluation by Aligning Metrics with Real-World Clinical Judgment},
  author    = {Li, Ruochen and Li, Jun and Jian, Bailiang and Yuan, Kun and Zhu, Youxiang},
  booktitle = {Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing},
  pages     = {11823--11837},
  year      = {2025}
}

@misc{li2026reevalmed_dataset,
  title     = {ReEvalMed: Rethinking Medical Report Evaluation by Aligning Metrics with Real-World Clinical Judgment (version 1.0.0)},
  author    = {Li, Ruochen and Xia, Yufei and Zhu, Youxiang and Li, Jun and Jian, Bailiang and Yuan, Kun},
  publisher = {PhysioNet},
  year      = {2026},
  note      = {RRID:SCR_007345},
  doi       = {10.13026/esap-z328},
  url       = {https://doi.org/10.13026/esap-z328}
}
```

Formal dataset citation (as provided by PhysioNet):

> Li, R., Xia, Y., Zhu, Y., Li, J., Jian, B., & Yuan, K. (2026). ReEvalMed: Rethinking Medical Report Evaluation by Aligning Metrics with Real-World Clinical Judgment (version 1.0.0). PhysioNet. RRID:SCR_007345. https://doi.org/10.13026/esap-z328

PhysioNet also asks users to cite the platform:

> Goldberger, A., Amaral, L., Glass, L., Hausdorff, J., Ivanov, P. C., Mark, R., ... & Stanley, H. E. (2000). PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals. *Circulation*, 101(23), e215–e220.

Please also acknowledge the source datasets, [MIMIC-CXR](https://physionet.org/content/mimic-cxr/) and [ReXVal](https://physionet.org/content/rexval-dataset/1.0.0/).

---

## 📬 Contact

Questions or issues? Open a GitHub issue or email **liruochen8@gmail.com**.
