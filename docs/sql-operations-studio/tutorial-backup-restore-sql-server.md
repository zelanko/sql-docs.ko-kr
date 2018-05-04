---
title: SQL 작업 Studio (미리 보기)를 사용 하 여 데이터베이스 백업 및 복원 | Microsoft Docs
description: SQL 작업 Studio (미리 보기)를 사용 하 여 데이터베이스 백업 및 복원 하는 방법을 알아봅니다
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.openlocfilehash: 0285535beb45cbc6ad207280c3152fb875ffc46c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>백업 및 복원을 사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

이 자습서에서 사용 하는 방법을 배웁니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 에:
> [!div class="checklist"]
> * 데이터베이스 백업 
> * 백업 상태 보기
> * 백업을 수행 하는 데 사용 하는 스크립트 생성
> * 데이터베이스 복원
> * 복원 작업의 상태 보기

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server *TutorialDB*합니다. 만들려는 *TutorialDB* 데이터베이스에서 다음 퀵 스타트 중 하나를 완료 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>데이터베이스 백업

1. TutorialDB 데이터베이스 대시보드를 엽니다 (열고는 **서버** 세로 막대 (**CTRL + G**)를 확장 하 고 **데이터베이스**를 마우스 오른쪽 단추로 클릭 **TutorialDB**, 선택한 **관리**). 

2. 열기는 **Backup database** 대화 (클릭 **백업** 에 **작업** 위젯).

   ![작업 위젯](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 이 자습서에서는 기본 백업 옵션을 클릭 **백업**합니다.
   ![백업 대화 상자](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

클릭 한 후 **백업**, **Backup database** 대화 사라지고 백업 프로세스를 시작 합니다.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>백업 상태를 확인 하 고 백업 스크립트를 보려면

1. 열기는 **작업 기록** 에서 시계 아이콘을 클릭 하 여 세로 막대는 *작업 모음* 하거나 키를 눌러 **CTRL + T**합니다.

   ![작업 기록](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 편집기에서 백업 스크립트를 보려면 마우스 오른쪽 단추로 클릭 **성공한 백업 데이터베이스** 선택 **스크립트**합니다.

   ![백업 스크립트](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>백업 파일에서 데이터베이스를 복원 합니다.


1. 열기는 **서버** 세로 막대 (**CTRL + G**) 서버를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리**합니다. 

2. 열기는 **데이터베이스 복원** 대화 (클릭 **복원** 에 **작업** 위젯).

2. 선택 **백업 파일** 에 **에서 복원** 필드입니다. 

3. 에 있는 줄임표 (...)는 **백업 파일 경로** 의 최신 백업 파일을 선택 하 고 필드 *TutorialDB*합니다.

3. 형식 **TutorialDB_Restored** 에 **대상 데이터베이스** 필드에 **대상** 섹션에 새 데이터베이스를 백업 파일을 복원 합니다.

   ![복원(restore)](./media/tutorial-backup-restore-sql-server/restore.png)

4. 클릭 **복원**

5. 복원 작업의 상태를 보려면 클릭 **CTRL + T** 열려는 **작업 기록** 사이드바 합니다.

   ![복원(restore)](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


이 자습서에서는 알아보았습니다 하는 방법:
> [!div class="checklist"]
> * 데이터베이스 백업 
> * 백업 상태 보기
> * 백업을 수행 하는 데 사용 하는 스크립트 생성
> * 데이터베이스 복원
> * 복원 작업의 상태 보기

