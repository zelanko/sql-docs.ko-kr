---
title: 데이터베이스 백업 및 복원
titleSuffix: Azure Data Studio
description: Azure Data Studio를 사용 하 여 데이터베이스를 백업 및 복원 하는 방법을 알아봅니다
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e6025c59206f48fe6cf5cd5bf5182ea73090bbf
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207132"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>데이터베이스 백업 및 복원을 사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

이 자습서에서 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 사용법을 알아봅니다.
> [!div class="checklist"]
> * 데이터베이스 백업 
> * 백업 상태를 보려면
> * 백업하는 데 사용되는 스크립트를 생성하는 방법.
> * 데이터베이스 복원
> * 복원 작업의 상태를 보려면

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면, 다음 빠른 시작 중 하나를 수행합니다.

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 SQL Server에 연결 및 쿼리](quickstart-sql-server.md)

이 자습서에서는 SQL Server 데이터베이스에 연결 합니다. Azure SQL Database에 자동화 된 백업, Azure Data Studio Azure SQL Database 백업을 수행 하지 않으며 복원 하도록 합니다. 자세한 내용은 참조 하세요 [자동 SQL Database 백업에 알아보기](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)합니다.

## <a name="backup-a-database"></a>데이터베이스 백업

1. TutorialDB 데이터베이스 대시보드를 열고(**서버** 사이드바(**CTRL + G**)), **데이터베이스**를 확장하고, **TutorialDB**에서 마우스 오른쪽 단추로 클릭한 뒤, **관리**를 선택합니다.

2. **Backup database** 대화 상자를 엽니다(**작업** 위젯에서 **백업** 클릭).

   ![작업 위젯](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 이 자습서에서는 기본 백업 옵션을 사용하므로, **백업**을 클릭합니다.
   ![백업 대화 상자](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

**백업**을 클릭하고 나면 **Backup database** 대화 상자가 사라지고 백업 프로세스가 시작됩니다.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>백업 상태 확인 및 백업 스크립트 보기

1. *작업 모음*에 있는 시계 아이콘을 클릭하거나 **CTRL-T**를 눌러서 **작업 기록** 사이드바를 엽니다.

   ![작업 기록](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 백업 스크립트를 편집기에서 보려면 **데이터베이스 백업 성공**을 마우스 오른쪽 단추로 클릭하고 **스크립트**를 선택합니다.

   ![백업 스크립트](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>백업 파일에서 데이터베이스 복원


1. **서버** 사이드바(**CTRL + G**)를 열고, 서버를 마우스 오른쪽 단추로 클릭한 뒤 **관리**를 선택합니다. 

2. **데이터베이스 복원** 대화 상자를 엽니다(**작업** 위젯의 **복원** 클릭).

2. **복원 위치** 필드에서 **백업 파일**을 선택합니다. 

3. **백업 파일 경로** 필드에 있는 줄임표(...)를 클릭하고 *TutorialDB*의 최신 백업 파일을 선택합니다.

3. 새 데이터베이스로 백업 파일을 복원하기 위해 **대상** 섹션의 **대상 데이터베이스** 필드에 **TutorialDB_Restored**를 입력합니다.

   ![복원(restore)](./media/tutorial-backup-restore-sql-server/restore.png)

4. **복원**을 클릭합니다.

5. 복원 작업의 상태를 확인하려면 **CTRL + T** 키를 누르고 **작업 기록** 세로 막대를 엽니다.

   ![복원(restore)](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


이 자습서에서는 다음과 같은 방법을 학습했습니다.
> [!div class="checklist"]
> * 데이터베이스 백업 
> * 백업 상태를 보려면
> * 백업하는 데 사용되는 스크립트를 생성하는 방법.
> * 데이터베이스 복원
> * 복원 작업의 상태를 보려면

