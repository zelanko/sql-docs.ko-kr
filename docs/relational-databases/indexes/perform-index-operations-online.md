---
description: 온라인으로 인덱스 작업 수행
title: 온라인으로 인덱스 작업 수행 | Microsoft 문서
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
ms.prod_service: table-view-index, sql-database
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3b54f8e3f4cc2656469aaccabe810a89cb661e5c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97407361"
---
# <a name="perform-index-operations-online"></a>온라인으로 인덱스 작업 수행
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 항목에서는 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 온라인으로 인덱스를 만들거나, 다시 작성하거나, 삭제하는 방법에 대해 설명합니다. ONLINE 옵션을 사용하면 여러 사용자가 인덱스 작업 동안 기본 테이블이나 클러스터형 인덱스 데이터 및 모든 관련 비클러스터형 인덱스에 동시에 액세스할 수 있습니다. 예를 들어 특정 사용자가 클러스터형 인덱스를 다시 작성하는 동안 해당 사용자와 다른 사용자가 계속해서 기본 데이터를 업데이트하고 쿼리할 수 있습니다. 클러스터형 인덱스 작성 또는 다시 작성 등의 DDL(데이터 정의 언어) 작업을 오프라인으로 수행할 때 이러한 작업은 기본 데이터와 관련 인덱스에 대해 배타적 잠금을 보유합니다. 이로 인해 해당 인덱스 작업이 완료될 때까지 기본 데이터를 수정하거나 쿼리할 수 없습니다.  
  
> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서만 사용할 수 있습니다. 자세한 내용은 [SQL Server의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-version-15.md)을 참조하세요. 
>
> 온라인 인덱스 작업은 Azure SQL Database에서 사용할 수 있습니다.
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **온라인으로 인덱스를 다시 작성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   온라인 인덱스 작업은 인덱스 작업 동안 동시 사용자 작업이 필수적인 1년 365일, 하루 24시간 운영되는 비즈니스 환경에 적합합니다.  
  
-   다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 ONLINE 옵션을 사용할 수 있습니다.  
  
    -   [CREATE  INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP  INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (CLUSTERED 인덱스 옵션을 사용하는 UNIQUE 또는 PRIMARY KEY 제약 조건을 추가하거나 삭제하려는 경우)  
  
-   온라인으로 인덱스를 만들거나, 다시 작성하거나, 삭제하는 작업과 관련된 제한 사항은 [온라인 인덱스 작업에 대한 지침](../../relational-databases/indexes/guidelines-for-online-index-operations.md)을 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rebuild-an-index-online"></a>온라인으로 인덱스를 다시 작성하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 온라인으로 인덱스를 다시 작성할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 온라인으로 인덱스를 다시 작성할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 확장합니다.  
  
5.  온라인으로 다시 작성할 인덱스를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
6.  **페이지 선택** 아래에서 **옵션** 을 선택합니다.  
  
7.  **온라인 DML 처리 허용** 을 선택한 다음 목록에서 **True** 를 선택합니다.  
  
8.  **확인** 을 클릭합니다.  
  
9. 온라인으로 다시 작성할 인덱스를 마우스 오른쪽 단추로 클릭하고 **다시 작성** 을 선택합니다.  
  
10. **인덱스 다시 작성** 대화 상자에서 **다시 작성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인** 을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
### <a name="to-create-rebuild-or-drop-an-index-online"></a>온라인으로 인덱스를 만들거나, 다시 작성하거나, 삭제하려면  
  
다음 예제에서는 AdventureWorks 데이터베이스의 기존 온라인 인덱스를 다시 작성합니다.

```sql
ALTER INDEX AK_Employee_NationalIDNumber
    ON HumanResources.Employee
    REBUILD WITH (ONLINE = ON);
```  
  
다음 예에서는 `NewGroup` 절을 사용하여 온라인으로 클러스터형 인덱스를 삭제하고 결과 테이블을 `MOVE TO` 파일 그룹으로 옮깁니다. 테이블을 이동하기 전과 이동한 후에 파일 그룹에서의 인덱스 및 테이블 배치를 확인하기 위해 `sys.indexes`, `sys.tables`및 `sys.filegroups` 카탈로그 뷰를 쿼리합니다.  
  
[!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  

자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [다시 시작 가능한 인덱스 고려 사항](guidelines-for-online-index-operations.md#resumable-index-considerations)
