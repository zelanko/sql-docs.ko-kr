---
title: Machine Learning 확장을 사용하여 모델 가져오기 또는 보기
titleSuffix: Azure Data Studio
description: Azure Data Studio용 Machine Learning 확장을 사용하여 ONNX 모델을 가져오거나 데이터베이스에서 이미 가져온 모델을 보는 방법을 알아봅니다.
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3c5faa821ecd9adcfcea426f88a388a6f7d10f27
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901051"
---
# <a name="import-or-view-models-with-machine-learning-extension-preview-for-azure-data-studio"></a>Azure Data Studio용 Machine Learning 확장(미리 보기)을 사용하여 모델 가져오기 또는 보기

[Azure Data Studio용 Machine Learning 확장](machine-learning-extension.md)을 사용하여 ONNX 모델을 가져오거나 데이터베이스에서 이미 가져온 모델을 보는 방법을 알아봅니다.

> [!IMPORTANT]
> Machine Learning 확장을 사용한 가져오기 및 데이터베이스에서 보기는 현재 [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 및 [ONNX를 사용하는 Azure SQL Edge](/azure/azure-sql-edge/onnx-overview)에서만 지원됩니다.

## <a name="prerequisites"></a>필수 구성 요소

- [Azure Data Studio용 Machine Learning 확장](machine-learning-extension.md)을 설치하고 구성합니다. [확장 설정에서 Python 설치 경로](machine-learning-extension.md#settings)를 지정해야 합니다.

- **onnxruntime**, **mlflow** 및 **mlflow-dbstore** Python 패키지. 이러한 패키지가 아직 설치되지 않았다면 Machine Learning 확장에서 패키지를 설치하라는 메시지가 표시됩니다.

## <a name="view-models"></a>모델 보기

데이터베이스에 저장된 ONNX 모델을 보려면 아래 단계를 수행합니다.

1. **모델 가져오기 또는 보기**를 클릭합니다.

1. **onnxruntime**, **mlflow** 및 **mlflow-dbstore**를 설치하라는 메시지가 표시되면 **예**를 클릭합니다.

1. 모델이 저장된 **모델 데이터베이스** 및 **모델 테이블**을 선택합니다.

그러면 모델의 목록이 표시됩니다. 모델 이름 및 설명을 편집하거나 목록에서 모델을 삭제할 수 있습니다.

## <a name="import-a-new-model"></a>새 모델 가져오기

데이터베이스에서 ONNX 모델을 가져오려면 아래 단계를 수행합니다.

1. **모델 가져오기 또는 보기**를 클릭합니다.

1. **onnxruntime**, **mlflow** 및 **mlflow-dbstore**를 설치하라는 메시지가 표시되면 **예**를 클릭합니다.

1. **모델 가져오기**를 클릭합니다.

1. 가져온 모델을 저장할 **모델 데이터베이스**를 선택합니다.

1. 가져온 모델을 저장할 **모델 테이블**을 선택합니다. **기존 테이블**을 선택하거나 **새 테이블**을 만들 수 있습니다. **다음**을 클릭합니다.

1. 모델이 있는 위치를 선택하고 **다음**을 클릭합니다. 다음을 사용할 수 있습니다.
    - **파일 업로드**. 파일의 모델을 사용하려면 이 옵션을 선택합니다. **원본 파일**에서 모델 파일을 선택하고 **다음**을 클릭합니다.
    - **Azure Machine Learning**. Azure Machine Learning의 모델을 사용하려면 이 옵션을 선택합니다. 먼저 **Azure에 로그인**합니다. 그런 다음 **Azure 계정**, **Azure 구독**, **Azure 리소스 그룹** 및 **Azure ML 작업 영역**을 선택합니다. 사용하려는 모델을 선택하고 **다음**을 클릭합니다.

1. 모델 **이름** 및 **설명**을 입력하고 **배포**를 클릭하여 데이터베이스에 모델을 저장합니다.

> [!NOTE]
> Machine Learning 확장은 현재 미리 보기 상태입니다. 따라서 모델이 저장되는 테이블 스키마는 나중에 변경될 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio의 Machine Learning 확장](machine-learning-extension.md)
- [데이터베이스의 패키지 관리](machine-learning-extension-manage-packages.md)
- [예측 만들기](machine-learning-extension-predictions.md)
- [SQL Machine Learning 설명서](../machine-learning/index.yml)
- [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [SQL Edge(미리 보기)에서 Open Neural Network Exchange를 통한 기계 학습 및 AI](/azure/azure-sql-edge/onnx-overview)
