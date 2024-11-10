## 0. 베이스 모델 설정
데이터 수가 적으므로 경량화된 모델 사용
#### 모델 후보
* MobileNet
* EfficientNet
#### 학습 환경
* Epoch: 30~50
* Batch Size: 32
* 

## 1. 데이터 수만 늘려(CIFAR-10 활용) 학습

## 2. 다양한 trick 이용
* Data augmentation
    * flipping
    * gray scale
    * brightness
    * rotation
    * center crop
    * blurring
    * mixup
    * cutout
    * cutmix

* Dropout
* Normalization


## 실험 목록
#### 실험1
* 파일명: 
* 데이터: 기본
* 모델: MobileNet-v2
* 전처리: 
* 배치 크기: 
* 에포크: 
* 옵티마이저: 
* 학습 스케쥴러: 
* 기타: 

#### 실험2
* 파일명: 
* 데이터: 기본
* 모델: EfficientNet-b0
* 전처리: 
* 배치 크기: 
* 에포크: 
* 옵티마이저: 
* 학습 스케쥴러: 
* 기타: 

#### 실험3
* 파일명: 
* 데이터: 기본 + CIFAR-10
* 모델: MobileNet-v2
* 전처리: 
* 배치 크기: 
* 에포크: 
* 옵티마이저: 
* 학습 스케쥴러: 
* 기타: 

#### 실험4
* 파일명: 
* 데이터: 기본 + CIFAR-10
* 모델: EfficientNet-b0
* 전처리: 
* 배치 크기: 
* 에포크: 
* 옵티마이저: 
* 학습 스케쥴러: 
* 기타: 

#### 실험5
* 파일명: 
* 데이터: 
* 모델: 
* 전처리: 
* 배치 크기: 
* 에포크: 
* 옵티마이저: 
* 학습 스케쥴러: 
* 기타: 