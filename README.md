<p align="center">
    <!-- community badges -->
    <a href="https://discord.gg/uMbNqcraFc"><img src="https://dcbadge.vercel.app/api/server/uMbNqcraFc?style=plastic"/></a>
    <!-- doc badges -->
    <a href='https://docs.nerf.studio/'>
        <img src='https://readthedocs.com/projects/plenoptix-nerfstudio/badge/?version=latest' alt='Documentation Status' /></a>
    <!-- pi package badge -->
    <a href="https://badge.fury.io/py/nerfstudio"><img src="https://badge.fury.io/py/nerfstudio.svg" alt="PyPI version"></a>
    <!-- code check badges -->
    <a href='https://github.com/nerfstudio-project/nerfstudio/actions/workflows/core_code_checks.yml'>
        <img src='https://github.com/nerfstudio-project/nerfstudio/actions/workflows/core_code_checks.yml/badge.svg' alt='Test Status' /></a>
    <!-- license badge -->
    <a href="https://github.com/nerfstudio-project/nerfstudio/blob/master/LICENSE">
        <img alt="License" src="https://img.shields.io/badge/License-Apache_2.0-blue.svg"></a>
</p>

<p align="center">
    <!-- pypi-strip -->
    <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://docs.nerf.studio/_images/logo-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://docs.nerf.studio/_images/logo.png">
    <!-- /pypi-strip -->
    <img alt="nerfstudio" src="https://docs.nerf.studio/_images/logo.png" width="400">
    <!-- pypi-strip -->
    </picture>
    <!-- /pypi-strip -->
</p>

<!-- Use this for pypi package (and disable above). Hacky workaround -->
<!-- <p align="center">
    <img alt="nerfstudio" src="https://docs.nerf.studio/_images/logo.png" width="400">
</p> -->

<p align="center"> A collaboration friendly studio for NeRFs </p>

<p align="center">
    <a href="https://docs.nerf.studio">
        <img alt="documentation" src="https://user-images.githubusercontent.com/3310961/194022638-b591ce16-76e3-4ba6-9d70-3be252b36084.png" width="150"></a>
    <a href="https://viewer.nerf.studio/">
        <img alt="viewer" src="https://user-images.githubusercontent.com/3310961/194022636-a9efb85a-14fd-4002-8ed4-4ca434898b5a.png" width="150"></a>
    <a href="https://colab.research.google.com/github/nerfstudio-project/nerfstudio/blob/main/colab/demo.ipynb">
        <img alt="colab" src="https://raw.githubusercontent.com/nerfstudio-project/nerfstudio/main/docs/_static/imgs/readme_colab.png" width="150"></a>
</p>

<img src="https://user-images.githubusercontent.com/3310961/194017985-ade69503-9d68-46a2-b518-2db1a012f090.gif" width="52%"/> <img src="https://user-images.githubusercontent.com/3310961/194020648-7e5f380c-15ca-461d-8c1c-20beb586defe.gif" width="46%"/>

- [Quickstart](#quickstart)
- [Learn more](#learn-more)
- [Supported Features](#supported-features)

# About

### What is different between original repo and this fork?
1. This fork has `ns-process-data splatfacto`
2. This fork uses **all images** for training. But, eval images is splitted by `fraction` or `interval`. Default settings is `fraction`. Eval images is 0,1 of all images.

### Why add this ns-process-data splatfacto?
It mimics `python3 convert.py -s /path/to/input/folder` from Original `Inria 3DGS`

### What is special things about python3 convert.py?

1. original `ns-process-data images` make "images" in output folder become smaller despite has same resolution, it hurts quality.
2. It uses `exhausive_matcher` instead of `vocab_tree_matcher` in `ns-process-data images`
3. it uses hyperparameter of `ba_global_function_tolerance = 0.000001`
4. It uses `colmap image_undistorter`


### So what I get if I use that?
I got extra quality boost, about 0.3 - 0,7 dB in PSNR evaluation of all images. I have tested it on different dataset.

### What is different between this implementation and python3 convert.py.?
1. The original `convert.py` gives result of `colmap` format which does not have `transforms.json` and `sparse_pc.json`. This implementation creates that files so it compatible with NerfstudioDataparser.
2. The original `convert.py` uses `magick command` for resizing images. This repo uses `OpenCV` for resizing images.

### Why uses all training images?
It mimics INRIA 3DGS which uses all images for training data

### Will it be overfitting?
Yes, thats okay for me. Overfitting is not problem because we don't generate entirely new scene. But we must maximize the existing scene quality.

### How about quality?
It increases from 28,7 dB to 29,2 dB PSNR (extra 0,5 dB) for `apartement eyeful tower 1k JPEGs` dataset. Another dataset is not yet tested. Hopefully in short of time.
