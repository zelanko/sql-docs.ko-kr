---
description: 인덱스 및 제약 조건 활성화
title: 인덱스 및 제약 조건 활성화 | Microsoft 문서
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], enabling
- nonclustered indexes [SQL Server], enabling a disabled index
- index enabling [SQL Server]
- disabled indexes [SQL Server], how to enable
- constraints [SQL Server], enabling
- clustered indexes, enabling disabled indexes
ms.assetid: c55c8865-322e-4ab0-ba04-ea1f56735353
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b9df5eb968e329f67fd9a98f7ddb1d4eff027a35
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460366"
---
# <a name="enable-indexes-and-constraints"></a>인덱스 및 제약 조건 활성화
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 비활성화된 인덱스를 활성화하는 방법에 대해 설명합니다. 비활성화된 인덱스는 다시 작성되거나 삭제될 때까지 비활성화된 상태로 유지됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **비활성화된 인덱스를 활성화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   인덱스를 다시 작성한 후에 해당 인덱스를 비활성화하여 비활성화된 제약 조건은 수동으로 활성화해야 합니다. 연관된 인덱스를 다시 작성하여 PRIMARY KEY 및 UNIQUE 제약 조건을 활성화합니다. PRIMARY KEY 또는 UNIQUE 제약 조건을 참조하는 FOREIGN KEY 제약 조건을 활성화하기 전에 이 인덱스를 다시 작성(활성화)해야 합니다. ALTER TABLE CHECK CONSTRAINT 문을 사용하여 FOREIGN KEY 제약 조건을 활성화합니다.  
  
-   ONLINE 옵션이 ON으로 설정된 경우 비활성화된 클러스터형 인덱스를 다시 작성할 수 없습니다.  
  
-   클러스터형 인덱스를 비활성화하거나 활성화하고 비클러스터형 인덱스를 비활성화하면 클러스터형 인덱스 동작으로 인해 다음과 같은 결과가 비활성화된 비클러스터형 인덱스에 나타납니다.  
  
    |클러스터형 인덱스 동작|비활성화된 비클러스터형 인덱스...|  
    |----------------------------|-----------------------------------|  
    |ALTER INDEX REBUILD|비활성화된 상태로 유지됩니다.|  
    |ALTER INDEX ALL REBUILD|다시 작성되고 활성화됩니다.|  
    |DROP INDEX|비활성화된 상태로 유지됩니다.|  
    |CREATE INDEX WITH DROP_EXISTING|비활성화된 상태로 유지됩니다.|  
  
     클러스터형 인덱스를 새로 만들 때의 동작은 ALTER INDEX ALL REBUILD를 사용할 때와 동일합니다.  
  
-   클러스터형 인덱스와 연관된 비클러스터형 인덱스에 허용된 동작은 두 인덱스 유형의 상태(비활성화되어 있거나 활성화되어 있는지)에 따라 다릅니다. 다음 표에는 비클러스터형 인덱스에 허용된 동작이 요약되어 있습니다.  
  
    |비클러스터형 인덱스 동작|클러스터형 인덱스와 비클러스터형 인덱스가 모두 비활성화됩니다.|클러스터형 인덱스가 활성화되고 비클러스터형 인덱스는 비활성화되거나 활성화됩니다.|  
    |-------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
    |ALTER INDEX REBUILD|동작이 실패합니다.|동작이 성공합니다.|  
    |DROP INDEX|동작이 성공합니다.|동작이 성공합니다.|  
    |CREATE INDEX WITH DROP_EXISTING|동작이 실패합니다.|동작이 성공합니다.|  

-   사용되지 않는 압축된 비클러스터형 인덱스를 다시 빌드할 때 data_compression은 기본적으로 'none'으로 설정됩니다. 다시 말해서 인덱스가 압축되지 않습니다. 비클러스터형 인덱스를 사용하지 않도록 설정할 경우 압축 설정 메타데이터가 손실되기 때문입니다. 이 문제를 해결하려면 rebuild 문에서 명시적 데이터 압축을 지정해야 합니다.

###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. DBCC DBREINDEX를 사용하는 경우 사용자는 테이블의 소유자이거나 **sysadmin** 고정 서버 역할 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-enable-a-disabled-index"></a>비활성화된 인덱스를 활성화하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스를 활성화할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스를 활성화할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **인덱스** 폴더를 확장합니다.  
  
5.  활성화할 인덱스를 마우스 오른쪽 단추로 클릭하고 **다시 작성** 을 선택합니다.  
  
6.  **인덱스 다시 작성** 대화 상자에서 **다시 작성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인** 을 클릭합니다.  
  
#### <a name="to-enable-all-indexes-on-a-table"></a>테이블의 모든 인덱스를 활성화하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스를 활성화할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스를 활성화할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **모두 다시 작성** 을 선택합니다.  
  
5.  **인덱스 다시 작성** 대화 상자에서 **다시 작성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인** 을 클릭합니다. **다시 작성할 인덱스** 표에서 인덱스를 제거하려면 인덱스를 선택한 다음 Delete 키를 누릅니다.  
  
 **인덱스 다시 작성** 대화 상자에는 다음 정보가 표시됩니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-enable-a-disabled-index-using-alter-index"></a>ALTER INDEX를 사용하여 비활성화된 인덱스를 활성화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD;   
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-create-index"></a>CREATE INDEX를 사용하여 비활성화된 인덱스를 활성화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- re-creates the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    -- using the OrganizationLevel and OrganizationNode columns  
    -- and then deletes the existing IX_Employee_OrganizationLevel_OrganizationNode index  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)  
    WITH (DROP_EXISTING = ON);  
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-dbcc-dbreindex"></a>DBCC DBREINDEX를 사용하여 비활성화된 인덱스를 활성화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", IX_Employee_OrganizationLevel_OrganizationNode);  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-alter-index"></a>ALTER INDEX를 사용하여 테이블의 모든 인덱스를 활성화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    ALTER INDEX ALL ON HumanResources.Employee  
    REBUILD;  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-dbcc-dbreindex"></a>DBCC DBREINDEX를 사용하여 테이블의 모든 인덱스를 활성화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", " ");  
    GO  
    ```  
  
 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md), [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md) 및 [DBCC DBREINDEX&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)를 참조하세요.  
  
  
