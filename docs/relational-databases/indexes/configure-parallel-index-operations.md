---
title: 병렬 인덱스 작업 구성 | Microsoft 문서
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 627fa6a19c88507034bfbd8a7236b94e17242851
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72908123"
---
# <a name="configure-parallel-index-operations"></a>병렬 인덱스 작업 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 항목에서는 최대 병렬 처리 수준을 정의하고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 이 설정을 수정하는 방법에 대해 설명합니다. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 이상을 실행하는 다중 프로세서 시스템에서는 다른 쿼리와 마찬가지로 인덱스 문이 여러 프로세서(CPU)를 사용하여 인덱스 문과 관련된 검색, 정렬 및 인덱스 작업을 수행할 수 있습니다. 단일 인덱스 문 실행에 사용되는 CPU 수는 [최대 병렬 처리 수준](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 서버 구성 옵션, 현재 작업 및 인덱스 통계에 따라 결정됩니다. max degree of parallelism 옵션은 병렬 계획 실행에 사용할 프로세서의 최대 개수를 결정합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 시스템에서 진행 중인 작업이 많음을 감지하면 문이 실행되기 전에 인덱스 작업의 병렬 처리 수준이 자동으로 감소됩니다. 분할되지 않은 인덱스의 선행 키 열의 고유 값 수가 제한되거나 각 고유 값의 빈도가 상당히 다양한 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 병렬 처리 수준을 줄일 수도 있습니다. 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing)를 참조하세요. 
  
> [!NOTE]  
> 병렬 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서만 사용할 수 있습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **최대 병렬 처리 수준을 설정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   쿼리 최적화 프로그램에서 사용하는 프로세서 수는 대개 최적의 성능을 제공합니다. 그러나 매우 큰 인덱스를 생성, 다시 작성 및 삭제하는 작업에서는 리소스가 많이 소모되므로 인덱스 작업 중 다른 애플리케이션 및 데이터베이스 작업에 사용할 리소스가 부족할 수 있습니다. 이 문제가 발생하면 인덱스 작업에 사용할 프로세서 수를 제한하여 인덱스 문 실행에 사용되는 최대 프로세서 수를 직접 구성할 수 있습니다.  
  
-   MAXDOP 인덱스 옵션을 지정한 쿼리에 대해서만 max degree of parallelism 구성 옵션이 무시됩니다. 다음 표에서는 최대 병렬 처리 수준 구성 옵션 및 MAXDOP 인덱스 옵션에 지정할 수 있는 유효한 정수 값을 보여 줍니다.  
  
    |값|Description|  
    |-----------|-----------------|  
    |0|서버가 현재 시스템 작업에 따라 사용되는 CPU의 수를 결정하도록 지정합니다. 이 값은 기본값이며 권장 설정입니다.|  
    |1|병렬 계획이 생성되지 않습니다. 작업이 직렬로 실행됩니다.|  
    |2-64|지정된 값으로 프로세서 수를 제한합니다. 현재 작업에 따라 지정된 것보다 적은 수의 프로세서가 사용될 수도 있습니다. 사용 가능한 CPU 수보다 더 큰 수를 지정하면 사용 가능한 실제 CPU 수가 사용됩니다.|  
  
-   다음은 병렬 인덱스 실행 및 MAXDOP 인덱스 옵션이 적용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  
  
    -   [CREATE  INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX(...) REBUILD](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)(클러스터형 인덱스에만 해당)  
  
    -   [ALTER TABLE ADD (인덱스) CONSTRAINT](../../t-sql/statements/alter-table-table-constraint-transact-sql.md) 
  
    -   [ALTER TABLE DROP (클러스터형 인덱스) CONSTRAINT](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)   
  
-   `ALTER INDEX (...) REORGANIZE` 문에서는 MAXDOP 인덱스 옵션을 지정할 수 없습니다.  
  
-   쿼리 최적화 프로그램에서 작성 작업에 병렬 처리 수준을 적용할 경우 정렬이 필요한 분할 인덱스 작업의 메모리 요구 사항이 늘어날 수 있습니다. 병렬 처리 수준이 높을수록 메모리 요구 사항이 늘어납니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요.  
  
###  <a name="permissions"></a><a name="Security"></a> <a name="Permissions"></a> 권한  
 테이블 또는 보기에 대한 `ALTER` 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>인덱스에 대한 최대 병렬 처리 수준을 설정하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스에 대한 최대 병렬 처리 수준을 설정할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스에 대한 최대 병렬 처리 수준을 설정할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 확장합니다.  
  
5.  최대 병렬 처리 수준을 설정할 인덱스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **페이지 선택**아래에서 **옵션**을 선택합니다.  
  
7.  **최대 병렬 처리 수준**을 선택하고 1에서 64 사이의 값을 입력합니다.  
  
8.  **확인**을 클릭합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>기존 인덱스에 대한 최대 병렬 처리 수준을 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>새 인덱스에 대한 최대 병렬 처리 수준 설정  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
 
## <a name="see-also"></a>참고 항목
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing)    
[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)     
[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)     
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)      
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)      
[ALTER TABLE table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)       
[ALTER TABLE index_option &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md)    
