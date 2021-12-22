# Punctuation Restoration using Transformer Models

This repository is forked from [*xashru/punctuation-restoration*](https://github.com/xashru/punctuation-restoration) and modified for Korean pretrained models and datasets.
Great Thanks to xashru!
This repository contins official implementation of the paper [*Punctuation Restoration using Transformer Models for High-and Low-Resource Languages*](https://aclanthology.org/2020.wnut-1.18/) accepted at the EMNLP workshop [W-NUT 2020](http://noisy-text.github.io/2020/).


## Data

#### Korean
Korean datasets are provided in `data/aihub` directory. These are collected from links below.
- AI Hub 감성 대화 말뭉치 : https://aihub.or.kr/aidata/7978
- AI Hub Ksponspeech : https://aihub.or.kr/aidata/105



## Model Architecture
We fine-tune a Transformer architecture based language model (e.g., BERT) for the punctuation restoration task.
Transformer encoder is followed by a bidirectional LSTM and linear layer that predicts target punctuation token at
each sequence position.
![](./assets/model_architectue.png)


## Dependencies
Install PyTorch following instructions from [PyTorch website](https://pytorch.org/get-started/locally/). Remaining
dependencies can be installed with the following command
```bash
pip install -r requirements.txt
```


## Training
To train punctuation restoration model with optimal parameter settings for English run the following command
```
python src/train.py --cuda=True --pretrained_model=klue/roberta-small --freeze_bert=False --lstm_dim=-1
 --seed=1 --lr=5e-6 --epoch=10 --use_crf=False --augment_type=all  --augment_rate=0.15 
--alpha_sub=0.4 --alpha_del=0.4 --data_path=data/aihub --save_path=output
```


#### Supported Huggingface models
```
bert-base-multilingual-cased
bert-base-multilingual-uncased
xlm-mlm-en-2048
xlm-mlm-100-1280
distilbert-base-multilingual-cased
xlm-roberta-base
xlm-roberta-large
klue/roberta-base
klue/roberta-small
```



## Pretrained Models
You can find pretrained mdoels for Huggingface



## Inference
You can run inference on unprocessed text file to produce punctuated text using `inference` module. Note that if the 
text already contains punctuation they are removed before inference. 

Example script for English:
```bash
python inference.py --pretrained-model=klue/roberta-small --weight_path=weights.pt  
--in_file=data/example_input.txt --out_file=data/example_output.txt
```
This should create the text file with following output:
```text
요즘 젊은 직원들 대하기가 여간 조심스러운게 아니야. 왜 조심스러우신 마음이신걸까요? 요즘은 조금만 조언해도 꼰대라는 소리 듣기 십상이거든. 그럼 앞으로 어떻게 하실 계획이세요? 어차피 다 실수하면서 배우는거니까 알아서들 하리라 믿어줘야지. 멋진 상사이신거 같아요. 요즘 이 책을 읽는데 너무 괜찮은 책 인 것 같아. 마음이 평온해져. 마음에 드는 책을 찾으셔서 기쁘시겠어요. 공부 때문에 힘든 때에 읽으면 마음이 편해지는 책이라서 친구들에게도 읽어보게 하고 싶어. 친구들에게 책을 추천하려면 어떤 방법으로 하는 게 좋을까요? 인터넷에 글을 써서 올려보는 게 좋을 것 같아. 친구들과 공유하고 싶어. 좋은 책을 공유하여 많은 친구들이 읽어볼 수 있으면 좋겠어요. 치료를 계속 받아야 하는 친구가 있는데 병원비 때문에 퇴원한다는 거 내가 돈을 빌려줬어. 친구에게 도움을 줄 수 있으셔서 좋으셨겠어요. 치료를 계속 받아야 하는데 중단하면 못 쓰지. 이런 상황에서 가장 좋은 방법으로는 무엇이 있을까요? 친구에게 돈 갚으라고 압박을 주면 안 되겠지? 두 분의 깊은 우정을 응원할게요. 남편이 공들여 요리를 해주는 날은 사랑받는 기분이 들어. 그게 바로 오늘이고. 오늘 남편 분이 사랑을 담아 요리를 해주셨군요. 정말 행복하시겠어요. 응. 우리 남편은 요리도 참 잘해. 남편 분이 요리를 잘하시는군요. 어떤 요리였나요? 김치볶음밥 밥 모양을 하트 모양으로 예쁘게 만들어주기도 했어. 사랑이 담긴 김치볶음밥이네요. 영원한 사랑을 기원할게요. 어제까지 나와 제일 친했던 친구가 오늘은 인사도 안해. 무슨일이 있었나요? 아니 갑자기 그래서 너무 당황스러워. 이유를 모르는 건가요? 응. 난 모르겠어. 그 친구뿐만 아니라 다른 친구들도 날 피하는 것 같아. 저런. 너무 속상하시겠어요. 나이가 드니 치매가 걸릴까 봐 두려워. 나이에 따른 변화가 두려우신가 봐요. 모든 기억이 사라지고 자식도 남편도 못알아보드라고. 가까운 사람과의 기억이 소실될까 봐 무척 두려우신 것 같아요. 남자친구가 자꾸 자기 멋대로 해. 무엇을 그렇게 하였나요? 놀러 가기로 했는데 장소를 자기가 가고 싶은 곳으로 정하잖아. 남자친구에게 앞으로 어떻게 할 계획이세요? 전학 온 학교에서 새로운 친구가 생겼어. 다행이야. 기분이 좋아보이세요. 따돌림을 당한 경험이 있어서 걱정했었거든. 앞으로도 좋은 일이 많이 생기시길 바랄게요. 남편이 죽는다는 생각만 해도 눈물나. 남편 분이 어디가 안 좋으신가요? 
```

Please note that *Comma* includes commas, colons and dashes, *Period* includes full stops, exclamation marks 
and semicolons and *Question* is just question marks. 


## Test
Trained models can be tested on processed data using `test` module to prepare result.

For example, to test the best preforming English model run following command
```bash
python src/test.py --pretrained_model=roberta-large --lstm_dim=-1 --use_crf=False --data_path=data/test
--weight_path=weights.pt --sequence_length=256 --save_path=output
```
Please provide corresponding arguments for `pretrained_model`, `lstm_dim`, `use_crf` that were used during training the
model. This will run test for all data available in `data_path` directory.


## Cite this work

```
@inproceedings{alam-etal-2020-punctuation,
    title = "Punctuation Restoration using Transformer Models for High-and Low-Resource Languages",
    author = "Alam, Tanvirul  and
      Khan, Akib  and
      Alam, Firoj",
    booktitle = "Proceedings of the Sixth Workshop on Noisy User-generated Text (W-NUT 2020)",
    month = nov,
    year = "2020",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/2020.wnut-1.18",
    pages = "132--142",
}
```
