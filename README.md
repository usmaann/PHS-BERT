# PHS-BERT
We present and release [PHS-BERT](https://arxiv.org/abs/2204.04521), a transformer-based pretrained language model (PLM), to identify tasks related to public health surveillance (PHS) on social media. Compared with existing PLMs that are mainly evaluated on limited tasks, PHS-BERT achieved state-of-the-art performance on 25 tested datasets, showing that our PLM is robust and generalizable in common PHS tasks.

## Usage
We provide one version of pretrained weights. The currently available version of pretrained weights is as follows:
* [PHS-BERT](https://drive.google.com/file/d/1RIzqFHPwx_Ro152dkHiKU9omKaZzrhFF/view?usp=sharing) - based on BERT-base model

Alternatively, load the model via [Huggingface's Transformers library](https://github.com/huggingface/transformers]):
```
from transformers import AutoTokenizer, AutoModel
tokenizer = AutoTokenizer.from_pretrained("publichealthsurveillance/PHS-BERT")
model = AutoModel.from_pretrained("publichealthsurveillance/PHS-BERT")
```

## Training Procedure
### Pretraining
We followed the standard pretraining protocols of BERT and initialized PHS-BERT with weights from BERT during the training phase instead of training from scratch and used the uncased version of the BERT model. 
<br/>
<br/>
PHS-BERT is trained on a corpus of health-related tweets that were crawled via the Twitter API. Focusing on the tasks related to PHS, keywords used to collect pretraining corpus are set to disease, symptom, vaccine, and mental health-related words in English. Retweet tags were deleted from the raw corpus, and URLs and usernames were replaced with HTTP-URL and @USER, respectively. All emoticons were replaced with their associated meanings. 
<br/>
<br/>
Each sequence of BERT LM inputs is converted to 50,265 vocabulary tokens. Twitter posts are restricted to 200 characters, and during the training and evaluation phase, we used a batch size of 8. Distributed training was performed on a TPU v3-8.

### Fine-tuning
We used the embedding of the special token [CLS] of the last hidden layer as the final feature of the input text. We adopted the multilayer perceptron (MLP) with the hyperbolic tangent activation function and used Adam optimizer. The models are trained with a one cycle policy at a maximum learning rate of 2e-05 with momentum cycled between 0.85 and 0.95.

## Datasets
### Suicide
- [R-SSD](https://drive.google.com/file/d/1efbfuKJop7oQ_P8Rck8wNy17256JZlPm/view?usp=sharing)
### Stress
- [Dreaddit](https://drive.google.com/file/d/13ap2w3RRhyGNU5ky9mZDSPeDs3OFpI8P/view?usp=sharing)
- [SAD](https://drive.google.com/file/d/1zfB24UtFjYx-H9Q7-gU39o6hqZnPSf5x/view?usp=sharing)
### Health Mention
- [PHM](https://drive.google.com/file/d/1-FPyWDU9J3gsT2eXS5Iw9TDGkGsqv8Yk/view?usp=sharing)
- [HMC2019](https://drive.google.com/file/d/1pjlz-EviuAIlDoyZbxR5fiU2mpE9Qypo/view?usp=sharing)
- [RHMD](https://drive.google.com/file/d/1buPTwEzrvT1YXLx9RC9nsT-BzcoUEsbK/view?usp=sharing)
### Vaccine Sentiment
- [VS1](https://drive.google.com/file/d/1s06UlqirJKZ8wkmYXgBG7_od4kO1MdGX/view?usp=sharing)
- [VS2](https://drive.google.com/file/d/17qIoxaLqq15q2oAOcJQMa_yiAPqsnbFU/view?usp=sharing)
### COVID Related
- [Covid Lies](https://drive.google.com/file/d/1_sd40-6JkYv-evoJtz9ytBRlIlFBykDw/view?usp=sharing)
- [Covid Category](https://drive.google.com/file/d/1JV_vpopcgShEwvH7xTgWTQlA3dws7P2k/view?usp=sharing)
- [COVIDSentiA](https://drive.google.com/file/d/1M0X7_I2BavsOKE0VYBCcKwvZ2IljuOn8/view?usp=sharing)
- [COVIDSentiB](https://drive.google.com/file/d/1fHT7nHzmMjLfxWk22mNpNbJLKXWq4Vt6/view?usp=sharing)
- [COVIDSentiC](https://drive.google.com/file/d/1x0rKbNwuOISKOUqum2VkabyaodTh1XO8/view?usp=sharing)
### Depression
- [eRISK T3](https://drive.google.com/file/d/16lJ0h1PDnzGox90SymV7VdwOeFPCjItY/view?usp=sharing)
- [Depression_Reddit_1](https://drive.google.com/file/d/1jpvemeq-Uw3s-hnP-HF_gf7Mgt-_8GWh/view?usp=sharing)
- [eRisk19 T1](https://drive.google.com/drive/folders/1s6XRNs95d7IgpjJxGSKdRE2TrLOa1B08?usp=sharing)
- [Depression_Reddit_2](https://drive.google.com/file/d/1qdzT0ijowPbaXOPWb_cpx2xfqD79bsT1/view?usp=sharing)
- [Depression_Twitter_1](https://drive.google.com/file/d/19cLiTSMNcirttzwAgOChcIcY0c746FI2/view?usp=sharing)
- [Depression_Twitter_2](https://drive.google.com/file/d/1BQSccZ9Y2KtrvKYMrY2i8O--4ECLfMQM/view?usp=sharing)
### Other Health Related
- [PubHealth](https://drive.google.com/drive/folders/1zR_Zi56i1qiQBTh-w1rryB-IZWpdjWc8?usp=sharing)
- [Abortion](https://drive.google.com/drive/folders/1cmSpmsmkAna-AK6sEb6724ZV3i68zGXM?usp=sharing)
- [Amazon Health](https://drive.google.com/file/d/1RL-oyuN2FeDYjbskZgmcaHWKb3a60WhN/view?usp=sharing)
- [SMM4H T1](https://drive.google.com/file/d/1MNoCBArz_dYpRQBARs1NXdu7tlpjbg8r/view?usp=sharing)
- [SMM4H T2](https://drive.google.com/file/d/1dGceZB7mxbHc0fxw-DTnPq3TpDvSqffH/view?usp=sharing)
- [HRT](https://drive.google.com/file/d/16v7UFYzPNb0W3de8JGRmw0OnuDovrQcX/view?usp=sharing)

## Societal Impact
We train and release a PLM to accelerate the automatic identification of tasks related to PHS on social media. Our work aims to develop a new computational method for screening users in need of early intervention and is not intended to use in clinical settings or as a diagnostic tool.

## BibTex entry and citation info
For more details, refer to the paper [Benchmarking for Public Health Surveillance tasks on Social Media with a Domain-Specific Pretrained Language Model](https://arxiv.org/abs/2204.04521).

```
@misc{https://doi.org/10.48550/arxiv.2204.04521,
  doi = {10.48550/ARXIV.2204.04521},
  url = {https://arxiv.org/abs/2204.04521},
  author = {Naseem, Usman and Lee, Byoung Chan and Khushi, Matloob and Kim, Jinman and Dunn, Adam G.},
  keywords = {Computation and Language (cs.CL), FOS: Computer and information sciences, FOS: Computer and information sciences},
  title = {Benchmarking for Public Health Surveillance tasks on Social Media with a Domain-Specific Pretrained Language Model},
  publisher = {arXiv},
  year = {2022},
  copyright = {Creative Commons Attribution 4.0 International}
}
```

## Contact Information
If you have any questions, please submit a GitHub issue or contact Usman Naseem (usman.naseem@sydney.edu.au).
