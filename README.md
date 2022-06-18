# QS-Attn: Query-Selected Attention for Contrastive Learning in I2I Translation (CVPR2022)
 [![arXiv](https://img.shields.io/badge/paper-cvpr2022-green)](https://openaccess.thecvf.com/content/CVPR2022/html/Hu_QS-Attn_Query-Selected_Attention_for_Contrastive_Learning_in_I2I_Translation_CVPR_2022_paper.html) [![arXiv](https://img.shields.io/badge/arXiv-2203.08483-red)](https://arxiv.org/abs/2203.08483)
>Unpaired image-to-image (I2I) translation often requires to maximize the mutual information between the source and the translated images across different domains, which is critical for the generator to keep the source content and prevent it from unnecessary modifications. The self-supervised contrastive learning has already been successfully applied in the I2I. By constraining features from the same location to be closer than those from different ones, it implicitly ensures the result to take content from the source. However, previous work uses the features from random locations to impose the constraint, which may not be appropriate since some locations contain less information of source domain. Moreover, the feature itself does not reflect the relation with others. This paper deals with these problems by intentionally selecting significant anchor points for contrastive learning. We design a query-selected attention (QS-Attn) module, which compares feature distances in the source domain, giving an attention matrix with a probability distribution in each row. Then we select queries according to their measurement of significance, computed from the distribution. The selected ones are regarded as anchors for contrastive loss. At the same time, the reduced attention matrix is employed to route features in both domains, so that source relations maintain in the synthesis. We validate our proposed method in three different I2I datasets, showing that it increases the image quality without adding learnable parameters.

<p align="center">
<img src="./teaser.png" width="800px"/>
<br></p>

<p align="center">
<img src="./arch.png" width="800px"/>
<br>
QS-Attn applies attention to select anchors for contrastive learning in single-direction I2I task
</p>

## Getting Started
### Prerequisites
- Ubuntu 16.04
- NVIDIA GPU + CUDA CuDNN
- Python 3
Please use `pip install -r requirements.txt` to install the dependencies.

## Pretrained Models
We provide Global, Local and Global+Local models for three datasets.
| Model | Cityscapes | Horse2zebra | AFHQ
| :---- | :--------- | :---------- | :---
| Global | [Cityscapes_Global](https://drive.google.com/file/d/1GTevGHIXn0NW2mAzb_3tq5NjkJGVamt5/view?usp=sharing) | [Horse2zebra_Global](https://drive.google.com/file/d/1Nhp34UpFJlQA-FH4J8eqwvp7a_boJNKb/view?usp=sharing) | [AFHQ_Global](https://drive.google.com/file/d/1OHmoTc_rxkMzkstN2caVmAxDkw4F2QVN/view?usp=sharing)
| Local | [Cityscapes_Local](https://drive.google.com/file/d/1uI2G7SXlF5YAo7z9olFFKINtYToTiwbu/view?usp=sharing) | [Horse2zebra_Local](https://drive.google.com/file/d/1TrmGhj5eElSU0doc5ehEAje_G7PC1HCh/view?usp=sharing) | [AFHQ_Local](https://drive.google.com/file/d/13wCMffJibqzKhqOqbpSQ5gdr0WeDdBf9/view?usp=sharing)
| Global+Local | [Cityscapes_Global+Local](https://drive.google.com/file/d/1Cccobqbn67J1rDN5AuFyyIIKasA5bA-y/view?usp=sharing) | [Horse2zebra_Global+Local](https://drive.google.com/file/d/1SP3kf7LNYmpaZZJ7o6N5uPQT-ZjhHIsm/view?usp=sharing) | [AFHQ_Global+Local](https://drive.google.com/file/d/1xvDpD9dbjrZIzT8FjTd8q0dWdhSzNjZx/view?usp=sharing)

## Training
- Download `horse2zebra` dataset :
```
bash ./datasets/download_qsattn_dataset.sh horse2zebra
```
- Train the global model:
```
python train.py \
--dataroot=datasets/horse2zebra \
--name=horse2zebra_global \
--QS_mode=global
```
- You can use visdom to view the training loss:
Run `python -m visdom.server` and click the URL http://localhost:8097.

## Inference
- Test the global model:
```
python test.py \
--dataroot=datasets/horse2zebra \
--name=horse2zebra_qsattn_global \
--QS_mode=global
```

## Citation
If you use this code for your research, please cite
```
@article{hu2022qs,
  title={QS-Attn: Query-Selected Attention for Contrastive Learning in I2I Translation},
  author={Hu, Xueqi and Zhou, Xinyue and Huang, Qiusheng and Shi, Zhengyi and Sun, Li and Li, Qingli},
  journal={arXiv preprint arXiv:2203.08483},
  year={2022}
}
```
