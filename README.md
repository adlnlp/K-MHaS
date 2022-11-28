# [K-MHaS: A Multi-label Hate Speech Detection Dataset in Korean Online News Comment](https://aclanthology.org/2022.coling-1.311/)

### <div align="center"> Jean Lee, Taejun Lim, Heejun Lee, Bogeun Jo, <br> Yangsok Kim, Heegeun Yoon and Soyeon Caren Han.</div>
### <div align="center"> Accepted by the 29th International Conference on Computational Linguistics <br> (COLING 2022).</div>

[<img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>](https://colab.research.google.com/drive/171KhS1_LVBtpAFd_kaT8lcrZmhcz5ehY?usp=sharing)

- **26 Nov 2022 : HuggingFace update** our dataset can be loaded through [huggingface](https://huggingface.co/datasets/jeanlee/kmhas_korean_hate_speech). 

**:movie_camera: Paper Presentation** 
: Please click on the image below.
[<img src="https://github.com/adlnlp/K-MHaS/blob/main/resource/1_K-MHaS.png" width="70%">](https://www.youtube.com/watch?v=r5i5emeEwsY)


## Korean Multi-label Hate Speech Dataset 
We introduce **K-MHaS**, a new multi-label dataset for **hate speech detection** that effectively handles **Korean** language patterns. 
- consisting of **109,692** utterances from **Korean online news comments**, labelled with 8 fine-grained hate speech classes. 
- providing **(a)binary** classification and **(b)multi-label** classification from 1(one) to 4(four) labels. 
- data collection period : between January 2018 and June 2020. 


## Multi-label Annotation 
Compared with previous studies, the multi-label annotation scheme allows non-exclusive concepts, accounting for the overlapping shades of given categories. 

Our annotation scheme has two layers: 
- **(a) binary** classification (`Hate Speech` or `Not Hate Speech`) and 
- **(b) fine-grained** classification. 
    - `Politics`(정치성향차별)
    - `Origin`(출신차별)
    - `Physical`(외모차별)
    - `Age`(연령차별)
    - `Gender`(성차별)
    - `Religion`(종교차별)
    - `Race`(인종차별)
    - `Profanity`(혐오욕설)

For the fine-grained classification, a `Hate Speech` class from the binary classification, is broken down into eight classes, associated with the hate speech category. In order to reflect the social and historical context, we select the eight hate speech classes. For example, the `politics` class is chosen, due to a significant influence on the style of Korean hate speech.

- Comparison of datasets
<img src="https://github.com/adlnlp/K-MHaS/blob/main/resource/5_literature.png" width="70%">

## Dataset Details
In this repository, we provide splitted datasets that have 78,977(train) / 8,776 (validation) / 21,939 (test) samples, preserving the class proportion. The label numbers matching in both English and Korean is below. 

label types  |  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8
----------|-----------|-----------|-----------|----------|----------|---------|---------|---------|-----------
`En` |  `Origin` | `Physical` | `Politics` | `Profanity` | `Age` | `Gender` | `Race` | `Religion` | `Not Hate Speech`
`Kr` |  `출신차별` | `외모차별` | `정치성향차별` | `혐오욕설` | `연령차별` | `성차별` | `인종차별` | `종교차별` | `해당사항없음`


```
document	label
좌좀 홍어들이 일베보다 더 극혐이다	0,2
와 이거 완전 재앙이네. 깨끗한 나라 만든다면서 왜 이런 사건이 터지냐??	2
몬생긴 여자인간들은 찌그러져있어라 확그냥 막그냥	1,5
오면 화염병 던진다 돼지새키야	1,3
수꼴틀딱시키들이 다 디져야 나라가 똑바로 될것같다..답이 없는 종자들ㅠ	2,3,4
ㅇㅇ? 양놈이건 깜씨건 뭔 아방가르드하네	0,6
OOO천지 개독교 새끼들아 다 착해져라!	3,7
다들 오지랖 좀...되게 할 짓 없어보여요	8
```


## Experiments
We evaluate strong baseline experiments on our dataset using Korean-BERT-based language models with six different metrics (F1-[macro, micro, weighted], Exact Match, AUC and Hamming Loss). 

- **[MultiBERT](https://huggingface.co/bert-base-multilingual-cased) (Wolf et al., 2020)** : pre-trained on the Wikipedia in 104 different languages (110M parameters and 119K vocab.). 
- **[KoELECTRA](https://github.com/monologg/KoELECTRA) (Park, 2020)** : pre-trained on 34GB Korean news, Wikipedia, Namu (Korean wiki) and Modu (14M parameters and 35K vocab.). 
- **[KoBERT](https://github.com/SKTBrain/KoBERT) (SKTBrain, 2019)** : pre-trained on 54M words from Korean Wikipedia (92M parameters and 8K vocab.). 
- **[KR-BERT](https://github.com/snunlp/KR-BERT) (Lee et al., 2020)** : pre-trained on 2.47GB corpus with 233M words from Korean Wikipedia and news, applying either
    - (1) the character-level tokenizer; or
    - (2) the sub-character-level tokenizer. 

---
**The overall performance for all labels**
- The micro F1-score range between 0.8139 (Multi-BERT) and 0.8500 (KR-BERT-c: using character-level tokenizer).
- KoELECTRA obtains overall the best or second best among six metrics. 
- This indicates the effects of the pre-training data source, considering that the KoELECTRA corpora contains modern slang and buzzwords.

<img src="https://github.com/adlnlp/K-MHaS/blob/main/resource/10_overallEval.png" width="70%">

---
**The breakdown performance for the multi-label classification**
- KR-BERT using sub-character-level tokenizer achieved the best, or second best performance.
- The sub-character tokeniser can decompose Hangul(Korean language) syllable characters into sub-characters. 
- It provides a great ability to detect a hate speech word, composed by each character in different hate speech labels.
<img src="https://github.com/adlnlp/K-MHaS/blob/main/resource/11_multiEval.png" width="70%">


## Contributors
The contributors of the work are: 
- [Jean Lee](https://jeanlee-ai.github.io/) (Ph.D. candidate at the University of Sydney)
- [Taejun Lim](https://github.com/taezun) (Mphil. candidate at the University of Sydney)
- [Heejun Lee](https://bigwaveai.com/) (BigWave AI)
- [Bogeun Jo](https://bigwaveai.com/) (BigWave AI)
- Yangsok Kim (Professor at Keimyung University)
- Heegeun Yoon (National Information Society Agency)
- [Soyeon Caren Han](https://drcarenhan.github.io/) (Senior lecturer at the University of Western Australia, Honorary senior lecturer at the University of Sydney)



## Citation
If you use the dataset, please cite this our paper [K-MHaS: A Multi-label Hate Speech Detection Dataset in Korean Online News Comment](https://aclanthology.org/2022.coling-1.311.pdf) accepted by [COLING2022](https://coling2022.org/). 
```
@inproceedings{lee-etal-2022-k,
    title = "K-{MH}a{S}: A Multi-label Hate Speech Detection Dataset in {K}orean Online News Comment",
    author = "Lee, Jean  and
      Lim, Taejun  and
      Lee, Heejun  and
      Jo, Bogeun  and
      Kim, Yangsok  and
      Yoon, Heegeun  and
      Han, Soyeon Caren",
    booktitle = "Proceedings of the 29th International Conference on Computational Linguistics",
    month = oct,
    year = "2022",
    address = "Gyeongju, Republic of Korea",
    publisher = "International Committee on Computational Linguistics",
    url = "https://aclanthology.org/2022.coling-1.311",
    pages = "3530--3538",
    abstract = "Online hate speech detection has become an important issue due to the growth of online content, but resources in languages other than English are extremely limited. We introduce K-MHaS, a new multi-label dataset for hate speech detection that effectively handles Korean language patterns. The dataset consists of 109k utterances from news comments and provides a multi-label classification using 1 to 4 labels, and handles subjectivity and intersectionality. We evaluate strong baselines on K-MHaS. KR-BERT with a sub-character tokenizer outperforms others, recognizing decomposed characters in each hate speech class.",
}
```

