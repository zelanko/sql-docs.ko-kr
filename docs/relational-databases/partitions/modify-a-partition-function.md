---
description: 파티션 함수 수정
title: 파티션 함수 수정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae5bfc09-f27a-4ea9-9518-485278b11674
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8174cdaae012631ff834392d7bb664c82971ca3d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464844"
---
# <a name="modify-a-partition-function"></a>파티션 함수 수정
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 분할된 테이블이나 인덱스의 파티션 함수에 지정된 파티션 수를 하나씩 더하거나 빼서 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블이나 인덱스가 분할되는 방식을 변경할 수 있습니다. 파티션 추가는 기존의 한 파티션을 두 파티션으로 "분할"하고 새 파티션의 경계를 다시 정의하는 것입니다. 파티션 삭제는 두 파티션의 경계를 하나로 "병합"하는 것입니다. 이 마지막 동작에서 한 파티션은 다시 채워지고 다른 한 파티션은 할당되지 않은 상태로 남게 됩니다.  
  
> [!CAUTION]  
>  둘 이상의 테이블 또는 인덱스가 같은 파티션 함수를 사용할 수 있습니다. 파티션 함수를 수정할 경우 단일 트랜잭션에 있는 모든 대상에 영향을 줍니다. 파티션 함수를 수정하기 전에 파티션 함수의 종속성을 확인합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 파티션 함수 수정**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   ALTER PARTITION FUNCTION은 한 파티션을 둘로 분할하거나 두 파티션을 하나로 병합하는 데만 사용할 수 있습니다. 10개의 파티션을 5개로 줄이는 것과 같이 테이블이나 인덱스가 분할되는 방식을 변경하려면 다음 옵션 중 하나를 사용합니다.  
  
    -   원하는 파티션 함수가 있는 분할된 테이블을 새로 만든 다음 INSERT INTO ... SELECT FROM [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 **의** 파티션 관리 마법사 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 이전 테이블의 데이터를 새 테이블에 삽입합니다.  
  
    -   힙에 분할된 클러스터형 인덱스를 만듭니다.  
  
        > [!NOTE]  
        >  분할된 클러스터형 인덱스를 삭제하면 힙이 분할됩니다.  
  
    -   [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX 문에 DROP EXISTING = ON 절을 사용하여 기존의 분할 인덱스를 삭제하고 다시 작성합니다.  
  
    -   ALTER PARTITION FUNCTION 문의 시퀀스를 수행합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 파티션 함수 수정을 위한 복제 지원을 제공하지 않습니다. 게시 데이터베이스의 파티션 함수를 변경하려면 구독 데이터베이스에서 직접 파티션 함수를 수정해야 합니다.  
  
-   ALTER PARTITION FUNCTION의 영향을 받는 모든 파일 그룹이 온라인 상태여야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 ALTER PARTITION FUNCTION을 실행하려면 다음 중 하나의 권한이 필요합니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 함수가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 함수가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **파티션 함수를 수정하려면**  
  
 이 특정 동작은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 수행할 수 없습니다. 파티션 함수를 수정하려면 먼저 함수를 삭제한 다음 파티션 작성 마법사를 사용하여 원하는 속성이 포함된 새 함수를 만들어야 합니다. 자세한 내용은 다음을 참조하세요.  
  
#### <a name="to-delete-a-partition-function"></a>파티션 함수를 삭제하려면  
  
1.  파티션 함수를 삭제할 데이터베이스를 확장한 다음 **스토리지** 폴더를 확장합니다.  
  
2.  **파티션 함수** 폴더를 확장합니다.  
  
3.  삭제할 파티션 함수를 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다.  
  
4.  **개체 삭제** 대화 상자에서 올바른 파티선 함수를 선택했는지 확인한 다음 **확인** 을 클릭합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-split-a-single-partition-into-two-partitions"></a>단일 파티션을 두 개의 파티션으로 분할하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- Look for a previous version of the partition function "myRangePF1" and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called "myRangePF1" that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Split the partition between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    ```  
  
#### <a name="to-merge-two-partitions-into-one-partition"></a>두 개의 파티션을 하나의 파티션으로 병합하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- Look for a previous version of the partition function "myRangePF1" and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called "myRangePF1" that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Merge the partitions between boundary_values 1 and 100  
    --and between boundary_values 100 and 1000 to create one partition  
    --between boundary_values 1 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    MERGE RANGE (100);  
    ```  
  
 자세한 내용은 [ALTER PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)을 참조하세요.  
  
  
