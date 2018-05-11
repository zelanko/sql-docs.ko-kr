---
title: 인덱스 및 제약 조건 비활성화 | Microsoft 문서
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.disableindexes.f1
helpviewer_keywords:
- disabled indexes [SQL Server], index operations
- nonclustered indexes [SQL Server], disabling
- disabled indexes [SQL Server], guidelines
- clustered indexes, disabling
- constraints [SQL Server], disabling
- disabled indexes [SQL Server], viewing
- FOREIGN KEY constraints, disabling
- statistical information [SQL Server], indexes
- index disabling [SQL Server]
- indexed views [SQL Server], disabled indexes
ms.assetid: 2198f1af-fa44-47e9-92df-f4fde322ba18
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eca111e19c0ab16b3f59c90ae42532b9b4192d7d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="disable-indexes-and-constraints"></a>인덱스 및 제약 조건 비활성화
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 인덱스 또는 제약 조건을 비활성화하는 방법에 대해 설명합니다. 인덱스를 비활성화하면 사용자가 인덱스에 액세스할 수 없으며 클러스터형 인덱스의 경우 기본 테이블 데이터에도 액세스할 수 없습니다. 인덱스 정의는 메타데이터에 보관되고 인덱스 통계는 비클러스터형 인덱스에 유지됩니다. 뷰의 비클러스터형 또는 클러스터형 인덱스를 비활성화하면 인덱스 데이터가 물리적으로 삭제됩니다. 테이블의 클러스터형 인덱스를 비활성화하면 테이블 데이터에 액세스할 수 없습니다. 데이터는 테이블에 계속 남아 있지만 인덱스를 삭제하거나 다시 작성할 때까지 DML(데이터 조작 언어) 작업에 데이터를 사용할 수 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **인덱스를 비활성화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   비활성화된 인덱스는 유지 관리되지 않습니다.  
  
-   쿼리 최적화 프로그램에서 쿼리 실행 계획을 만들 때 비활성화된 인덱스는 고려하지 않습니다. 또한 테이블 힌트로 비활성화된 인덱스를 참조하는 쿼리가 실패합니다.  
  
-   기존의 비활성화된 인덱스와 같은 이름을 사용하는 인덱스는 만들 수 없습니다.  
  
-   비활성화된 인덱스는 삭제할 수 없습니다.  
  
-   고유 인덱스를 비활성화하면 다른 테이블에서 인덱싱된 열을 참조하는 모든 FOREIGN KEY 제약 조건과 PRIMARY KEY 또는 UNIQUE 제약 조건도 비활성화됩니다. 클러스터형 인덱스를 비활성화하는 경우 기본 테이블에 대한 들어오는 FOREIGN KEY 제약 조건과 나가는 FOREIGN KEY 제약 조건도 모두 비활성화됩니다. 인덱스가 비활성화되면 경고 메시지에 제약 조건 이름이 나열됩니다. 인덱스를 다시 작성한 후 ALTER TABLE CHECK CONSTRAINT 문을 사용하여 모든 제약 조건을 수동으로 활성화해야 합니다.  
  
-   비클러스터형 인덱스는 관련 클러스터형 인덱스를 비활성화할 경우 자동으로 비활성화됩니다. 이렇게 비활성화된 인덱스는 테이블이나 뷰의 클러스터형 인덱스를 활성화하거나 테이블의 클러스터형 인덱스를 삭제해야 활성화할 수 있습니다. ALTER INDEX ALL REBUILD 문을 사용하여 클러스터형 인덱스를 활성화하지 않는 한 비클러스터형 인덱스는 명시적으로 활성화해야 합니다.  
  
-   ALTER INDEX ALL REBUILD 문은 테이블의 비활성화된 인덱스를 모두 작성하고 비활성화합니다. 뷰의 비활성화된 인덱스는 예외입니다. 뷰의 인덱스는 별도의 ALTER INDEX ALL REBUILD 문으로 활성화해야 합니다.  
  
-   테이블에서 클러스터형 인덱스를 비활성화하면 해당 테이블을 참조하는 뷰의 모든 클러스터형 인덱스와 비클러스터형 인덱스도 비활성화됩니다. 이러한 인덱스는 참조되는 테이블의 인덱스에 따라 다시 작성해야 합니다.  
  
-   클러스터형 인덱스를 삭제하거나 다시 작성할 경우를 제외하고는 비활성화된 클러스터형 인덱스의 데이터 행에 액세스할 수 없습니다.  
  
