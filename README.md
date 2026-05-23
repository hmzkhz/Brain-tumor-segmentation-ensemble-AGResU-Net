# Brain Tumor Segmentation using AGResU-Net

## Overview
Brain tumor segmentation is a critical step in medical image analysis, enabling accurate diagnosis, treatment planning, and disease monitoring. Manual segmentation is time-consuming. This motivates the use of deep learning approaches.

In this project, we propose an **ensemble learning strategy built on AGResU-Net architectures** to enhance segmentation performance by combining predictions from multiple models.

## Paper
*Attention Gate ResU-Net for Automatic MRI Brain Tumor Segmentation*
## Dataset
**BraTS 2019**: We uploaded a subset as two files HGG and LGG to the Kaggle dataset.

* original dataset: **335 patients** (259 HGG + 76 LGG)
* Subset used: **160 patients** (128 HGG + 32 LGG), preserving the 80/20 ratio

## Models Used
- U-Net
- ResU-Net
- AGU-Net
- AGResU-Net

## Enhancements
- Ensemble Learning
- Test-Time Augmentation

## Results
* Paper Results

| Model       | DSC-Whole | DSC-Core | DSC-Enh | HD95-W | HD95-C | HD95-E |
| ----------- | --------: | -------: | ------: | -----: | -----: | -----: |
| U-Net†      |     0.864 |    0.746 |   0.696 |      - |      - |      - |
| ResU-Net†   |     0.867 |    0.760 |   0.704 |      - |      - |      - |
| AGU-Net†    |     0.870 |    0.760 |   0.700 |      - |      - |      - |
| AGResU-Net† |     0.870 |    0.777 |   0.709 |      - |      - |      - |

* Our Results

| Model            | DSC-Whole | DSC-Core | DSC-Enh | HD95-W | HD95-C | HD95-E |
| ---------------- | --------: | -------: | ------: | -----: | -----: | -----: |
| U-Net            |     0.701 |    0.712 |   0.768 |   9.23 |   5.42 |   3.14 |
| ResU-Net         |     0.694 |    0.700 |   0.781 |   8.37 |   6.05 |   3.43 |
| AGU-Net          |     0.711 |    0.702 |   0.783 |   9.98 |   6.51 |   3.10 |
| AGResU-Net       |     0.721 |    0.694 |   0.770 |  10.60 |   5.68 |   3.50 |
| AGU-Net + TTA    |     0.713 |    0.718 |   0.795 |   9.88 |   5.47 |   3.45 |
| AGResU-Net + TTA |     0.726 |    0.716 |   0.793 |  10.03 |   5.38 |   3.39 |
| Ensemble (TTA)   |     0.724 |    0.717 |   0.800 |   8.61 |   5.19 |   3.41 |



## Key Findings
* The table below shows the DSC improvement from the best individual base model to the esemble (TTA): 

| Tumor Region     | Best Base Model (DSC) | Ensemble (TTA) DSC |   Gain |
| ---------------- | --------------------: | -----------------: | -----: |
| Whole Tumour     |    0.721 (AGResU-Net) |              0.724 | +0.003 |
| Core Tumour      |         0.712 (U-Net) |              0.717 | +0.005 |
| Enhancing Tumour |       0.783 (AGU-Net) |              0.800 | +0.017 |

The enhancing tumour region saw the most meaningful gain (+0.017 DSC). This is 
significant as enhancing tumour is the most important region for treatment planning. 
Whole and core tumour gains were smaller but consistent. 
For the HD95 case, it measures the 95th percentile surface distance between prediction 
and ground truth. The ensemble improved HD95 on the core tumour region (5.42 → 5.19) 
but unfortunately showed marginal degradation on whole and enhancing tumour 
compared to the single best individual model. This is expected behaviour where 
ensemble averaging softens sharp boundaries slightly, which can increase the maximum 
surface distance on some samples even while improving the overall DSC. 

