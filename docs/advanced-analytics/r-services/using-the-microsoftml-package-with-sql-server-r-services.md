---
title: "SQL Server R Services에서 MicrosoftML 패키지 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# SQL Server R Services에서 MicrosoftML 패키지 사용
Microsoft R Server 및 SQL Server vNext CTP 1.0과 함께 제공되는 **MicrosoftML** 패키지에는 Microsoft에서 개발한 여러 가지 기계 학습 알고리즘이 포함되어 있으며, 이 알고리즘은 멀티 코어 처리 및 빠른 데이터 스트리밍을 지원합니다. 이 패키지에는 텍스트 처리 및 기능에 대한 변환도 포함되어 있습니다.

### <a name="new-machine-learning-algorithms"></a>새로운 기계 학습 알고리즘


-  **빠른 선형.** 이진 분류 또는 회귀에 사용할 수 있는 확률적 이중 좌표 경사를 기반으로 하는 선형 학습자입니다. 이 모델은 L1 및 L2 정규화를 지원합니다.

- **신속한 트리.** 원래 FastRank로 알려진 향상된 의상 결정 트리 알고리즘으로, Bing에서 사용하기 위해 개발되었습니다. 가장 빠르고 가장 인기 있는 학습자 중 하나입니다. 이진 분류 및 회귀를 지원합니다.

- **빠른 포리스트.** 임의 포리스트 방법을 기반으로 하는 로지스틱 회귀 분석 모델입니다. 이 모델은 RevoScaleR의 `rxLogit` 함수와 유사하지만 L1 및 L2 정규화를 지원합니다. 이진 분류 및 회귀를 지원합니다.

- **로지스틱 회귀 분석.** RevoScaleR의 `rxLogit` 함수와 유사한 로지스틱 회귀 분석 모델로, L1 및 L2 정규화를 추가로 지원합니다. 이진 또는 다중 클래스 분류를 지원합니다.

- **신경망.** 이진 분류, 다중 클래스 분류 및 회귀에 대한 신경망 모델입니다. GPU 가속 및 사용자 지정할 수 있는 복잡한 네트워크를 지원합니다.

- **1클래스 SVM.** 불균형 데이터 집합에서 이진 분류에 사용할 수 있는 SVM 방법을 기반으로 하는 변칙 검색 모델입니다.

## <a name="transformation-functions"></a>변환 함수

**MicrosoftML** 패키지에는 데이터 변환 및 기능 추출에 사용할 수 있는 다음과 같은 함수도 포함되어 있습니다.

- `featurizeText()`
 
  지정된 텍스트 문자열로 ngrams 개수를 생성합니다. 

  이 함수에는 사용된 언어 검색, 텍스트 토큰화 및 정규화 수행, 중지 단어 제거 및 텍스트에서 기능 생성 옵션이 포함되어 있습니다. 

- `categorical()`

  범주에 대한 사전을 작성하고 각 범주를 표시기 벡터로 변환합니다. 
 
- `categoricalHash()`

  값을 해시하고 해시를 모음의 인덱스로 사용하여 범주 값을 표시기 배열로 변환합니다.  

- `selectFeatures()` 

  기본값이 아닌 값을 계산하거나 레이블을 기준으로 상호 정보 점수를 계산하여 지정된 변수에서 기능의 하위 집합을 선택합니다. 

이러한 새로운 기능에 대한 자세한 내용은 [MicrosoftML 함수](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)를 참조하세요.

## <a name="support-for-microsoftml-in-r-services"></a>R Services에서 MicrosoftML 지원

**MicrosoftML** 패키지는 **RevoScaleR** 패키지에서 사용하는 데이터 처리 파이프라인과 완전히 통합됩니다. 현재 SQL Server R Services를 포함한 모든 Windows 기반 컴퓨터 컨텍스트에서 **MicrosoftML** 패키지를 사용할 수 있습니다.



## <a name="see-also"></a>관련 항목:


[RevoScaleR 함수 참조](https://msdn.microsoft.com/microsoft-r/scaler/scaler)

