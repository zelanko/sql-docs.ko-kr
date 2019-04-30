---
title: 클러스터형 인덱스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cea4731ee665e401429679d764832247b2a2242
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155375"
---
# <a name="create-clustered-indexes"></a>클러스터형 인덱스 만들기
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 테이블에 클러스터형 인덱스를 만들 수 있습니다. 몇 가지 경우를 제외하고 모든 테이블에는 클러스터형 인덱스가 있어야 합니다. 쿼리 성능을 향상시키는 것 외에도 요청 시 클러스터형 인덱스를 다시 작성하거나 다시 구성하여 테이블 조각화를 제어할 수 있습니다. 뷰에서 클러스터형 인덱스를 만들 수도 있습니다. 클러스터형된 인덱스는 [클러스터형 및 비클러스터형 인덱스 소개](clustered-and-nonclustered-indexes-described.md)항목에 정의되어 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [일반적인 구현 방법](#Implementations)  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **테이블에 클러스터형 인덱스를 만들려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Implementations"></a> 일반적인 구현 방법  
 클러스터형 인덱스는 다음과 같은 방법으로 구현됩니다.  
  
-   **PRIMARY KEY 및 UNIQUE 제약 조건**  
  
     PRIMARY KEY 제약 조건을 만들 때 테이블에 클러스터형 인덱스가 없으며 고유 비클러스터형 인덱스를 지정하지 않은 경우 열에 고유 클러스터형 인덱스가 자동으로 생성됩니다. 기본 키 열에는 NULL 값이 허용되지 않습니다.  
  
     UNIQUE 제약 조건을 만들면 고유 비클러스터형 인덱스가 생성되어 기본적으로 UNIQUE 제약 조건을 적용합니다. 테이블에 클러스터형 인덱스가 없는 경우 고유 클러스터형 인덱스를 지정할 수 있습니다.  
  
     제약 조건의 일부로 생성된 인덱스에는 제약 조건 이름과 같은 이름이 자동으로 지정됩니다. 자세한 내용은 [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md) 및 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)를 참조하세요.  
  
-   **제약 조건의 영향을 받지 않는 인덱스**  
  
     비클러스터형 PRIMARY KEY 제약 조건이 지정된 경우 기본 키 열이 아닌 열의 클러스터형 인덱스를 만들 수 있습니다.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   클러스터형 인덱스 구조를 만들 때는 각 파일과 파일 그룹에서 기존(원본) 구조와 새(대상) 구조를 위한 디스크 공간이 모두 필요합니다. 기존 구조는 인덱스 생성 트랜잭션이 커밋된 후 할당 취소됩니다. 정렬에 사용할 임시 디스크 공간이 추가로 필요할 수도 있습니다. 자세한 내용은 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)을 참조하세요.  
  
-   기존의 비클러스터형 인덱스를 여러 개 포함하는 힙에 클러스터형 인덱스를 만들 때는 RID(행 식별자) 대신 클러스터링 키 값을 포함하도록 모든 비클러스터형 인덱스를 다시 작성해야 합니다. 마찬가지로 비클러스터형 인덱스가 여러 개 있는 테이블에서 클러스터형 인덱스를 삭제하면 DROP 작업의 일부로 비클러스터형 인덱스가 모두 다시 작성됩니다. 대형 테이블에서는 이 작업을 수행하는 데 시간이 오래 걸립니다.  
  
     대형 테이블에 인덱스를 만들 경우 클러스터형 인덱스로 시작하고 비클러스터형 인덱스를 작성하는 것이 좋습니다. 기존 테이블에 인덱스를 만들 때는 ONLINE 옵션을 ON으로 설정하는 것이 좋습니다. 이 옵션을 ON으로 설정하면 장기 테이블 잠금이 보유되지 않습니다. 따라서 기본 테이블에 대한 쿼리나 업데이트를 계속할 수 있습니다. 자세한 내용은 [Perform Index Operations Online](perform-index-operations-online.md)을 참조하세요.  
  
-   클러스터형 인덱스의 인덱스 키는 ROW_OVERFLOW_DATA 할당 단위에 기존 데이터가 있는 `varchar` 열을 포함할 수 없습니다. `varchar` 열에 대한 클러스터형 인덱스를 만들고 기존 데이터가 IN_ROW_DATA 할당 단위에 있는 경우에는 데이터를 행 외부로 밀어넣는 열에 대한 후속 삽입 또는 업데이트 동작이 실패합니다. 행 오버플로 데이터가 포함될 수 있는 테이블에 대한 정보를 얻으려면 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql) 동적 관리 함수를 사용합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>개체 탐색기를 사용하여 클러스터형 인덱스를 만들려면  
  
1.  개체 탐색기에서 클러스터형 인덱스를 만들 테이블을 확장합니다.  
  
2.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 인덱스**를 가리킨 다음, **클러스터형 인덱스...** 를 선택합니다.  
  
3.  **새 인덱스** 대화 상자의 **일반** 페이지에서 **인덱스 이름** 상자에 새 인덱스의 이름을 입력합니다.  
  
4.  **인덱스 키 열** 아래에서 **추가...** 를 클릭합니다.  
  
5.  **table_name**_에서 열 선택_ 대화 상자에서 클러스터형 인덱스에 추가할 테이블 열의 확인란을 선택합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  **새 인덱스** 대화 상자에서 **확인**을 클릭합니다.  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>테이블 디자이너를 사용하여 클러스터형 인덱스를 만들려면  
  
1.  개체 탐색기에서 클러스터형 인덱스를 사용하여 테이블을 만들 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 테이블…** 을 클릭합니다.  
  
3.  늘 하던 방식대로 새 테이블을 만듭니다. 자세한 내용은 [테이블 만들기&#40;데이터베이스 엔진&#41;](../tables/create-tables-database-engine.md)를 참조하세요.  
  
4.  위에서 만든 새 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
5.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
6.  **인덱스/키** 대화 상자에서 **추가**를 클릭합니다.  
  
7.  **선택한 기본/고유 키 또는 인덱스** 입력란에서 새 인덱스를 선택합니다.  
  
8.  표에서 **CLUSTERED로 만들기**를 선택하고 속성 오른쪽에 있는 드롭다운 목록에서 **예** 를 선택합니다.  
  
9. **닫기**를 클릭합니다.  
  
10. **파일** 메뉴에서 _table name_ **저장**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-clustered-index"></a>클러스터형 인덱스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [기본 키 만들기](../tables/create-primary-keys.md)   
 [UNIQUE 제약 조건 만들기](../tables/create-unique-constraints.md)  
  
  
