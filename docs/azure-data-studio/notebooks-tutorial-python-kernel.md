---
title: Azure Data Studio에서 Python 커널을 사용하여 Notebook 만들기
description: 이 자습서에서는 Python Notebook을 만들고 실행하는 방법을 보여 줍니다.
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 8d0666c74f464535d2de08dd44e92c521cfcd73f
ms.sourcegitcommit: 4f4ca7075a73a7a4d7196dcb279c58e15c2daf37
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82196795"
---
# <a name="create-and-run-a-python-notebook"></a>Python 노트북 만들기 및 실행

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 Python 커널을 사용하여 Azure Data Studio에서 Notebook을 만들고 실행하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Azure Data Studio가 설치되어 있음](download-azure-data-studio.md)

## <a name="new-notebook"></a>새 Notebook

다음 단계는 Azure Data Studio에서 Notebook 파일을 만드는 방법을 보여 줍니다.

1. Azure Data Studio를 엽니다. SQL Server에 연결하라는 메시지가 표시되면 연결하거나 **취소**를 클릭합니다.

1. **파일** 메뉴에서 **새 Notebook**을 선택합니다.

1. **커널**로 **Python 3**을 선택합니다.

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="커널 설정":::

1. Python을 구성하라는 메시지가 표시되면 **Notebook용 Python 구성**에서 다음 중 하나를 선택합니다.

   - **새 Python 설치**를 선택하여 Azure Data Studio용으로 새 Python 사본을 설치하거나
   - **기존 Python 설치 사용**을 선택하여 기존 Python 설치의 경로를 지정합니다.

## <a name="run-a-notebook-cell"></a>Notebook 셀 실행

코드 또는 텍스트를 포함하는 셀을 만들 수 있습니다. 코드 셀을 현재 위치에서 실행하면 셀의 실행이 완료된 후 Notebook에 결과가 표시됩니다. 텍스트 셀을 사용하면 서식이 지정된 문서를 코드 안에 배치할 수 있습니다.

### <a name="code"></a>코드

도구 모음에서 **+코드** 명령을 선택하여 새 Python 코드 셀을 추가합니다.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="Notebook 도구 모음":::

이 예제에서는 간단한 수치 연산을 수행합니다.

```python
a = 1
b = 2
c = a/b
print(c)
```
셀 왼쪽의 재생 단추를 클릭하여 셀을 실행합니다. 결과가 아래에 나타납니다.

:::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="Notebook 셀 실행":::

### <a name="text"></a>텍스트

도구 모음에서 **+텍스트** 명령을 선택하여 새 텍스트 셀을 추가합니다.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python-text.png" alt-text="Notebook 도구 모음":::

셀이 편집 모드로 바뀌고, 이제 markdown을 입력하면서 동시에 미리 보기를 확인할 수 있습니다.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-cell-python.png" alt-text="markdown 셀":::

텍스트 셀 바깥쪽을 선택하면 markdown 텍스트만 표시됩니다.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-preview-python.png" alt-text="markdown 텍스트":::

## <a name="next-steps"></a>다음 단계

Notebook에 대한 자세한 정보:

- [SQL Server에서 Notebook을 사용하는 방법](notebooks-guidance.md)

- [SQL Server Notebook 만들기 및 실행](notebooks-tutorial-sql-kernel.md)

- [Azure Data Studio에서 Notebooks를 관리하는 방법](notebooks-manage-sql-server.md)
