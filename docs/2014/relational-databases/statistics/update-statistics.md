---
title: 통계 업데이트 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- updating statistics
- statistics [SQL Server], updating
ms.assetid: 4b97c0b4-03ff-4cfb-9c3f-3b33290b7a2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d83dcaf8ea6f674ae1086d2d02f9423a3bb98358
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053428"
---
# <a name="update-statistics"></a>통계 업데이트
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블 또는 인덱싱된 뷰에 대한 쿼리 최적화 통계를 업데이트할 수 있습니다. 기본적으로 쿼리 최적화 프로그램은 필요할 때 통계를 업데이트하여 쿼리 계획을 향상시킵니다. 하지만 경우에 따라 사용자가 UPDATE STATISTICS 또는 `sp_updatestats` 저장 프로시저를 사용하여 기본 업데이트 주기보다 자주 통계를 업데이트하여 쿼리 성능을 향상시킬 수 있습니다.  
  
 통계를 업데이트하면 쿼리가 최신 통계로 컴파일되지만 쿼리도 다시 컴파일됩니다. 쿼리 계획 향상과 쿼리 재컴파일 소요 시간 간의 성능 균형을 유지해야 하므로 통계를 너무 자주 업데이트하지 않는 것이 좋습니다. 구체적인 성능 균형 유지의 정도는 응용 프로그램에 따라 달라집니다. UPDATE STATISTIC은 통계를 작성하기 위해 tempdb를 사용하여 행 샘플을 정렬할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 통계 개체를 업데이트하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 UPDATE STATISTICS를 사용하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 통해 변경 작업을 하려면 테이블 또는 뷰에 대한 ALTER 권한이 있어야 합니다. `sp_updatestats`를 사용할 경우 **sysadmin** 고정 서버 역할에 멤버 자격이 있거나 데이터베이스(**dbo**)의 소유권이 있어야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-update-a-statistics-object"></a>통계 개체를 업데이트하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 통계를 업데이트할 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 통계를 업데이트할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **통계** 폴더를 확장합니다.  
  
5.  업데이트하려는 통계 개체를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **통계 속성 –***statistics_name* 대화 상자에서 **이 열에 대한 통계 업데이트** 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-update-a-specific-statistics-object"></a>특정 통계 개체를 업데이트하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example updates the statistics for the AK_SalesOrderDetail_rowguid index of the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;   
    GO  
    ```  
  
#### <a name="to-update-all-statistics-in-a-table"></a>테이블의 모든 통계를 업데이트하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all indexes on the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail;   
    GO  
    ```  
  
 자세한 내용은 [UPDATE STATISTICS&#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)를 참조하세요.  
  
#### <a name="to-update-all-statistics-in-a-database"></a>데이터베이스의 모든 통계를 업데이트하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all tables in the database.   
    EXEC sp_updatestats;  
    ```  
  
 자세한 내용은 [sp_updatestats&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)를 참조하세요.  
  
  
