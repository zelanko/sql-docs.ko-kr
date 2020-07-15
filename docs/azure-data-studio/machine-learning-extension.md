---
title: Machine Learning 확장(미리 보기)
titleSuffix: Azure Data Studio
description: Azure Data Studio용 Machine Learning 확장을 사용하면 패키지를 관리하고, 기계 학습 모델을 가져오고, 예측을 만들고, SQL 데이터베이스에 대한 실험을 실행하는 notebook을 만들 수 있습니다.
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e6b38724e2cb8fde7fe38a544c3f87fba3cebd45
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352420"
---
# <a name="machine-learning-extension-preview-for-azure-data-studio"></a>Azure Data Studio용 Machine Learning 확장(미리 보기)

[Azure Data Studio](what-is.md)용 Machine Learning 확장을 사용하면 패키지를 관리하고, 기계 학습 모델을 가져오고, 예측을 만들고, SQL 데이터베이스에 대한 실험을 실행하는 notebook을 만들 수 있습니다. 이 확장은 현재 미리 보기로 제공됩니다.

## <a name="prerequisites"></a>필수 구성 요소

Azure Data Studio를 실행하는 컴퓨터에 다음 필수 구성 요소를 설치해야 합니다.

- [Python 3](https://www.python.org/downloads/). Python 설치가 끝나면 [확장 설정](#settings)에서 Python 설치의 로컬 경로를 지정해야 합니다. Azure Data Studio에서 [Python 커널 notebook](notebooks-tutorial-python-kernel.md)을 사용한다면 이 확장은 기본적으로 notebook의 경로를 사용합니다.

- Windows, macOS 또는 Linux용 [Microsoft ODBC driver 17 for SQL Server](../connect/odbc/download-odbc-driver-for-sql-server.md).

- [R 3.5](https://www.r-project.org/)(선택 사항). 3\.5 이외의 다른 버전은 현재 지원되지 않습니다. R 3.5 설치가 끝나면 [확장 설정](#settings)에서 R을 활성화하고 R 설치의 로컬 경로를 지정해야 합니다. 이 작업은 데이터베이스에서 R 패키지를 관리하려는 경우에만 필요합니다.

## <a name="install-the-extension"></a>확장 설치

Azure Data Studio에서 Machine Learning 확장을 설치하려면 다음 단계를 수행하세요.

1. Azure Data Studio에서 확장 관리자를 엽니다. 확장 아이콘을 선택하거나 보기 메뉴에서 확장을 선택합니다.

1. **Machine Learning** 확장을 선택하고 세부 정보를 확인합니다.

1. **Install**을 클릭합니다.

1. **다시 로드**를 클릭하여 확장을 사용 설정합니다. (확장을 처음 설치할 때만 필요합니다.)

<a name="settings"></a>

## <a name="extension-settings"></a>확장 설정

Machine Learning 확장 설정을 변경하려면 다음 단계를 수행하세요.

1. Azure Data Studio에서 확장 관리자를 엽니다. 확장 아이콘을 선택하거나 보기 메뉴에서 확장을 선택합니다.

1. **사용** 확장에서 **Machine Learning** 확장을 찾습니다.

1. **관리** 아이콘을 클릭합니다.

1. **확장 설정** 아이콘을 클릭합니다.

확장 설정은 다음과 같이 표시됩니다.

:::image type="content" source="media/machine-learning-extension/ml-extension-settings.png" alt-text="Machine Learning 확장 설정":::

### <a name="enable-python"></a>Python 사용

데이터베이스에서 Machine Learning 확장과 Python 패키지 관리를 모두 사용하려면 아래 단계를 수행하세요.

> [!IMPORTANT]
> Machine Learning의 기능 대부분이 작동하려면 Python을 사용 설정하고 구성해야 합니다. 데이터베이스 기능에서 Python 패키지 관리를 사용하지 않을 때도 마찬가집니다.

1. **Machine Learning: Python 사용 설정**이 활성화되어 있는지 확인합니다. 이 설정은 기본적으로 사용하도록 설정됩니다.

1. **Machine Learning: Python 경로**에 기존 Python 설치 경로를 입력합니다. Python 실행 파일의 전체 경로이거나 실행 파일이 있는 폴더일 수 있습니다. Azure Data Studio에서 [Python 커널 notebook](notebooks-tutorial-python-kernel.md)을 사용한다면 이 확장은 기본적으로 notebook의 경로를 사용합니다.

### <a name="enable-r"></a>R 사용 설정

데이터베이스에서 Machine Learning 확장과 R 패키지 관리를 모두 사용하려면 아래 단계를 수행하세요.

1. **Machine Learning: R 사용 설정**이 활성화되어 있는지 확인합니다. 이 설정은 기본적으로 사용하지 않도록 설정됩니다.

1. **Machine Learning: R 경로**에 기존 R 설치 경로를 입력합니다. R 실행 파일의 전체 경로여야 합니다. 

## <a name="use-the-machine-learning-extension"></a>Machine Learning 확장 사용

Azure Data Studio에서 Machine Learning 확장을 사용하려면 다음 단계를 수행하세요.

1. Azure Data Studio에서 연결을 엽니다.

1. 서버를 마우스 오른쪽 단추로 클릭하고 **관리**를 선택합니다.

1. **일반**의 왼쪽 메뉴에서 **Machine Learning**을 클릭합니다.

**다음 단계**에 있는 링크를 사용하면 Machine Learning 확장을 사용하여 패키지를 관리하고, 예측을 만들고, 데이터베이스에 모델을 가져오는 방법을 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [데이터베이스의 패키지 관리](machine-learning-extension-manage-packages.md)
- [예측 만들기](machine-learning-extension-predictions.md)
- [모델 가져오기 또는 보기](machine-learning-extension-import-view-models.md)
- [Azure Data Studio의 Notebook](notebooks-guidance.md)
- [SQL Machine Learning 설명서](../machine-learning/index.yml)
- [SQL Edge(미리 보기)에서 Open Neural Network Exchange를 통한 기계 학습 및 AI](/azure/azure-sql-edge/onnx-overview)
