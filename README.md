EMT: Enhanced-Memory Transformer for Coherent Paragraph Video Captioning
=====
PyTorch code for our ICTAI 2021 paper "EMT: Enhanced-Memory Transformer for Coherent Paragraph Video Captioning" Enhanced
by [Leonardo Vilela Cardoso](http://lattes.cnpq.br/6741312586742178), [Silvio Jamil F. Guimarães](http://lattes.cnpq.br/8522089151904453) and 
[Zenilton K. G. Patrocínio Jr](http://lattes.cnpq.br/8895634496108399), 


A coherent description is an ultimate goal concerning video captioning through multiple sentences since it may directly impact consistency and intelligibility. A paragraph describing a video is affected by different events extracted from it. When generating a new event, it should produce a detailed narrative of the video content. But it also might provide some clues that may help reduce the textual repetition occurring in the final description. Recently, transformers have emerged as an appealing solution to several tasks, including video captioning. An augmented transformer with a memory module can somehow cope with text repetition. Thus, to further increase the coherence among the generated sentences, we propose the adoption of attention mechanisms to enhance memory data in a memory-augmented transformer. This new approach, called Enhanced-Memory Transformer (EMT), assesses the data importance (about the video segments) contained in the memory module and uses that to improve readability by reducing repetition. Experimental evaluation of EMT using the test split of the ActivityNet Captions dataset achieved 22.84 in CIDEr-D score, and 4.55 in Reduction-4 score (R@4), representing improvements of 1.03\% and 16.36\%, respectively (compared to the literature). The obtained results show the great potential of this new approach as it provides increased coherence among the various video segments, decreasing the repetition in the generated sentences and improving the description diversity.

## Getting started
### Prerequisites
0. Clone this repository
```
# no need to add --recursive as all dependencies are copied into this repo.
git clone https://github.com/leol30/EMT.git
cd EMT
```

1. Prepare feature files

Download features from Google Drive: [rt_anet_feat.tar.gz (39GB)](https://drive.google.com/file/d/1mbTmMOFWcO30PIcuSpYiZ1rqoy5ltE3A/view?usp=sharing) 
and [rt_yc2_feat.tar.gz (12GB)](https://drive.google.com/file/d/1mj76DwNexFCYovUt8BREeHccQn_z_By9/view?usp=sharing).
These features are repacked from features provided by [densecap](https://github.com/salesforce/densecap#annotation-and-feature). 
```
mkdir video_feature && cd video_feature
tar -xf path/to/rt_anet_feat.tar.gz 
tar -xf path/to/rt_yc2_feat.tar.gz 
```

2. Install dependencies
- Python 2.7
- PyTorch 1.1.0
- nltk
- easydict
- tqdm
- tensorboardX

3. Add project root to `PYTHONPATH`
```
source setup.sh
```
Note that you need to do this each time you start a new session.


### Training and Inference
We give examples on how to perform training and inference with EMT.

0. Build Vocabulary
```
bash scripts/build_vocab.sh DATASET_NAME
```
`DATASET_NAME` can be `anet` for ActivityNet Captions or `yc2` for YouCookII.


1. EMT training

The general training command is:
```
bash scripts/train.sh DATASET_NAME

To train our EMT model on ActivityNet Captions:
```
bash scripts/train.sh anet
```
Training log and model will be saved at `results/anet_re_*`.  
Once you have a trained model, you can follow the instructions below to generate captions. 


2. Generate captions 
```
bash scripts/translate_greedy.sh anet_re_* val
```
Replace `anet_re_*` with your own model directory name. 
The generated captions are saved at `results/anet_re_*/greedy_pred_val.json`


3. Evaluate generated captions
```
bash scripts/eval.sh anet val results/anet_re_*/greedy_pred_val.json
```
The results should be comparable with the results we present at Table 2 of the paper. 
E.g., B@4 10.00; C 22.84 R@4 4.55.

## Citations
If you find this code useful for your research, please cite our paper:
```
@inproceedings{cardoso2021enhanced,
  title={Enhanced-Memory Transformer for Coherent Paragraph Video Captioning},
  author={Cardoso, Leonardo Vilela and Guimaraes, Silvio Jamil F and Patroc{\'\i}nio, Zenilton KG},
  booktitle={2021 IEEE 33rd International Conference on Tools with Artificial Intelligence (ICTAI)},
  pages={836--840},
  year={2021},
  organization={IEEE}
}
```

## Others
This code used resources from the following projects: 
[mart](https://github.com/jayleicn/recurrent-transformer),
[transformers](https://github.com/huggingface/transformers), 
[transformer-xl](https://github.com/kimiyoung/transformer-xl), 
[densecap](https://github.com/salesforce/densecap),
[OpenNMT-py](https://github.com/OpenNMT/OpenNMT-py).

## Contact
Leonardo Vilela Cardoso with this e-mail: lvcardoso@sga.pucminas.br

