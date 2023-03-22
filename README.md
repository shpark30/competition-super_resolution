# Outline
 - 2022.09 Dacon 주관 이미지 초해상화 대회 참여
 - 목적 : AI 휴먼 이미지 생성 Output 화질 개선을 위한 이미지 초해상화 모델 POC
 - 품질이 저하된 저해상도 촬영 이미지(512x512)를 고품질의 고해상도 촬영 이미지(2048x2048)로 생성

# Description
**Competition Link : [AI 양재 허브 인공지능 오픈소스 경진대회](https://dacon.io/competitions/official/235977/overview/description)<p>**

**[Metric]**
PSNR(Peak Signal-to-Noise Ratio)
$$PSNR = 10log_{10}(\frac{R^2}{MSE})$$

**[🚩 Score]**
> **Private Score** : 23.18931 **[28th]** <p>
**Public Score** : 23.73144 **[31th]** <p>
---


# HAT [[Paper Link]](https://arxiv.org/abs/2205.04437) [![Replicate](https://replicate.com/cjwbw/hat/badge)](https://replicate.com/cjwbw/hat)

### Activating More Pixels in Image Super-Resolution Transformer
Xiangyu Chen, [Xintao Wang](https://scholar.google.com.hk/citations?user=FQgZpQoAAAAJ&hl=en), [Jiantao Zhou](https://scholar.google.com/citations?hl=zh-CN&user=mcROAxAAAAAJ) and [Chao Dong](https://scholar.google.com.hk/citations?user=OSDCB0UAAAAJ&hl=zh-CN)

<img src="https://raw.githubusercontent.com/chxy95/HAT/master/figures/Performance_comparison.png" width="600"/>

#### BibTeX

    @article{chen2022activating,
      title={Activating More Pixels in Image Super-Resolution Transformer},
      author={Chen, Xiangyu and Wang, Xintao and Zhou, Jiantao and Dong, Chao},
      journal={arXiv preprint arXiv:2205.04437},
      year={2022}
    }

## Environment
- [PyTorch >= 1.7](https://pytorch.org/)
- [BasicSR == 1.3.4.9](https://github.com/XPixelGroup/BasicSR/blob/master/INSTALL.md) 
### Installation
```
pip install -r requirements.txt
python setup.py develop
```

## How To Test
- Refer to `./options/test` for the configuration file of the model to be tested, and prepare the testing data and pretrained model.  
- The pretrained models are available at
[Google Drive](https://drive.google.com/drive/folders/1HpmReFfoUqUbnAOQ7rvOeNU3uf_m69w0?usp=sharing) or [Baidu Netdisk](https://pan.baidu.com/s/1u2r4Lc2_EEeQqra2-w85Xg) (access code: qyrl).  
- Then run the follwing codes (taking `HAT_SRx4_ImageNet-pretrain.pth` as an example):
```
python hat/test.py -opt options/test/HAT_SRx4_ImageNet-pretrain.yml
```
The testing results will be saved in the `./results` folder.

## How To Train
- Refer to `./options/train` for the configuration file of the model to train.
- Preparation of training data can refer to [this page](https://github.com/XPixelGroup/BasicSR/blob/master/docs/DatasetPreparation.md). ImageNet dataset can be downloaded at the [official website](https://image-net.org/challenges/LSVRC/2012/2012-downloads.php).
- The training command is like
```
CUDA_VISIBLE_DEVICES=0,1,2,3,4,5,6,7 python -m torch.distributed.launch --nproc_per_node=8 --master_port=4321 hat/train.py -opt options/train/train_HAT_SRx2_from_scratch.yml --launcher pytorch
```
- Note that the default batch size per gpu is 4, which will cost about 20G memory for each GPU.  

The training logs and weights will be saved in the `./experiments` folder.

## Results
The inference results on benchmark datasets are available at
[Google Drive](https://drive.google.com/drive/folders/1t2RdesqRVN7L6vCptneNRcpwZAo-Ub3L?usp=sharing) or [Baidu Netdisk](https://pan.baidu.com/s/1CQtLpty-KyZuqcSznHT_Zw) (access code: 63p5).


## Contact
If you have any question, please email chxy95@gmail.com or join in the [Wechat group of BasicSR](https://github.com/XPixelGroup/BasicSR#-contact) to discuss with the authors.
