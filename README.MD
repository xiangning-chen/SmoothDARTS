# SmoothDARTS (SDARTS)
Code accompanying the paper  
[ICML'2020](https://icml.cc/Conferences/2020): ***Stabilizing Differentiable Architecture Search via Perturbation-based Regularization*** [paper](https://arxiv.org/abs/2002.05283)  
Xiangning Chen, Cho-Jui Hsieh

This code is based on the implementation of [DARTS](https://github.com/quark0/darts), [NAS-Bench-1Shot1](https://github.com/automl/nasbench-1shot1) and [RobustDARTS](https://github.com/MetaAnonym/RobustDARTS).

The stability of DARTS has been challenged for yielding deteriorating architectures as the search proceeds. We find that the precipitous validation loss landscape, which leads to a dramatic performance drop when distilling the final architecture, is an essential factor that causes instability. Based on this observation, we propose a perturbation-based regularization - SmoothDARTS (SDARTS), to smooth the loss landscape and improve the generalizability of DARTS-based methods. In particular, our new formulations stabilize DARTS-based methods by either random smoothing or adversarial attack. Furthermore, we mathematically show that SDARTS implicitly regularizes the Hessian norm of the validation loss, which accounts for a smoother loss landscape and improved performance.

![](fig.png)

## Datasets
Instructions for acquiring PTB is [here](https://github.com/salesforce/awd-lstm-lm/blob/master/getdata.sh). 
While CIFAR-10, CIFAR-100 and SVHN can be automatically downloaded by torchvision.
To use NAS-Bench-1Shot1 to monitor the anytime test accuracy of NAS algorithms, please download this tfrecord:
[https://storage.googleapis.com/nasbench/nasbench_only108.tfrecord](https://storage.googleapis.com/nasbench/nasbench_only108.tfrecord).
Then insert its path to ```nasbench_analysis/eval_darts_one_shot_model_in_nasbench.py```

## Architecture Search
* **Search on NAS-Bench-1Shot1 (3 spaces to choose from):**

```SDARTS-RS: cd optimizers/darts && python train_search.py --search_space=1 --perturb_alpha=random```

```SDARTS-ADV: cd optimizers/darts && python train_search.py --search_space=1 --perturb_alpha=pgd_linf```

* **Search for CNN cells (4 spaces and 3 datasets to choose from):**

```SDARTS-RS: cd sota/cnn && python train_search.py --search_space=s1 --perturb_alpha=random```

```SDARTS-ADV: cd sota/cnn && python train_search.py --search_space=s1 --perturb_alpha=pgd_linf```

* **Search for RNN cells:**

```SDARTS-RS: cd sota/rnn && python train_search.py --perturb_alpha=random```

```SDARTS-ADV: cd sota/rnn && python train_search.py --perturb_alpha=pgd_linf```

## Architecture Evaluation
* Evaluate CNN cells: ```cd sota/cnn && python train.py --auxiliary --cutout```
* Evaluate RNN cells: ```cd sota/rnn && python train.py```

## Reference
If you find this code useful in your research please cite

```
@misc{chen2021stabilizing,
    title={Stabilizing Differentiable Architecture Search via Perturbation-based Regularization}, 
    author={Xiangning Chen and Cho-Jui Hsieh},
    year={2021},
    eprint={2002.05283},
    archivePrefix={arXiv},
    primaryClass={cs.LG}
}
```

## Related Publications
* Xiangning Chen, Ruochen Wang, Minhao Cheng, Xiaocheng Tang, Cho-Jui Hsieh. [DrNAS: Dirichlet Neural Architecture Search](https://openreview.net/forum?id=9FWas6YbmB3). ICLR 2021. [Code](https://github.com/xiangning-chen/DrNAS).
* Ruochen Wang, Minhao Cheng, Xiangning Chen, Xiaocheng Tang, Cho-Jui Hsieh. [Rethinking Architecture Selection in Differentiable NAS](https://openreview.net/forum?id=PKubaeJkw3). ICLR 2021 (oral). [Code](https://github.com/ruocwang/darts-pt).

