---
title: 파티션 구성표 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 515de63f-dfc5-434d-9adb-f3b5992f745a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d57984228e23143d2061df6bf447f978f9bd3c46
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060905"
---
# <a name="modify-a-partition-scheme"></a>파티션 구성표 수정
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 분할된 테이블에 추가되는 다음 파티션을 보관할 파일 그룹을 지정하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 파티션 구성표를 수정할 수 있습니다. 이렇게 하려면 파일 그룹에 NEXT USED 속성을 할당합니다. 빈 파일 그룹이나 파티션이 이미 있는 파일 그룹에 NEXT USED 속성을 할당할 수 있습니다. 즉, 파일 그룹에 한 개 이상의 파티션을 보관할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **분할된 테이블 또는 인덱스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 ALTER PARTITION SCHEME가 적용되는 모든 파일 그룹은 온라인 상태여야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 다음 사용 권한을 통해 ALTER PARTITION SCHEME을 실행할 수 있습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 구성표가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 구성표가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **파티션 구성표를 수정하려면**  
  
 이 특정 동작은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 수행할 수 없습니다. 파티션 구성표를 수정하려면 먼저 구성표를 삭제한 다음 파티션 작성 마법사를 사용하여 원하는 속성이 포함된 새 구성표를 만들어야 합니다. 자세한 내용은 **분할 된 테이블 및 인덱스 만들기**에서 [SQL Server Management Studio를 사용 하 여 분할 된 테이블 및 인덱스 만들기](create-partitioned-tables-and-indexes.md#SSMSProcedure) 를 참조 하세요.  
  
#### <a name="to-delete-a-partition-scheme"></a>파티션 구성표를 삭제하려면  
  
1.  더하기 기호를 클릭하여 파티션 구성표를 삭제할 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **스토리지** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **파티션 구성표** 폴더를 확장합니다.  
  
4.  삭제할 파티션 구성표를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
5.  **개체 삭제** 대화 상자에서 올바른 파티션 구성표를 선택했는지 확인한 다음 **확인**을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-modify-a-partition-scheme"></a>파티션 구성표를 수정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- add five new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test5fg;  
    GO  
    -- if the "myRangePF1" partition function and the "myRangePS1" partition scheme exist,  
    -- drop them from the AdventureWorks2012 database  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
    DROP PARTITION FUNCTION myRangePF1;  
    GO  
    IF EXISTS (SELECT * FROM sys.partition_schemes  
        WHERE name = 'myRangePS1')  
    DROP PARTITION SCHEME myRangePS1;  
    GO  
    -- create the new partition function "myRangePF1" with four partition groups  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    -- create the new partition scheme "myRangePS1"that will use   
    -- the "myRangePF1" partition function with five file groups.  
    -- The last filegroup, "test5fg," will be kept empty but marked  
    -- as the next used filegroup in the partition scheme.  
    CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg, test5fg);  
    GO  
    --Split "myRangePS1" between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    GO  
    -- Allow the "myRangePS1" partition scheme to use the filegroup "test5fg"  
    -- for the partition with boundary_values of 100 and 500  
    ALTER PARTITION SCHEME myRangePS1  
    NEXT USED test5fg;  
    GO  
    ```  
  
 자세한 내용은 [ALTER PARTITION SCHEME&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-partition-scheme-transact-sql)을 참조하세요.  
  
  
