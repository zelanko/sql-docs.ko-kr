---
title: 데이터베이스 백업 및 복원
description: 이 자습서에 따라 Azure Data Studio를 사용하여 데이터베이스를 백업 및 복원하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 5e276a830f5fa6abc9b1fcf70c540d4cb955d5af
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522427"
---
# <a name="backup-and-restore-databases-using-azure-data-studio"></a>Azure Data Studio를 사용하여 데이터베이스 백업 및 복원

이 자습서에서는 Azure Data Studio를 사용하여 다음을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
> * 데이터베이스 백업 
> * 백업 상태 보기
> * 백업을 수행하는 데 사용되는 스크립트 생성
> * 데이터베이스 복원
> * 복원 작업의 상태 보기

## <a name="prerequisites"></a>필수 구성 요소

이 자습서에는 SQL Server *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면 다음 빠른 시작 중 하나를 완료합니다.

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 SQL Server 연결 및 쿼리](quickstart-sql-server.md)

이 자습서를 진행하려면 SQL Server 데이터베이스에 연결해야 합니다. Azure SQL Database에는 자동화된 백업이 있으므로 Azure Data Studio는 Azure SQL Database 백업 및 복원을 수행하지 않습니다. 자세한 내용은 [자동 SQL Database 백업에 대한 자세한 정보](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)를 참조하세요.

## <a name="back-up-a-database"></a>데이터베이스 백업

1. TutorialDB 데이터베이스 대시보드를 열고 **서버** 사이드바를 연 후(**Ctrl+G**) **데이터베이스**를 확장하고 **TutorialDB**를 마우스 오른쪽 단추로 클릭한 후 **관리**를 선택합니다.

2. **데이터베이스 백업** 대화 상자를 엽니다(**작업** 위젯에서 **백업** 클릭).

   ![작업 위젯](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 이 자습서에서는 기본 백업 옵션을 사용하므로 **백업**을 클릭합니다.
   ![백업 대화 상자](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

**백업**을 클릭하면 **데이터베이스 백업** 대화 상자가 사라지고 백업 프로세스가 시작됩니다.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>백업 상태 확인 및 백업 스크립트 확인

1. **작업 기록** 창이 나타나거나 **CTRL+T**를 누릅니다.

   ![작업 기록](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 편집기에서 백업 스크립트를 보려면 **데이터베이스 백업 성공**을 마우스 오른쪽 단추로 클릭하고 **스크립트**를 선택합니다.

   ![백업 스크립트](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>백업 파일에서 데이터베이스 복원

1. **서버** 사이드바를 열고(**Ctrl+G**) 서버를 마우스 오른쪽 단추로 클릭한 이후에 **관리**를 선택합니다.

2. **데이터베이스 복원** 대화 상자를 엽니다(**작업** 위젯에서 **복원** 클릭).

   ![작업 복원](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. **복원 원본** 필드에서 **백업 파일**을 선택합니다.

4. **백업 파일 경로** 필드에서 줄임표(...)를 클릭하고 *TutorialDB*에 대한 최신 백업 파일을 선택합니다.

5. **대상** 섹션의 **대상 데이터베이스** 필드에 **TutorialDB_Restored**를 입력하여 백업 파일을 새 데이터베이스로 복원합니다. 그런 다음, **복원**을 선택합니다.

   ![복원](./media/tutorial-backup-restore-sql-server/restore.png)

6. 복원 작업의 상태를 보려면 **CTRL+T**를 눌러 **작업 기록**을 엽니다.

   ![복원](./media/tutorial-backup-restore-sql-server/task-history-restore.png)