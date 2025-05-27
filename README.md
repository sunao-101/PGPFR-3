# PGPFR
This repository is the official implementation of the submission "[Data-Free Class-Incremental Gesture Recognition with Prototype-Guided Pseudo Feature Replay]"<https://arxiv.org/abs/2505.20049>.

# Abstract
Gesture recognition is an important research area in the field of computer vision. Most gesture recognition efforts focus on close-set scenarios, thereby limiting the capacity to effectively handle unseen or novel gestures. We aim to address class-incremental gesture recognition, which entails the ability to accommodate new and previously unseen gestures over time. Specifically, we introduce a Prototype-Guided Pseudo Feature Replay (PGPFR) framework for data-free class-incremental gesture recognition. This framework comprises four components: Prototype-Guided Pseudo Feature Generation (PGPFG), Variational Prototype Replay  (VPR) for old classes, Truncated Cross-Entropy (TCE) for new classes, and Continual Classifier Re-Training (CCRT). To tackle the issue of catastrophic forgetting, the PFGBP dynamically generates a diversity of pseudo features in an online manner, leveraging class prototypes of old classes along with batch class prototypes of new classes. Furthermore, the VPR enforces consistency between the classifier's weights and the prototypes of old classes, leveraging class prototypes and covariance matrices to enhance robustness and generalization capabilities. The TCE mitigates the impact of domain differences of the classifier caused by pseudo features. Finally, the CCRT training strategy is designed to prevent overfitting to new classes and ensure the stability of features extracted from old classes. Extensive experiments conducted on two widely used gesture recognition datasets, namely SHREC 2017 3D and EgoGesture 3D, demonstrate that our approach outperforms existing state-of-the-art methods by 11.8\% and 12.8\% in terms of mean global accuracy, respectively.


# Datasets

* [EgoGesture3D](https://drive.google.com/file/d/1pHE0Q9MtVS5BLaV2CBN1rLP_Ed7nvfac/view?usp=drive_link): Please refer to the [EgoGesture](https://ieeexplore.ieee.org/document/8299578) paper and the website for the original video dataset and corresponding license.
* [SHREC-2017 train/val/test splits](https://drive.google.com/file/d/1o5T1b_jUG-czGp-xsGOFaVgzEJNEMnmh/view?usp=drive_link): This zip file only contains the split files comprising the list of files. Please refer to the [SHREC 2017 website](http://www-rech.telecom-lille.fr/shrec2017-hand/) to download the dataset.
  
# Dataset preparation

- Replace the dataset directory `root_dir` in `run_trial.sh` with your own local dataset directory
```bash
for  dataset_name  in ${datasets[*]}; do

if [ $dataset_name  =  "hgr_shrec_2017" ]

then

dataset="hgr_shrec_2017"

root_dir="/ogr_cmu/data/SHREC_2017"

elif [ $dataset_name  =  "ego_gesture" ]

then

dataset="ego_gesture"

root_dir="/ogr_cmu/data/ego_gesture_v4"

fi
```  

# Training

- Run all experiments by one command

```

./scripts/run_experiments_all.sh

```

- Run single specific experiments by simply changing some configurations in the `run_experiments_all.sh` file. Running Pgpfr(ours) approach on Shrec-2017 for one trial. If you want to run other baseline experiments, you can choose the corresponding method.

```bash

split_type="agnostic"

CUDA_VISIBLE_DEVICES=0

gpu=0

datasets=("hgr_shrec_2017")

baselines=("Pgpfr")

trial_ids=(0)

n_trials=${#trial_ids[@]}

n_tasks=7

```

If you use our code in your research or applications, please cite it as follows:
```
@misc{wang2025datafreeclassincrementalgesturerecognition,
      title={Data-Free Class-Incremental Gesture Recognition with Prototype-Guided Pseudo Feature Replay}, 
      author={Hongsong Wang and Ao Sun and Jie Gui and Liang Wang},
      year={2025},
      eprint={2505.20049},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2505.20049}, 
}
```
