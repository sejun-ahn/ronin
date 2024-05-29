# RoNIN: Robust Neural Inertial Navigation in the Wild

**Paper**: [ICRA 2020](https://ieeexplore.ieee.org/abstract/document/9196860), [arXiv](https://arxiv.org/abs/1905.12853)  
**Website**: http://ronin.cs.sfu.ca/  
**Demo**: https://youtu.be/JkL3O9jFYrE

---
### 변경점
1. "numpy.int"가 deprecated되어 "numpy.int64"로 대체
2. 실제 train dataset과 list.txt 내용이 서로 달라 해당 list 파일 수정
3. IMURecorder 애플리케이션을 이용하여 취득한 데이터만을 이용한 Inference를 위한 코드 수정

### 구동 환경
- python 3.8
- cudatoolkit 11.8
- pytorch 2.3
- numpy 1.24

### Usage:
1. Clone the repository.
2. (Optional) Download the dataset and the pre-trained models<sup>1</sup> from [HERE](https://doi.org/10.20383/102.0543). 
3. Position Networks 
    1. To train/test **RoNIN ResNet** model:
        * run ```source/ronin_resnet.py``` with mode argument. Please refer to the source code for the full list of command 
        line arguments. 
        * Example training command: ```python ronin_resnet.py --mode train --train_list <path-to-train-list> --root_dir 
        <path-to-dataset-folder> --out_dir <path-to-output-folder>```.
        * Example testing command: ```python ronin_resnet.py --mode test --test_list <path-to-train-list> --root_dir 
        <path-to-dataset-folder> --out_dir <path-to-output-folder> --model_path <path-to-model-checkpoint>```.
    2. To train/test **RoNIN LSTM** or **RoNIN TCN** model:
        * run ```source/ronin_lstm_tcn.py``` with mode (train/test) and model type. Please refer to the source code for the 
        full list of command line arguments. Optionally you can specify a configuration file such as ```config/temporal_model_defaults.json``` with the data
         paths.
        * Example training command: ```python ronin_lstm_tcn.py train --type tcn --config <path-to-your-config-file> 
        --out_dir <path-to-output-folder> --use_scheduler```.
        * Example testing command: ```python ronin_lstm_tcn.py test --type tcn --test_list <path-to-test-list> 
        --data_dir <path-to-dataset-folder> --out_dir <path-to-output-folder> --model_path <path-to-model-checkpoint>```.
4. Heading Network
    * run ```source/ronin_body_heading.py``` with mode (train/test). Please refer to the source code 
    for the full list of command line arguments. Optionally you can specify a configuration file such as 
    ```config/heading_model_defaults.json``` with the data paths.
    * Example training command: ```python ronin_body_heading.py train --config <path-to-your-config-file> 
    --out_dir <path-to-output-folder> --weights 1.0,0.2```.
    * Example testing command: ```python ronin_body_heading.py test --config <path-to-your-config-file> 
    --test_list <path-to-test-list>  --out_dir <path-to-output-folder> --model_path <path-to-model-checkpoint>```.

<sup>1</sup> The models are trained on the entire dataset

### Citation
Please cite the following paper is you use the code, paper or data:  
[Herath, S., Yan, H. and Furukawa, Y., 2020, May. RoNIN: Robust Neural Inertial Navigation in the Wild: Benchmark, Evaluations, & New Methods. In 2020 IEEE International Conference on Robotics and Automation (ICRA) (pp. 3146-3152). IEEE.](https://ieeexplore.ieee.org/abstract/document/9196860)
