# Electra pretrain with AIHub
## 개요
AI hub가 새롭게 공개한 대규모 웹데이터 기반 한국어 말뭉치 데이터를 Electra를 통해 학습시키는 것 <br>
[ai hub 데이터 주소](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=624) <br>
모델은 koELECTRA([github link](https://github.com/monologg/KoELECTRA))를 참조하였으며, vocab 파일도 여기서 가져왔습니다. <br> <br>

## 데이터 전처리
데이터 전처리는 2단계로 나누어서 진행하였습니다. <br>
1단계는 시간이 오래 걸리기 때문에, colab 환경이 아닌 local환경에서 진행하였습니다. <br>
이번에 AI hub에서 공개한 데이터에는 문장뿐만 아니라 그 문장의 주제와 카테고리 등 많은 정보가 있지만, <br>
pretrain을 하기 위해서는 필요하지 않은 정보이기 때문에 이 항목들을 제거하고 문장을 분류하는 작업을 시행했습니다. <br>
2단계를 진행하기 전에, 1단계에서 전처리한 데이터들을 colab 환경으로 빠르게 불러오기 위해 데이터들을 kaggle에 업로드하였습니다.(비공개 데이터) <br>
2단계 데이터 전처리는 NSP(next sentence prediction)을 위한 전처리 과정입니다. <br> <br>

## 학습 모델
학습에 사용한 모델은 ELECTRA([논문 링크](https://arxiv.org/abs/2003.10555))입니다. <br>
모델 코드는 기존의 ELECTRA 코드가 아닌 직접 구현한 코드입니다. <br>
기존의 ELECTRA 코드에서 샘플링 과정이 softmax 값중 가장 큰 값으로만 교체가 되는 반면, <br>
직접 구현한 코드는 softmax 값에서 샘플링하도록 하여, 다른 토큰들로도 교체가 가능하도록 하였습니다.<br> <br>

## 사전 학습
기존의 ELECTRA 모델의 생성자의 경우, BERT에서 활용하는 NSP 학습을 포함하여 학습을 진행하도록 하였습니다. <br>
모델 파라미터는 koELECTRA의 base와 small++의 파라미터와 동일합니다. <br>
학습의 효율을 위해 몇가지 방법을 사용하였습니다. <br>
colab 환경에서 큰 배치 사이즈로 base와 small++를 학습시키기 위해 TPU와 혼합 정밀도(float32, bfloat16)를 사용하였습니다. <br>
생성자의 임베딩은 판별자의 임베딩과 공유하도록 하였습니다. <br>
ram 절약을 위해 배치 사이즈 만큼만 데이터를 가져와서 학습에 사용하도록 하였습니다. <br> <br>

## 할것
- 새로운 데이터 전처리 방식으로 학습하기 (더 효율적으로 데이터 만들기) <br>
- 학습한 ELECTRA small++, base 모델 배포 (huggingface 활용) <br>
