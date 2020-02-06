---
title: 복제할 때 CHECK 제약 조건 해제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66be3c8c81127b107f730fb38b0be10064d72926
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72909376"
---
# <a name="disable-check-constraints-for-replication"></a>복제할 때 CHECK 제약 조건 해제
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 CHECK 제약 조건을 비활성화할 수 있습니다. 명시적으로 복제에 대한 CHECK 제약 조건을 비활성화할 수도 있습니다. 이는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 게시하는 경우 유용할 수 있습니다.  
  
> [!NOTE]  
>  테이블이 복제를 사용하여 게시된 경우 복제 에이전트에서 수행하는 작업에 대한 CHECK 제약 조건은 자동으로 비활성화됩니다. 복제 에이전트가 구독자에서 삽입, 업데이트 또는 삭제를 수행하면 제약 조건이 확인되지 않지만 사용자가 삽입, 업데이트 또는 삭제를 수행하면 제약 조건이 확인됩니다. 데이터가 원래 삽입, 업데이트 또는 삭제될 때 제약 조건이 게시자에 이미 확인되었으므로 복제 에이전트에 대한 제약 조건이 비활성화됩니다. 자세한 내용은 [스키마 옵션 지정](../../relational-databases/replication/publish/specify-schema-options.md)을 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>복제할 때 CHECK 제약 조건을 비활성화하려면  
  
1.  **개체 탐색기**에서 수정하려는 CHECK 제약 조건을 포함하는 테이블을 확장하고 **제약 조건** 폴더를 확장합니다.  
  
2.  수정할 CHECK 제약 조건을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
3.  **CHECK 제약 조건** 대화 상자의 **테이블 디자이너**에서 **복제에 적용** 에 대해 **아니요**를 선택합니다.  
  
4.  **닫기**를 클릭합니다.  

##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>복제할 때 CHECK 제약 조건을 비활성화하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 IDENTITY 열이 있는 테이블과 테이블에 대한 CHECK 제약 조건을 만듭니다. 그런 다음 제약 조건을 삭제하고 NOT FOR REPLICATION 절을 지정하여 다시 만듭니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.doc_exd (column_a int IDENTITY (1,1)   
    CONSTRAINT exd_check CHECK (column_a > 1))   
  
    ALTER TABLE dbo.doc_exd   
    DROP CONSTRAINT exd_check;   
    GO  
    ALTER TABLE dbo.doc_exd    
    ADD CONSTRAINT exd_check CHECK NOT FOR REPLICATION (column_a > 1);  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
###  <a name="TsqlExample"></a>   
## <a name="see-also"></a>참고 항목  
 [스키마 옵션 지정](../../relational-databases/replication/publish/specify-schema-options.md)  
  
  
