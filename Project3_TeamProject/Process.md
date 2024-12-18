## 0. 베이스 모델 설정
데이터 수가 적으므로 경량화된 모델 사용
#### 모델 후보
* MobileNet
* EfficientNet

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
#### 실험1 (baseline)
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

#### 실험2 (baseline)
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

#### 실험3 (large dataset)
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

#### 실험4 (large dataset)
* 파일명: 
* 데이터: 기본 4000장 + CIFAR-10 50000장
* 모델: EfficientNet-b0
* 전처리: Resize(224*224) + Normalize(0, 0.5)
* 배치 크기: 16
* 에포크: 12
* 옵티마이저: Adam
* 학습 스케쥴러: CosineAnnealingLR
* 기타: 
* 정확도: 87.73%

#### 실험5 (large dataset + augment)
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

#### 실험6 (large dataset + augment)
* 파일명: nocutmix
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug 15000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug: Basic + RandomRotation(-45~45) + RandomFlip(p=0.5)
* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 89.80%

#### 실험7 (large dataset + augment)
* 파일명: nocutmix
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug 15000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug: Basic + RandomRotation(-45~45) + RandomFlip(p=0.5)
    * 전체 데이터에 한번 더 0.1 확률로 CutMix(alpha=1.0, beta=1.0) 적용
* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 90.50%

#### 실험8 (large dataset + augment)
* 파일명: Experiment1
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug 15000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug: Basic + RandomRotation(-45~45) + RandomFlip(p=0.7) + RandomResizedCrop(224, scale=(0.8, 1.0)) + ColorJitter(brightness=0.2, contrast=0.2, hue=0.2, saturation=0.2)
* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 88.76%

#### 실험9 (large dataset + augment)
* 파일명: Experiment2
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug1 10000장 + CIFAR_aug2 10000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug1: Basic + RandomHorizontalFlip(p=0.5) + RandomRotation(45) + RandomResizedCrop(224, scale=(0.8, 1.0))
    * Aug2: Basic + RandomRotation -45~45 + RandomFlip(p=0.7) + ColorJitter(brightness=0.2, contrast=0.2, hue=0.2, saturation=0.2)

* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 89.91%

#### 실험10 (large dataset + augment)
* 파일명: Experiment2
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug1 15000장 + CIFAR_aug2 15000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug1: Basic + RandomHorizontalFlip(p=0.7) + RandomRotation(45) + RandomResizedCrop(224, scale=(0.5, 1.0))
    * Aug2: Basic + RandomRotation -45~45 + RandomFlip(p=0.7) + ColorJitter(brightness=0.5, contrast=0.5, hue=0.5, saturation=0.5)

* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 90.72%
  
#### 실험11 (large dataset + augment)
* 파일명: Experiment4
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug1 10000장 + CIFAR_aug2 10000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug1: Basic + RandomResizedCrop(224, scale=(0.8, 1.0)) + RandomHorizontalFlip(p=0.5)
    * Aug2: Basic + RandomRotation(45) + RandomHorizontalFlip(p=0.5) + 
    transforms.ColorJitter(brightness=0.3, contrast=0.3)
* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 92.08%

#### 실험12 (large dataset + augment)
* 파일명: Experiment6
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug1 15000장 + CIFAR_aug2 15000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug1: Basic + RandomResizedCrop(224, scale=(0.8, 1.0)) + RandomHorizontalFlip(p=0.5)
    * Aug2: Basic + RandomRotation(45) + RandomHorizontalFlip(p=0.5) + 
    transforms.ColorJitter(brightness=0.3, contrast=0.3)
* 배치 크기: 32
* 에포크: 30
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 93.45%

#### 실험13 (large dataset + augment)
* 파일명: Experiment5
* 데이터: 기본 4000장 + CIFAR-10 50000장 + CIFAR_aug1 15000장 + CIFAR_aug2 15000장
* 모델: EfficientNet-b0
* 전처리:
    * Basic: Resize(224*224) + Normalize(mean=(0.4914, 0.4822, 0.4465), std=(0.247, 0.243, 0.261))
    * Aug1: Basic + RandomResizedCrop(224, scale=(0.8, 1.0)) + RandomHorizontalFlip(p=0.5)
    * Aug2: Basic + RandomRotation(45) + RandomHorizontalFlip(p=0.5) + ColorJitter(brightness=0.3, contrast=0.3)
* 배치 크기: 32
* 에포크: 60
* 옵티마이저: Adam
* 학습 스케쥴러: 
* 기타: 
* 정확도: 94.65%

## 발표 구성

### 1. 기본
1-1. EfficientNet: 66.08%
* Batch: 32
* Epoch: 30
* Data: base 4000
* Optimizer: Adam  
1-2. ResNet:  
1-3. SE: 

### 2. CIFAR 데이터 추가
2-1. EfficientNet: 87.73%
* Batch: 32
* Epoch: 30
* Data: base 4000 + CIFAR-10 50000
* Optimizer: Adam  
2-2. ResNet:  
2-3. SE: 

### 3. 데이터 증강
3-1. EfficientNet: 89.80%
* Batch: 32
* Epoch: 30
* Data: base 4000 + CIFAR-10 50000 + CIFAR aug 15000
   * aug: RandomRotation(45) + RandomHorizontalFlip(0.5)
* Optimizer: Adam  
3-2. ResNet:  
3-3. SE: 

### 4. 증강 데이터 약간 늘림 + 다른 증강 데이터를 혼합
4-1. EfficientNet: 92.08%
* Batch: 32
* Epoch: 30
* Data: base 4000 + CIFAR-10 50000 + CIFAR aug1 10000 + CIFAR aug2 10000
   * aug1: RandomResizedCrop(0.8~1.0) + RandomHorizontalFlip(0.5)
   * aug2: RandomRotation(45) + RandomHorizontalFlip(p=0.5) + ColorJitter(brightness=0.3, contrast=0.3)
* Optimizer: Adam  
4-2. ResNet:  
4-3. SE:  

### 5. 증강 데이터 더 늘림 + 다른 증강 데이터를 혼합 + epoch 증가(because 학습 난이도 증가)
4-1. EfficientNet: 94.65%
* Batch: 32
* Epoch: 60
* Data: base 4000 + CIFAR-10 50000 + CIFAR aug1 15000 + CIFAR aug2 15000
   * aug1: RandomResizedCrop(0.8~1.0) + RandomHorizontalFlip(0.5)
   * aug2: RandomRotation(45) + RandomHorizontalFlip(p=0.5) + ColorJitter(brightness=0.3, contrast=0.3)
* Optimizer: Adam  
4-2. ResNet:  
4-3. SE:  