-   테이블에 비활성화된 클러스터형 인덱스가 없으면 비활성화된 비클러스터형 인덱스를 온라인으로 다시 작성할 수 있습니다. 그러나 ALTER INDEX REBUILD 또는 CREATE INDEX WITH DROP_EXISTING 문을 사용하는 경우에는 비활성화된 클러스터형 인덱스를 오프라인으로 다시 작성해야 합니다. 온라인 인덱스 작업에 대한 자세한 내용은 [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.  
  
-   비활성화된 클러스터형 인덱스가 있는 테이블에서는 CREATE STATISTICS 문을 실행할 수 없습니다.  
  
-   인덱스가 비활성화된 상태이고 다음 조건에 해당하면 AUTO_CREATE_STATISTICS 데이터베이스 옵션이 열에 대한 새 통계를 만듭니다.  
  
    -   AUTO_CREATE_STATISTICS가 ON으로 설정된 경우  
  
    -   열에 대한 기존 통계가 없는 경우  
  
    -   쿼리 최적화 동안 통계가 필요한 경우  
  
-   클러스터형 인덱스가 비활성화되면 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 가 기본 테이블에 대한 정보를 반환할 수 없습니다. 대신 이 문은 클러스터형 인덱스가 비활성화되었다고 보고합니다. [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) 를 사용하여 비활성화된 인덱스의 조각 모음을 수행할 수 없습니다. 이 문은 실패하고 오류 메시지가 표시됩니다. [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) 를 사용하여 비활성화된 인덱스를 다시 작성할 수 있습니다.  
  
-   새 클러스터형 인덱스를 만들면 이전에 비활성화된 비클러스터형 인덱스를 사용할 수 있습니다. 자세한 내용은 [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 ALTER INDEX를 실행하려면 최소한 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-disable-an-index"></a>인덱스를 비활성화하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스를 비활성화할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스를 비활성화할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **인덱스** 폴더를 확장합니다.  
  
5.  비활성화할 인덱스를 마우스 오른쪽 단추로 클릭하고 **사용 안 함**을 선택합니다.  
  
6.  **인덱스 비활성화** 대화 상자에서 올바른 인덱스가 **비활성화할 인덱스** 표에 있는지 확인한 다음 **확인**을 클릭합니다.  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>테이블의 모든 인덱스를 비활성화하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스를 비활성화할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스를 비활성화할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **모두 사용 안 함**을 선택합니다.  
  
5.  **인덱스 비활성화** 대화 상자에서 올바른 인덱스가 **비활성화할 인덱스** 표에 있는지 확인한 다음 **확인**을 클릭합니다. **비활성화할 인덱스** 표에서 인덱스를 제거하려면 인덱스를 선택한 다음 Delete 키를 누릅니다.  
  
 **인덱스 비활성화** 대화 상자에는 다음 정보가 표시됩니다.  
  
 **Index Name**  
 인덱스 이름을 표시합니다. 실행하는 동안 이 열에는 상태를 나타내는 아이콘도 표시됩니다.  
  
 **테이블 이름**  
 인덱스가 생성된 테이블 또는 뷰의 이름을 표시합니다.  
  
 **인덱스 유형**  
 인덱스의 유형( **클러스터형**, **비클러스터형**, **공간**또는 **XML**)을 표시합니다.  
  
 **상태**  
 비활성화 작업의 상태를 표시합니다. 실행 후에 표시될 수 있는 값은 다음과 같습니다.  
  
-   비어 있음  
  
     실행 전에 **상태** 가 비어 있습니다.  
  
-   **진행 중**  
  
     인덱스 비활성화가 시작되었지만 아직 완료되지 않았습니다.  
  
-   **성공**  
  
     비활성화 작업이 성공적으로 완료되었습니다.  
  
-   **오류**  
  
     인덱스 비활성화 작업을 실행하는 동안 오류가 발생하여 작업을 완료하지 못했습니다.  
  
-   **중지됨**  
  
     사용자가 작업을 중지하여 인덱스 비활성화가 완료되지 않았습니다.  
  
 **메시지**  
 비활성화 작업을 실행하는 동안 오류 메시지 텍스트를 제공합니다. 실행 중에는 오류 텍스트가 하이퍼링크로 표시됩니다. 하이퍼링크에는 오류 내용을 설명하는 텍스트가 표시됩니다. 대개의 경우 **메시지** 열에는 전체 메시지 텍스트의 일부만 표시됩니다. 다음과 같은 두 가지 방법으로 전체 텍스트를 볼 수 있습니다.  
  
-   마우스 포인터를 메시지 셀 위로 이동하여 오류 텍스트가 나타나는 도구 설명을 봅니다.  
  
-   하이퍼링크를 클릭하여 전체 오류 메시지가 있는 대화 상자를 표시합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-disable-an-index"></a>인덱스를 비활성화하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- disables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    DISABLE;  
    ```  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>테이블의 모든 인덱스를 비활성화하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Disables all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    DISABLE;  
    ```  
  
 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
  
