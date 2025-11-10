# Goal

Sliced code bits relative to Andrej's [nano gpt video](https://www.youtube.com/watch?v=kCc8FmEb1nY) and [github](https://github.com/karpathy/ng-video-lecture). You will need a GPU to finish, either 100$ cloud or 300$ GPU, tired with 300$ version as it can be rerun many times.

# Steps

## Installation to run on CPU untill 61 minutes (dev-gpt_61)
1. Install conda
2. conda env create --file environment.yml
3. conda activate
4. jupter lab

## Installation to run on GPU - Jetson(250$ + 512GB memory card)

### Pure Jetson "ORIN" nano software addons
1. [Image flash](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit#intro)
2. Dont change version of ubuntu, just update is fine (```sudo apt update && sudo apt upgrade```)
3. There is some issue with chromium . Fix with this [video](https://www.youtube.com/watch?v=x6bccF3xtRE)
4. ```sudo pip3 install -U jetson-stats``` for jtop
5. Install [cusparselt](https://developer.nvidia.com/cusparselt-downloads?target_os=Linux&target_arch=aarch64-jetson&Compilation=Native&Distribution=Ubuntu&target_version=22.04&target_type=deb_network) some random dependency.
6. [Torch install](https://docs.nvidia.com/deeplearning/frameworks/install-pytorch-jetson-platform/index.html) : check your jetson pack version & install from the correct whl otherwise screwed
7. Test by running ```python3 -c "import torch; print(torch.__version__)"``` if this doesnot show like "2.4.0a0+f70bd71a48" , which means it is gpu . If this is not working google/chatgpt to fix it. 

### Install miniconda
1. wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh -O ~/miniconda3/miniconda.sh
2. cd ~/miniconda3/
3. ./bin/conda init
4. bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
5. conda env create -file environment-jetson.yaml
6. conda activate NANO
7. Rerun the torch & cusparselt from previous step inside your "NANO" env
8. jupyter lab & double check if torch show gpu is present 

### Run the colab
1. Restart jetsonnano
2. GPU memory is small, so will run the colab in commandline
3. ``` jupyter nbconvert --to notebook --execute dev-gpt.ipynb --output output.ipynb```
4. go to miniconda "NANO" env & ```jupyter lab``` & open output.ipynb

## Directly run the code on jetson.
1. Following Bijan's [video](https://www.youtube.com/watch?v=s1uFVfuT2aw)
2. cd nanoGPT/data/shaakeshpeare ; python3 prepare.py
3. cd ../data/shakespeare_char/ ; python3 prepare.py
4. ``` git clone git clone https://github.com/karpathy/nanoGPT.git ```
5. ``` python3 train.py config/train_shakespeare_char.py --compile=False --eval_iters=20 --log_interval=1 --block_size=64 --batch_size=12 --n_layer=4 --n_head=4 --n_embd=128 --max_iters=2000 --lr_decay_iters=2000 --dropout=0.0 ```


# Output
Added to output/ folder with some screeshots.