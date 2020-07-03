---
title: DQS 데이터베이스 백업 및 복원 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: af6de293d3b5054e90f79a3f2f8f5cae4fbca04a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85886023"
---
# <a name="backing-up-and-restoring-dqs-databases"></a>DQS 데이터베이스 백업 및 복원
  이 항목에서는 DQS 데이터베이스를 백업 및 복원하는 방법에 대해 설명합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   DQS 서버 설치 중에 제공한 데이터베이스 마스터 키에 대한 암호를 알고 있어야 합니다.  
  
-   DQS에서 실행 중인 작업이나 프로세스가 없는지 확인합니다. 이는 **작업 모니터링** 화면을 사용하여 확인할 수 있습니다. 이 화면을 사용하는 방법은 [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md)을 참조하세요.  
  
-   DQS 서버에 로그온한 사용자가 없는지 확인합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
  
-   백업 및 복원 작업을 수행하려면 Windows 사용자 계정이 SQL Server 인스턴스에서 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
-   DQS에서 실행 중인 작업을 종료하거나 실행 중인 프로세스를 중지하려면 DQS_MAIN 데이터베이스에 대한 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="backup-and-restore-dqs-databases"></a><a name="BackupRestore"></a>DQS 데이터베이스 백업 및 복원  
  
1.  Microsoft SQL Server Management Studio를 시작하고 적합한 SQL Server 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 **데이터베이스** 노드를 확장합니다.  
  
3.  DQS_STAGING_DATA 데이터베이스를 백업합니다. SQL Server 데이터베이스 백업에 대한 단계별 지침은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)를 참조하세요.  
  
4.  DQS_PROJECTS 데이터베이스를 백업합니다.  
  
5.  DQS_MAIN 데이터베이스를 백업합니다.  
  
6.  SQL Server의 현재 인스턴스에 대한 연결을 끊고 이러한 데이터베이스를 복원할 SQL Server 인스턴스에 연결합니다.  
  
7.  DQS_MAIN 데이터베이스를 복원합니다. SQL Server 데이터베이스를 복원 하는 방법에 대 한 단계별 지침은 [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)를 참조 하세요.  
  
8.  DQS_PROJECTS 데이터베이스를 복원합니다.  
  
9. DQS_STAGING_DATA 데이터베이스를 복원합니다.  
  
10. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.  
  
11. 쿼리 편집기 창에서 다음 SQL 문을 복사 하 고를 *\<PASSWORD>* DQS 설치 중에 데이터베이스 마스터 키에 대해 제공한 암호로 바꿉니다.  
  
    ```sql  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
    ```  
  
12. F5 키를 눌러 문을 실행합니다. **결과** 창에서 문이 성공적으로 실행되었는지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Manage DQS Databases](../../2014/data-quality-services/manage-dqs-databases.md)  
  
  
