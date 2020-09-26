---
title: Azure Data Studio에서 Python 커널을 사용하여 Notebook 만들기
description: 이 자습서에서는 Python Notebook을 만들고 실행하는 방법을 보여 줍니다.
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: e019777c629084c5265cac1cd531ee01bdede01f
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364220"
---
# <a name="create-and-run-a-python-notebook"></a>Python 노트북 만들기 및 실행

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

이 자습서에서는 Python 커널을 사용하여 Azure Data Studio에서 Notebook을 만들고 실행하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Azure Data Studio가 설치되어 있음](../download-azure-data-studio.md)

## <a name="create-a-notebook"></a>Notebook 만들기

다음 단계는 Azure Data Studio에서 Notebook 파일을 만드는 방법을 보여 줍니다.

1. Azure Data Studio를 엽니다. SQL Server에 연결하라는 메시지가 표시되면 연결하거나 **취소**를 클릭합니다.

1. **파일** 메뉴에서 **새 Notebook**을 선택합니다.

1. **커널**로 **Python 3**을 선택합니다. **연결 대상**이 “localhost”로 설정됩니다.

   :::image type="content" source="media/notebooks-python-kernel/set-kernel-and-attach-to-python.png" alt-text="커널 설정":::

**파일** 메뉴의 **저장** 또는 **다른 이름으로 저장...** 명령을 사용하여 Notebook을 저장할 수 있습니다.

Notebook을 열려면 **파일** 메뉴의 **파일 열기...** 명령을 사용하거나 **시작** 페이지의 **파일 열기**를 선택하거나 명령 팔레트에서 **파일: 열기** 명령을 사용할 수 있습니다.

## <a name="change-the-python-kernel"></a>Python 커널 변경

Notebook에서 Python 커널에 처음으로 연결하면 **Notebook용 Python 구성** 페이지가 표시됩니다. 다음 중 하나를 선택할 수 있습니다.

- **새 Python 설치**를 선택하여 Azure Data Studio용으로 새 Python 사본을 설치합니다.
- **기존 Python 설치 사용**을 선택하여 Azure Data Studio가 사용할 수 있도록 기존 Python 설치의 경로를 지정합니다.

활성 Python 커널의 위치와 버전을 보려면 코드 셀을 만들고 다음 Python 명령을 실행합니다.

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

다른 Python 설치에 연결하려면:

1. **파일** 메뉴에서 **기본 설정**을 선택한 후 **설정**을 선택합니다.
1. **확장** 아래의 **노트북 구성**으로 스크롤합니다.
1. **기존 Python 사용** 아래에서 “Notebook에서 사용하는 기존 python 설치의 로컬 경로입니다” 옵션의 선택을 취소합니다.
1. Azure Data Studio를 다시 시작합니다.

Azure Data Studio가 시작된 후 Python 커널에 연결하면 **Notebook용 Python 구성** 페이지가 표시됩니다. 여기서 새 Python 설치를 만들지 아니면 기존 설치의 경로를 지정할지 선택할 수 있습니다.

## <a name="run-a-code-cell"></a>코드 셀 실행

셀의 왼쪽에 있는 **셀 실행** 단추(원형 검은색 화살표)를 클릭하여 실행 가능한 SQL 코드를 포함하는 셀을 만들 수 있습니다. 결과는 셀 실행이 완료된 후 Notebook에 표시됩니다.

예를 들면 다음과 같습니다.

1. 도구 모음에서 **+코드** 명령을 선택하여 새 Python 코드 셀을 추가합니다.

   :::image type="content" source="media/notebooks-python-kernel/notebook-toolbar-python.png" alt-text="Notebook 도구 모음":::

1. 다음 예를 복사하여 셀에 붙여넣은 다음 **셀 실행**을 클릭합니다. 이 예제에서는 간단한 수치 연산을 수행합니다. 결과는 아래에 나타납니다.

   ```python
   a = 1
   b = 2
   c = a/b
   print(c)
   ```

   :::image type="content" source="media/notebooks-python-kernel/run-notebook-cell-python.png" alt-text="Notebook 셀 실행":::

## <a name="next-steps"></a>다음 단계

Notebook에 대한 자세한 정보:

- [Kqlmagic을 사용하여 Python 확장](./notebooks-kqlmagic.md)
- [Azure Data Studio에서 Notebook을 사용하는 방법](./notebooks-guidance.md)
- [SQL Server Notebook 만들기 및 실행](./notebooks-sql-kernel.md)
