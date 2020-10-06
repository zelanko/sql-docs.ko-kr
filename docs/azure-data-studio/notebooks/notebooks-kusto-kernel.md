---
title: Azure Data Studio의 Kusto 커널을 사용하는 Notebook
description: 이 자습서에서는 Kusto Notebook을 만들고 실행하는 방법을 보여 줍니다.
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: a8379e10e8c3e3af64381e9a4536b253e203964e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725127"
---
# <a name="create-and-run-a-kusto-kql-notebook-preview"></a>Kusto(KQL) Notebook(미리 보기) 만들기 및 실행

이 문서에서는 [Kusto(KQL) 확장](../extensions/kusto-extension.md)을 사용하고 Azure Data Explorer 클러스터에 연결하여 [Azure Data Studio Notebook](./notebooks-guidance.md)을 만들고 실행하는 방법을 보여 줍니다.

Kusto(KQL) 확장을 사용하면 커널 옵션을 **Kusto**로 변경할 수 있습니다.

이 기능은 현재 미리 보기로 제공됩니다.

## <a name="prerequisites"></a>사전 요구 사항

Azure 구독이 아직 없는 경우 시작하기 전에 [Azure 체험 계정](https://azure.microsoft.com/free/)을 만듭니다.

- [연결할 수 있는 데이터베이스를 사용하는 Azure Data Explorer 클러스터](/azure/data-explorer/create-cluster-database-portal)
- [Azure Data Studio](../download-azure-data-studio.md)
- [Azure Data Studio용 Kusto(KQL) 확장](../extensions/kusto-extension.md)

## <a name="create-a-kusto-kql-notebook"></a>Kusto(KQL) Notebook 만들기

다음 단계는 Azure Data Studio에서 Notebook 파일을 만드는 방법을 보여 줍니다.

1. Azure Data Studio에서 Azure Data Explorer 클러스터에 연결합니다.

2. **연결** 창으로 이동한 다음, **서버** 창에서 Kusto 데이터베이스를 마우스 오른쪽 단추로 클릭하고 ‘새 노트북’을 선택합니다. **파일** > **새 Notebook**으로 이동해도 됩니다.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-new-notebook.png" alt-text="Notebook 열기":::

3. **커널**에서 *Kusto*를 선택합니다. **연결 대상** 메뉴가 클러스터 이름과 데이터베이스로 설정되어 있는지 확인합니다. 이 문서에서는 Samples 데이터베이스 데이터와 함께 help.kusto.windows.net 클러스터를 사용합니다.

   :::image type="content" source="media/notebooks-kusto-kernel/set-kusto-kernel.png" alt-text="Notebook 열기":::

**파일** 메뉴의 **저장** 또는 **다른 이름으로 저장...** 명령을 사용하여 Notebook을 저장할 수 있습니다.

Notebook을 열려면 **파일** 메뉴의 **파일 열기...** 명령을 사용하거나 **시작** 페이지의 **파일 열기**를 선택하거나 명령 팔레트에서 **파일: 열기** 명령을 사용할 수 있습니다.

## <a name="change-the-connection"></a>연결 변경

Notebook의 Kusto 연결을 변경하려면 다음을 수행합니다.

1. Notebook 도구 모음에서 **연결 대상** 메뉴를 선택하고 **연결 변경**을 선택합니다.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-select-attach-to-change-connections.png" alt-text="Notebook 열기":::

   > [!Note]
   > 데이터베이스 값이 채워져 있는지 확인합니다. Kusto Notebook에 데이터베이스가 지정되어 있어야 합니다.

2. 이제 최근 연결 서버를 선택하거나 새 연결 정보를 입력하여 연결할 수 있습니다.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-change-connection-cluster.png" alt-text="Notebook 열기":::

   > [!Note]
   > `https://` 없이 클러스터 이름을 지정합니다.

## <a name="run-a-code-cell"></a>코드 셀 실행

셀 왼쪽에 있는 **셀 실행** 단추를 선택하여 현재 위치에서 실행할 수 있는 KQL 쿼리가 포함된 셀을 만들 수 있습니다. 결과는 셀이 실행된 후 Notebook에 표시됩니다.

예를 들면 다음과 같습니다.

1. 도구 모음에서 **+코드** 명령을 선택하여 새 코드 셀을 추가합니다.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-kernel-code.png" alt-text="Notebook 열기":::

2. 다음 예제를 복사하여 셀에 붙여넣은 다음 **셀 실행**을 선택합니다. 이 예제에서는 특정 이벤트 유형에 대한 StormEvents 데이터를 쿼리합니다.

   ```kusto
    StormEvents
    | where EventType == "Waterspout"
   ```

   :::image type="content" source="media/notebooks-kusto-kernel/run-kusto-notebook-cell.png" alt-text="Notebook 열기":::

## <a name="save-the-result-or-show-chart"></a>결과 저장 또는 차트 표시

결과를 반환하는 스크립트를 실행하는 경우 결과 위에 표시되는 도구 모음을 사용하여 결과를 다른 형식으로 저장할 수 있습니다.

- CSV로 저장
- Excel로 저장
- JSON으로 저장
- XML로 저장
- 차트 표시

```kusto
    StormEvents
    | limit 10
```

:::image type="content" source="media/notebooks-kusto-kernel/run-notebook-save-results.png" alt-text="Notebook 열기":::

## <a name="known-issues"></a>알려진 문제

| 세부 정보 | 해결 방법 |
|---------|------------|
| [쿼리 결과는 열 머리글만 표시](https://github.com/microsoft/azuredatastudio/issues/12565)합니다. | 해당 없음 |

[기능 요청](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=)을 제출하여 제품 팀에 피드백을 제공할 수 있습니다.  
[버그](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=)를 제출하여 제품 팀에 피드백을 제공할 수 있습니다.

## <a name="next-steps"></a>다음 단계

Notebook에 대한 자세한 정보:

- [Azure Data Studio용 Kusto(KQL) 확장](../extensions/kusto-extension.md)
- [Azure Data Studio에서 Notebook을 사용하는 방법](./notebooks-guidance.md)
- [Python 노트북 만들기 및 실행](./notebooks-python-kernel.md)
- [SQL Server Notebook 만들기 및 실행](./notebooks-sql-kernel.md)