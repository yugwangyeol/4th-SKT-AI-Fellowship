# SKT AI Fellowship 4기 프로젝트 

<br/>

## 1. 배경 & 목적

- 얼굴, 이름, 주소 등 이미지 내의 개인정보 탐지 기술 개발
- Security Journal 논문지에 2023년 발간 예정

<br/>


## 2. 주최/주관 & 팀원

- 주최/주관: SKT AI Fellowship 4기
- 팀원: 전공생 총 3명

<br/>


## 3. 프로젝트 기간

- 2022.06. ~ 2022.11. (6개월)

<br/>


## 4. 프로젝트 소개

<img src='https://user-images.githubusercontent.com/75362328/212486986-da53186e-eec0-417f-8c4c-3a3864a74a5a.png' width='100%' height='80%'>

&nbsp;&nbsp;&nbsp;&nbsp; 본 연구 주제는 클라우드 상에 저장되어 있는 다양한 이미지 데이터로부터 개인정보를 탐지, PII Detection을 하는 것이다. 개인 정보라고 하는 것은 다양한 범주가 있는데 그중에서 비정형 이미지 데이터 중 패턴이 없어 딥러닝으로 탐지해야 하는 **얼굴, 이름, 주소를 탐지해 주는 서비스**를 제작하였다. 전체적인 Prototype은 크게 2가지로 나누어서 구성되어 있다. **Face Detection Flow**는 얼굴을 탐지하는 Task로 Face Detection과 Classification으로 이루어져 있고, **OCR/NER Flow**는 이름, 주소를 탐지해 주는 Task로 OCR과 NER로 이루어져 있다.

&nbsp;&nbsp;&nbsp;&nbsp; 우선 얼굴을 제대로 탐지해 주기 위해서 마네킹, 그림, 고글 등의 얼굴은 개인 정보로 탐지하지 않게끔 수작업으로 얼굴 이미지와 얼굴이 아닌 이미지를 각각 5만 장씩 데이터 셋을 구성하였다. 우선 얼굴 정보가 포함되어 있는지 없는지 판단하기 위해 Face Classification 모델들 중 가장 성능이 좋았던 **adv_inception_v3** 모델을 선정하였으나 상대적으로 낮은 탐지 성능을 보였다. 따라서 **DLIB, RetinaFace, MTCNN, DSFD** 등을 활용한 Face Detection 모델들을 실험한 결과 Inference Time과 F1 Score가 모두 좋았던 **MTCNN 모델을 선정**하였다. 

&nbsp;&nbsp;&nbsp;&nbsp; 이름과 주소 탐지를 위해서는 우선 글자를 탐지해 주는 OCR 단계를 거쳐야 한다. AI Hub의 ‘야외 실제 촬영 한글 이미지 데이터’와 ‘공공행정문서 데이터’를 조합해서 총 190만 장의 데이터 셋을 생성하였다. 글자가 있는 위치를 탐지해 주는 **Text Detection 단계에서는 MMOCR 라이브러리의 TextSnake 모델을 사용**하였는데, TextSnake는 긴 글 탐지 성능이 좋아 본 Task에 성능이 더 좋을 것이라 판단하였다. 또한 글자만 탐지된 이미지에서 텍스트를 추출해 내는 **Text Recognition 단계에서는 현재 Scene Text Recognition에서 SOTA인 PARSeq 모델을 사용**하였다.

&nbsp;&nbsp;&nbsp;&nbsp; 다음은 OCR을 통해 인식된 **텍스트 중 사람과 주소를 찾아내는 NER 파트**이다. ‘한국해양대학교 자연어 처리 연구실의 데이터 셋’을 활용해 fine-tuning을 진행하였다. **BERT, KRBERT, KoBigBird, KoELECTRA** 등의 모델을 실험한 결과 **가장 성능이 좋았던 KoELECTRA 모델을 선정**하였다. 그 과정에서 ‘경기도 의정부시’처럼 자세하지 않은 주소가 탐지된 경우 장소로 라벨링 하지 않았으며 ‘경기도 의정부시 의정로’ 이상으로 구체적으로 나와 있을 경우에만 개인 정보로 탐지하게끔 과적합시켜 주었다.

&nbsp;&nbsp;&nbsp;&nbsp; 결론적으로 Object Detection에서는 MTCNN, OCR에서는 TextSnake, Parseq, NER에서는 KoELECTRA 모델을 사용하였으며 진행 과정을 **Streamlit**을 활용하여 이미지 데이터에 대한 진행 과정을 보여주었다.

<br/>


## 5. 프로젝트 담당 역할

- 새로운 개인정보 분류 기준 생성 및 데이터 셋 구축 & 전처리
- MTCNN 모델 학습 및 최적화 & Inference 코드 제작
    - DLIB, DSFD, RetinaFace, TinaFace, SCRFD 등의 Face Detection 모델 구현 및 성능 비교
- NER 모델 KoELECTRA vs. Spacy(Baseline) 구현 및 성능 비교
- Streamlit 웹 제작 및 3가지 모델(Face Detection, OCR, NER) 연동

<br/>


## 6. 발표 자료

[SKT 최종 발표자료](https://drive.google.com/file/d/1lQaaSlg872ZF78BYy3yBNUmYEakoH74F/view)  
[SKT 발표 영상](https://www.youtube.com/watch?v=RH2qumoWMY0)  

<br/>


## 7. 코드 공새
- 코드 공개는 보안 문제로 공개가 불가합니다.
