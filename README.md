# EAES: Effective Augmented Embedding Spaces for Text-based Image Captioning

Pytorch implementation for the IEEE Access paper: [EAES: Effective Augmented Embedding Spaces for Text-based Image Captioning]()

![](https://i.imgur.com/EhVScIV.png)
Fig 1. An overview of our proposed EAES embedding module includes an objects-augmented module for augmenting spatial location information between objects as well as OCR tokens and grid features augmentation module for augmenting the global context features of the image.

## Installation

Clone this repository, and build it with the following command.

```
cd EAES_m4c
pip install -r requirements.txt
python setup.py build develop
```

## Materials

* The TextCaps dataset is able to be downloaded at the [official site](https://textvqa.org/textcaps/dataset/#).
* Grid features can be extracted from images via using the official repo at [https://github.com/facebookresearch/grid-feats-vqa](https://github.com/facebookresearch/grid-feats-vqa).
* BUTD features for visual objects and OCR tokens can found at the baseline M4C-Captioner repo at [M4C-Captioner](https://github.com/ronghanghu/mmf).
* RelDN, VinVL features can be extracted from images via using SGG benchmark toolbox which is available at [https://github.com/microsoft/scene_graph_benchmark](https://github.com/microsoft/scene_graph_benchmark).

However, we have extracted these mentioned features for this study, which anyone can be access via the links below:

| # | Type of feature | Features | Imdb file |
| -------- | -------- | -------- | -------- |
| 1     | BUTD      | [updating]()     | [updating]() |
| 2     | RelDN     | [updating]()     | [updating]() |
| 3     | VinVL     | [updating]()     | [updating]() |



## Training

Run following command

```
CUDA_VISIBLE_DEVICES=[your gpu ids] python tools/run.py \
--tasks captioning \
--datasets m4c_textcaps \
--model m4c_captioner \
--config configs/captioning/m4c_textcaps/m4c_captioner.yml \
--save_dir [save_dir]
```

Modify the `save_dir` with the path you expect the trained model will be saved at.

Note that in `m4c_captioner.yml` file you should modify the correct features path.

```
dataset_attributes:
  m4c_textcaps:
    image_features:
      test:
      - [image test feature path], [ocr test feature path]
      train:
      - [image train feature path], [ocr train feature path]
      val:
      - [image train feature path], [ocr train feature path]
    imdb_files:
      test:
      - [your path]/imdb_val_filtered_by_image_id.npy
      train:
      - [your path]/imdb_train.npy
      val:
      - [your path]/imdb_val_filtered_by_image_id.npy
```

Replace `image test feature path`, `image train feature path`, `ocr te feature path`, `ocr train feature path`, with the features path for visual objects and ocr tokens you downloaded at Materials section

## Inference

The inference process can be easily done by running following command:

```
CUDA_VISIBLE_DEVICES=[your gpu ids] python tools/run.py \
--tasks captioning \
--datasets m4c_textcaps \
--model m4c_captioner \
--config configs/captioning/m4c_textcaps/m4c_captioner.yml \
--save_dir [your save path] \
--resume_file [your final checkpoint path] \
--evalai_inference 1 \
--run_type inference
```

The final checkpoint should be named `m4c_captioner_final.pth` and is store at `[your save path]/m4c_textcaps_m4c_captioner/`.

## Citation

If you use any part of our code in your research, please cite our paper:

```BibTex
@article{khang2022effective,
  title={EAES: Effective Augmented Embedding Spaces for Text-based Image Captioning},
  author={Khang, Nguyen and Doanh, C. Bui and Truc, Trinh and Nguyen, D. Vo},
  journal={IEEE Access},
  year={2022},
  publisher={IEEE}
}
```

## Acknowledgement

The code is greatly inspired by the [M4C-Captioner](https://github.com/ronghanghu/mmf).
