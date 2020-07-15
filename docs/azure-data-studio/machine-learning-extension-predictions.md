---
title: Machine Learning 확장을 사용하여 예측 수행
titleSuffix: Azure Data Studio
description: Azure Data Studio용 Machine Learning 확장을 사용하여 데이터베이스에서 ONNX 모델로 예측을 수행하는 방법을 알아봅니다.
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: d4f057722896d577f9754960390a9a46f8711b7e
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352390"
---
# <a name="make-predictions-with-machine-learning-extension-preview-for-azure-data-studio"></a>Azure Data Studio용 Machine Learning 확장(미리 보기)을 사용하여 예측 수행

[Azure Data Studio용 Machine Learning 확장](machine-learning-extension.md)을 사용하여 데이터베이스에서 ONNX 모델로 예측을 수행하는 방법을 알아봅니다. 이 확장은 [PREDICT](../t-sql/queries/predict-transact-sql.md)를 사용하여 이전에 가져온 모델, 로컬 파일에 있는 모델 또는 Azure Machine Learning의 모델을 통해 테이블에 저장된 데이터 세트에 대한 예측을 수행하는 T-SQL 스크립트를 생성합니다.

> [!IMPORTANT]
> Machine Learning 확장을 사용한 예측 수행은 현재 [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 및 [ONNX를 사용하는 Azure SQL Edge](/azure/azure-sql-edge/onnx-overview)에서만 지원됩니다.

## <a name="prerequisites"></a>필수 구성 요소

- [Azure Data Studio용 Machine Learning 확장](machine-learning-extension.md)을 설치하고 구성합니다. [확장 설정에서 Python 설치 경로](machine-learning-extension.md#settings)를 지정해야 합니다.

- **onnxruntime**, **mlflow** 및 **mlflow-dbstore** Python 패키지. 이러한 패키지가 아직 설치되지 않았다면 Machine Learning 확장에서 패키지를 설치하라는 메시지가 표시됩니다.

## <a name="make-predictions-from-onnx-model"></a>ONNX 모델에서 예측 수행

ONNX 모델을 사용하여 예측을 수행하려면 다음 단계를 따르세요.

1. **예측 수행**을 클릭합니다.

1. **onnxruntime**, **mlflow** 및 **mlflow-dbstore**를 설치하라는 메시지가 표시되면 **예**를 클릭합니다.

1. 모델이 있는 위치를 선택하고 **다음**을 클릭합니다. 다음을 사용할 수 있습니다.
    - **가져온 모델**. 데이터베이스에 이미 저장된 모델을 사용하려면 이 옵션을 선택합니다. 모델이 있는 **model 데이터베이스** 및 **모델 테이블**에서 사용할 모델을 선택하고 **다음**을 클릭합니다.
    - **파일 업로드**. 파일의 모델을 사용하려면 이 옵션을 선택합니다. **원본 파일**에서 모델 파일을 선택하고 **다음**을 클릭합니다.
    - **Azure Machine Learning**. Azure Machine Learning의 모델을 사용하려면 이 옵션을 선택합니다. 먼저 **Azure에 로그인**합니다. 그런 다음 **Azure 계정**, **Azure 구독**, **Azure 리소스 그룹** 및 **Azure ML 작업 영역**을 선택합니다. 사용하려는 모델을 선택하고 **다음**을 클릭합니다.

1. 원본 데이터를 모델에 매핑합니다.
    - 예측을 적용하려는 데이터 세트가 포함된 **원본 데이터베이스** 및 **원본 테이블**을 선택합니다.
    - **모델 입력 매핑** 및 **모델 출력** 아래의 열을 매핑합니다. 확장은 이름 및 데이터 형식이 같은 열을 자동으로 매핑합니다.

1. **Predict**를 클릭합니다.

Azure Data Studio가 [PREDICT](../t-sql/queries/predict-transact-sql.md)를 사용하여 새 T-SQL 쿼리를 만듭니다. 이 쿼리를 사용하여 데이터에 대한 예측을 수행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio의 Machine Learning 확장](machine-learning-extension.md)
- [데이터베이스에서 패키지 관리](machine-learning-extension-manage-packages.md)
- [모델 가져오기 또는 보기](machine-learning-extension-import-view-models.md)
- [Azure Data Studio의 Notebook](notebooks-guidance.md)
- [SQL Machine Learning 설명서](../machine-learning/index.yml)
- [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [SQL Edge(미리 보기)에서 Open Neural Network Exchange를 통한 기계 학습 및 AI](/azure/azure-sql-edge/onnx-overview)
