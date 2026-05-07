This is an unofficial updated version of ConSinGAN. 
I ran this using Python 3.11.9 and PyTorch 2.5.1 with CUDA 12.1 support. 
I've only included the modified files (main_train.py and functions.py), which I modified to resolve dependency issues and redirect them to modern APIs. 
These should replace their original versions in the original.
For more information on the original implementation of ConSinGAN visit: https://github.com/tohinz/ConSinGAN

# Installation
```bash
!git clone https://github.com/tohinz/ConSinGAN
``` 
Update old ConSinGAN requirements
```bash
from pathlib import Path
import re

p = Path("requirements.txt")
text = p.read_text()

# Convert package==old.version into package>=old.version
text = re.sub(r"^([A-Za-z0-9_.-]+)==([^\n]+)$", r"\1>=\2", text, flags=re.MULTILINE)

p.write_text(text)
``` 
```bash
!pip install -r requirements.txt
``` 
# Unconditional Generation
To train a model with the default parameters from ConSinGAN:
```bash
!python main_train.py --gpu 0 --train_mode generation --input_name Images/Generation/angkorwat.jpg
```
#Image Animation
To generate GIFs from the trained model:
```bash
!python main_train.py --gpu 0 --train_mode animation --input_name Images/Animation/lightning1.png
```
```bash
!python evaluate_model.py --gpu 0 --model_dir TrainedModels/lightning1/...
```
#Harmonization
To train a default harmonization model that does not use anything besides the training image:
```bash
!python main_train.py --gpu 0 --train_mode harmonization --train_stages 3 --min_size 250 --lrelu_alpha 0.3 --niter 1000 --batch_norm --input_name Images/Harmonization/scream.jpg
```
If you already have a naive image that you want to use to monitor the progress (naive image only used at test time, not at train time):
```bash
!python evaluate_model.py --gpu 0 --model_dir TrainedModels/scream/.../ --naive_img Images/Harmonization/scream_naive.jpg```
