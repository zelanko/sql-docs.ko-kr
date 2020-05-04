---
title: Azure Data Studio의 SQL 커널 사용 Notebook
description: 이 자습서에서는 SQL Server Notebook을 만들고 실행하는 방법을 보여 줍니다.
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 70136c114fe1d4e9421400eff5f171a70289098c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178700"
---
# <a name="create-and-run-a-sql-server-notebook"></a>SQL Server Notebook 만들기 및 실행

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 SQL Server를 사용하여 Azure Data Studio에서 Notebook을 만들고 실행하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Azure Data Studio가 설치되어 있음](download-azure-data-studio.md)
- SQL Server가 설치되어 있음
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="new-notebook"></a>새 Notebook

다음 단계는 Azure Data Studio에서 Notebook 파일을 만드는 방법을 보여 줍니다.

1. Azure Data Studio에서 SQL Server에 연결합니다.

2. **서버** 창에서 **연결** 아래를 선택합니다. **새 Notebook**을 선택합니다.

   ![Notebook 열기](media/notebook-tutorial/azure-data-studio-open-notebook.png)

3. **커널** 및 대상 컨텍스트(**연결 대상**)가 채워질 때까지 기다립니다. **커널**이 **SQL**로 설정되어 있는지 확인하고, SQL Server의 **연결 대상**(예제에서는 *localhost*)을 설정합니다.

   ![커널 및 연결 대상 설정](media/notebook-tutorial/set-kernel-and-attach-to.png)

## <a name="run-a-notebook-cell"></a>Notebook 셀 실행

셀 왼쪽의 재생 단추를 눌러 각 Notebook 셀을 실행할 수 있습니다. 결과는 셀 실행이 완료된 후 Notebook에 표시됩니다.

### <a name="code"></a>코드

도구 모음에서 **+코드** 명령을 선택하여 새 코드 셀을 추가합니다.

![Notebook 도구 모음](media/notebooks-guidance/notebook-toolbar.png)

다음 예제에서는 새 데이터베이스를 만듭니다.

```sql
USE master
GO

   -- Drop the database if it already exists
IF  EXISTS (
        SELECT name
        FROM sys.databases
        WHERE name = N'TestNotebookDB'
   )
DROP DATABASE TestNotebookDB
GO

-- Create the database
CREATE DATABASE TestNotebookDB
GO
```

   ![Notebook 셀 실행](media/notebook-tutorial/run-notebook-cell.png)

결과를 반환하는 스크립트를 실행하는 경우 그 결과를 다른 형식으로 저장할 수 있습니다.

- CSV로 저장
- Excel로 저장
- JSON으로 저장
- XML로 저장

예제에서는 [PI](../t-sql/functions/pi-transact-sql.md)의 결과를 반환합니다.

```sql
SELECT PI() AS PI;
GO
```

![Notebook 셀 실행](media/notebook-tutorial/run-notebook-cell-2.png)

### <a name="text"></a>텍스트

도구 모음에서 **+텍스트** 명령을 선택하여 새 텍스트 셀을 추가합니다.

![Notebook 도구 모음](media/notebooks-guidance/notebook-toolbar.png)

셀이 편집 모드로 바뀌고, 이제 markdown을 입력하면서 동시에 미리 보기를 확인할 수 있습니다.

![markdown 셀](media/notebooks-guidance/notebook-markdown-cell.png)

텍스트 셀 바깥쪽을 선택하면 markdown 텍스트가 표시됩니다.

![markdown 텍스트](media/notebooks-guidance/notebook-markdown-preview.png)

## <a name="next-steps"></a>다음 단계

Notebook에 대한 자세한 정보:

- [SQL Server에서 Notebook을 사용하는 방법](notebooks-guidance.md)

- [Azure Data Studio에서 Notebooks를 관리하는 방법](notebooks-manage-sql-server.md)

- [Spark를 사용하여 샘플 Notebook 실행](../big-data-cluster/notebooks-tutorial-spark.md)