---
title: Azure Data Studio의 SQL 커널 사용 Notebook
description: 이 자습서에서는 SQL Server Notebook을 만들고 실행하는 방법을 보여 줍니다.
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: 022950fa27887618f16e5569ffe3370c069ea71c
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745863"
---
# <a name="create-and-run-a-sql-server-notebook"></a>SQL Server Notebook 만들기 및 실행

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 자습서에서는 SQL Server를 사용하여 Azure Data Studio에서 Notebook을 만들고 실행하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Azure Data Studio가 설치되어 있음](download-azure-data-studio.md)
- SQL Server가 설치되어 있음
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="create-a--notebook"></a>Notebook 만들기

다음 단계는 Azure Data Studio에서 Notebook 파일을 만드는 방법을 보여 줍니다.

1. Azure Data Studio에서 SQL Server에 연결합니다.

1. **서버** 창에서 **연결** 아래를 선택합니다. **새 Notebook**을 선택합니다.

   ![Notebook 열기](media/notebook-tutorial/azure-data-studio-open-notebook.png)

1. **커널** 및 대상 컨텍스트(**연결 대상**)가 채워질 때까지 기다립니다. **커널**이 **SQL**로 설정되어 있는지 확인하고, SQL Server의 **연결 대상**(여기서는 *localhost*)을 설정합니다.

   ![커널 및 연결 대상 설정](media/notebook-tutorial/set-kernel-and-attach-to.png)

**파일** 메뉴의 **저장** 또는 **다른 이름으로 저장...** 명령을 사용하여 Notebook을 저장할 수 있습니다. 

Notebook을 열려면 **파일** 메뉴의 **파일 열기...** 명령을 사용하거나 **시작** 페이지의 **파일 열기**를 선택하거나 명령 팔레트에서 **파일: 열기** 명령을 사용할 수 있습니다.

## <a name="change-the-sql-connection"></a>SQL 연결 변경

Notebook에 대한 SQL 연결을 변경하려면 다음을 수행합니다.

1. Notebook 도구 모음에서 **연결 대상** 메뉴를 선택하고 **연결 변경**을 선택합니다.

   ![Notebook 도구 모음에서 연결 대상 메뉴 클릭](./media/notebook-tutorial/select-attach-to-1.png)

2. 이제 최근 연결 서버를 선택하거나 새 연결 정보를 입력하여 연결할 수 있습니다.

   ![연결 대상 메뉴에서 서버 선택](./media/notebook-tutorial/select-attach-to-2.png)

## <a name="run-a-code-cell"></a>코드 셀 실행

셀의 왼쪽에 있는 **셀 실행** 단추(원형 검은색 화살표)를 클릭하여 실행 가능한 SQL 코드를 포함하는 셀을 만들 수 있습니다. 결과는 셀 실행이 완료된 후 Notebook에 표시됩니다.

예를 들면 다음과 같습니다.

1. 도구 모음에서 **+코드** 명령을 선택하여 새 코드 셀을 추가합니다.

   ![Notebook 도구 모음](media/notebooks-guidance/notebook-toolbar.png)

1. 다음 예를 복사하여 셀에 붙여넣은 다음 **셀 실행**을 클릭합니다. 다음 예제에서는 새 데이터베이스를 만듭니다.

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

## <a name="save-the-result"></a>결과 저장

결과를 반환하는 스크립트를 실행하는 경우 결과 위에 표시되는 도구 모음을 사용하여 결과를 다른 형식으로 저장할 수 있습니다.

- CSV로 저장
- Excel로 저장
- JSON으로 저장
- XML로 저장

예를 들어 다음 코드는 [PI](../t-sql/functions/pi-transact-sql.md)의 결과를 반환합니다.

```sql
SELECT PI() AS PI;
GO
```

![Notebook 셀 실행](media/notebook-tutorial/run-notebook-cell-2.png)

## <a name="next-steps"></a>다음 단계

Notebook에 대한 자세한 정보:

- [Azure Data Studio에서 Notebook을 사용하는 방법](notebooks-guidance.md)
- [Python 노트북 만들기 및 실행](notebooks-tutorial-python-kernel.md)
- [Spark를 사용하여 샘플 Notebook 실행](../big-data-cluster/notebooks-tutorial-spark.md)