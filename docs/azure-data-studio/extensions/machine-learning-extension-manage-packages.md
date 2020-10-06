---
title: Machine Learning 확장을 사용하여 패키지 관리
description: Azure Data Studio용 Machine Learning 확장으로 데이터베이스의 Python 또는 R 패키지를 관리하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: sstein
ms.custom: ''
ms.date: 05/19/2020
ms.openlocfilehash: 2977f25e09d3d634d479abd8371d010206edea90
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725170"
---
# <a name="manage-packages-in-database-with-machine-learning-extension-for-azure-data-studio-preview"></a>Azure Data Studio용 Machine Learning 확장(미리 보기)을 사용하여 데이터베이스의 패키지 관리

[Azure Data Studio용 Machine Learning 확장](machine-learning-extension.md)으로 데이터베이스의 Python 또는 R 패키지를 관리하는 방법을 알아봅니다.

> [!IMPORTANT]
> Machine Learning 확장으로 데이터베이스의 패키지를 관리하는 기능은 현재 SQL Server 2019에서의 [Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md)만 지원합니다.

## <a name="prerequisites"></a>필수 구성 요소

- [Azure Data Studio용 Machine Learning 확장](machine-learning-extension.md)을 설치하고 구성합니다. 패키지 관리가 작동하려면 [확장 설정에서 Python 또는 R 설치 경로](machine-learning-extension.md#settings)를 지정해야 합니다.

- **sqlmlutils** 패키지입니다. 패키지가 아직 설치되지 않았다면 Machine Learning 확장에서 이 패키지를 설치하라는 메시지가 표시됩니다.

- SQL Server on Linux에서는 Windows 인증이 지원되지 않습니다. 따라서 SQL 인증을 사용하여 SQL Server on Linux에 연결해야 합니다.

## <a name="manage-python-packages"></a>Python 패키지 관리

Machine Learning 확장을 사용하여 Python 패키지를 설치하거나 제거할 수 있습니다.

### <a name="install-new-python-package"></a>새 Python 패키지 설치

다음 단계를 수행하여 데이터베이스에 Python 패키지를 설치합니다.

1. **데이터베이스의 패키지 관리**를 선택합니다.

1. **sqlmlutils**를 설치하라는 메시지가 표시되면 **예**를 선택합니다.

1. **설치됨** 탭의 **패키지 유형**에서 **Python**을 선택하고 **위치**에서 데이터베이스를 선택합니다.

1. **새 항목 추가** 탭을 선택합니다.

1. **Python 패키지 검색**에 설치할 Python 패키지를 입력하고 **검색**을 선택합니다.

1. **패키지 이름**에 패키지가 있는지 확인하고 **패키지 버전**에 원하는 버전이 있는지 확인합니다.

1. **설치**를 선택합니다.

1. **닫기**를 선택하고 **작업**에서 패키지가 무사히 설치되었는지 확인합니다.

### <a name="uninstall-a-python-package"></a>Python 패키지 제거

다음 단계를 수행하여 데이터베이스에 있는 Python 패키지를 제거합니다.

> [!NOTE]
> 데이터베이스에 설치된 패키지만 제거할 수 있습니다. SQL Server Machine Learning Services를 사용하여 사전 설치된 패키지는 제거할 수 없습니다.

1. **데이터베이스의 패키지 관리**를 선택합니다.

1. **sqlmlutils**를 설치하라는 메시지가 표시되면 **예**를 선택합니다.

1. **설치됨** 탭의 **패키지 유형**에서 **Python**을 선택하고 **위치**에서 데이터베이스를 선택합니다.

1. 제거할 패키지를 선택합니다(복수 선택 가능).

1. **선택한 패키지 제거**를 선택합니다.

1. **닫기**를 선택하고 **작업**에서 패키지가 무사히 설치되었는지 확인합니다.

## <a name="manage-r-packages"></a>R 패키지 관리

Machine Learning 확장을 사용하여 R 패키지를 설치하거나 제거할 수 있습니다.

### <a name="install-new-r-package"></a>새 R 패키지 설치

다음 단계를 수행하여 데이터베이스에 Python 패키지를 설치합니다.

1. **데이터베이스의 패키지 관리**를 선택합니다.

1. **sqlmlutils**를 설치하라는 메시지가 표시되면 **예**를 선택합니다.

1. **설치됨** 탭의 **패키지 유형**에서 **R**을 선택하고 **위치**에서 데이터베이스를 선택합니다.

1. **새 항목 추가** 탭을 선택합니다.

1. **R 패키지 검색**에 설치할 R 패키지를 입력하고 **검색**을 선택합니다.

1. **패키지 이름**에 패키지가 있는지 확인하고 **패키지 버전**에 원하는 버전이 있는지 확인합니다.

1. **설치**를 선택합니다.

1. **닫기**를 선택하고 **작업**에서 패키지가 무사히 설치되었는지 확인합니다.

### <a name="uninstall-an-r-package"></a>R 패키지 제거

다음 단계를 수행하여 데이터베이스에 있는 R 패키지를 제거합니다.

> [!NOTE]
> 데이터베이스에 설치된 패키지만 제거할 수 있습니다. SQL Server Machine Learning Services를 사용하여 사전 설치된 패키지는 제거할 수 없습니다.

1. **데이터베이스의 패키지 관리**를 선택합니다.

1. **sqlmlutils**를 설치하라는 메시지가 표시되면 **예**를 선택합니다.

1. **설치됨** 탭의 **패키지 유형**에서 **R**을 선택하고 **위치**에서 데이터베이스를 선택합니다.

1. 제거할 패키지를 선택합니다(복수 선택 가능).

1. **선택한 패키지 제거**를 선택합니다.

1. **닫기**를 선택하고 **작업**에서 패키지가 무사히 설치되었는지 확인합니다.

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio의 Machine Learning 확장](machine-learning-extension.md)
- [예측 만들기](machine-learning-extension-predictions.md)
- [모델 가져오기 또는 보기](machine-learning-extension-import-view-models.md)
- [Azure Data Studio의 Notebook](../notebooks/notebooks-guidance.md)
- [SQL Machine Learning 설명서](../../machine-learning/index.yml)