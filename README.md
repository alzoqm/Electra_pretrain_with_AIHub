# Electra pretrain with AIHub
## 개요
AI hub가 새롭게 공개한 대규모 웹데이터 기반 한국어 말뭉치 데이터를 Electra를 통해 학습시키는 것 <br>
데이터 주소: https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=624 <br>
모델은 koELECTRA(github link:https://github.com/monologg/KoELECTRA)를 참조하였으며, vocab 파일도 여기서 가져왔습니다. <br>
## 데이터 전처리
데이터 전처리는 2단계로 나누어서 진행하였습니다. <br>
1단계는 시간이 오래 걸리기 때문에, colab 환경이 아닌 local환경에서 진행하였습니다. <br>
이번에 AI hub에서 공개한 데이터에는 문장뿐만 아니라 그 문장의 주제와 카테고리 등 많은 정보가 있지만, <br>
pretrain을 하기 위해서는 필요하지 않은 정보이기 때문에 이 항목들을 제거하고 문장을 분류하는 작업을 시행했습니다. <br>
2단계를 진행하기 전에, 1단계에서 전처리한 데이터들을 colab 환경으로 빠르게 불러오기 위해 데이터들을 kaggle에 업로드하였습니다.(비공개 데이터) <br>
