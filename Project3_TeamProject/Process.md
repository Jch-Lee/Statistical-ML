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
기본적으로 5-fold cv 진행 후, 평균 accuracy를 기록
#### 실험1
* 파일명: MobileNet+EfficientNet
* 데이터: 기본 4000장
* 모델: MobileNet-v2
* 전처리: Resize(224*224)
* 배치 크기: 32
* 에포크: 35
* 옵티마이저: Adam
* 기본 학습률: 0.001
* 학습 스케쥴러: 
* 기타: 
* 정확도: 61.96%

#### 실험2
* 파일명: MobileNet+EfficientNet
* 데이터: 기본 4000장
* 모델: EfficientNet-b0
* 전처리: Resize(224*224)
* 배치 크기: 32
* 에포크: 35
* 옵티마이저: Adam
* 기본 학습률: 0.001
* 학습 스케쥴러: 
* 기타: 
* 정확도: 66.08%

#### 실험3
* 파일명: Mob+Eff_bigdata
* 데이터: 기본 4000장 + CIFAR-10 50000장
* 모델: MobileNet-v2
* 전처리: Resize(224*224)
* 배치 크기: 32 
* 에포크: 25
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 85.13%

#### 실험4
* 파일명: 
* 데이터: 기본 + CIFAR-10
* 모델: EfficientNet-b0
* 전처리: Resize(224*224) + Normalize(0, 0.5)
* 배치 크기: 16
* 에포크: 12
* 옵티마이저: Adam
* 학습 스케쥴러: CosineAnnealingLR
* 기타: 
* 정확도: 87.73%

#### 실험5
* 파일명: Mob+Eff_bigdata_aug
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug1 10000장 + CIFAR_aug2 10000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug1: Basic + RandomCrop 0.8~1.0 + RandomFlip(p=0.5)
    * Aug2: Basic + RandomRotation -45~45 + RandomFlip(p=0.7) + ColorJitter(brightness=0.3, contrast=0.3)
    * 전체 데이터에 한번 더 0.1 확률로 CutMix(alpha=1.0, beta=1.0) 적용
* 배치 크기: 32
* 에포크: 25
* 옵티마이저: Adam
* 학습 스케쥴러: OneCycleLR
* 기타: 
* 정확도: 93.33%