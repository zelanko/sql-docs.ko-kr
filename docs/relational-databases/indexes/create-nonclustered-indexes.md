---
title: 비클러스터형 인덱스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], nonclustered indexes
- nonclustered indexes [SQL Server], creating
- nonclustered indexes [SQL Server], UNIQUE constraint
- indexes [SQL Server], nonclustered
- nonclustered indexes [SQL Server], PRIMARY KEY constraint
ms.assetid: 9402029a-1227-46c4-93aa-c2122eb1b943
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b1c6d278e421003b9a7c5db927d8c0d5d9e23343
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639926"
---
# <a name="create-nonclustered-indexes"></a>비클러스터형 인덱스 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 비클러스터형 인덱스를 만들 수 있습니다. 비클러스터형 인덱스는 하나 이상의 선택된 열을 다시 정렬하는 테이블에 저장된 데이터와 구별되는 인덱스 구조입니다. 비클러스터형 인덱스는 기본 테이블을 검색할 때보다 빠르게 데이터를 찾는 데 도움이 될 수 있습니다. 비클러스터형 인덱스의 데이터가 쿼리에 대한 완전한 대답이 되는 경우도 있지만, 비클러스터형 인덱스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 기본 테이블의 행으로 연결할 수도 있습니다. 일반적으로 비클러스터형 인덱스는 클러스터형 인덱스를 적용할 수 없고 자주 사용되는 쿼리의 성능을 개선하거나, 클러스터형 인덱스(힙이라고 함) 없이 테이블에서 행을 찾기 위해 만듭니다. 테이블 또는 인덱싱된 뷰에 비클러스터형 인덱스를 여러 개 만들 수 있습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Implementations"></a> 일반적인 구현 방법  
 비클러스터형 인덱스는 다음 방법으로 구현합니다.  
  
-   **UNIQUE 제약 조건**  
  
     UNIQUE 제약 조건을 만들면 고유 비클러스터형 인덱스가 생성되어 기본적으로 UNIQUE 제약 조건을 적용합니다. 테이블에 클러스터형 인덱스가 없는 경우 고유 클러스터형 인덱스를 지정할 수 있습니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
-   **제약 조건의 영향을 받지 않는 인덱스**  
  
     기본적으로 클러스터링 옵션을 지정하지 않으면 비클러스터형 인덱스가 생성됩니다. 각 테이블에서 만들 수 있는 최대 비클러스터형 인덱스 수는 999개입니다. 여기에는 PRIMARY KEY 또는 UNIQUE 제약 조건을 사용하여 생성된 인덱스가 포함되지만 XML 인덱스는 포함되지 않습니다.  
  
-   **인덱싱된 뷰의 비클러스터형 인덱스**  
  
     뷰에 클러스터형 고유 인덱스를 만든 후 비클러스터형 인덱스를 만들 수 있습니다. 자세한 내용은 [인덱싱된 뷰 만들기](../../relational-databases/views/create-indexed-views.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-nonclustered-index-by-using-the-table-designer"></a>테이블 디자이너를 사용하여 비클러스터형 인덱스를 만들려면  
  
1.  개체 탐색기에서 비클러스터형 인덱스를 만들 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  비클러스터형 인덱스를 만들 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
4.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
5.  **인덱스/키** 대화 상자에서 **추가**를 클릭합니다.  
  
6.  **선택한 기본/고유 키 또는 인덱스** 입력란에서 새 인덱스를 선택합니다.  
  
7.  표에서 **CLUSTERED로 만들기**를 선택하고 속성 오른쪽에 있는 드롭다운 목록에서 **아니요** 를 선택합니다.  
  
8.  **닫기**를 클릭합니다.  
  
9. **파일** 메뉴에서 **Save***table_name*을 클릭합니다.  
  
#### <a name="to-create-a-nonclustered-index-by-using-object-explorer"></a>개체 탐색기를 사용하여 비클러스터형 인덱스를 만들려면  
  
1.  개체 탐색기에서 비클러스터형 인덱스를 만들 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  비클러스터형 인덱스를 만들 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 인덱스**를 가리킨 다음 **비클러스터형 인덱스...** 를 선택합니다.  
  
5.  **새 인덱스** 대화 상자의 **일반** 페이지에서 **인덱스 이름** 상자에 새 인덱스의 이름을 입력합니다.  
  
6.  **인덱스 키 열**아래에서 **추가...** 를 클릭합니다.  
  
7.  **Select Columns from***table_name* 대화 상자에서 비클러스터형 인덱스에 추가할 테이블 열의 확인란을 선택합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **새 인덱스** 대화 상자에서 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-nonclustered-index-on-a-table"></a>테이블에 비클러스터형 인덱스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named IX_ProductVendor_VendorID and delete it if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
                WHERE name = N'IX_ProductVendor_VendorID')   
        DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;   
    GO  
    -- Create a nonclustered index called IX_ProductVendor_VendorID   
    -- on the Purchasing.ProductVendor table using the BusinessEntityID column.   
    CREATE NONCLUSTERED INDEX IX_ProductVendor_VendorID   
        ON Purchasing.ProductVendor (BusinessEntityID);   
    GO  
    ```  
  
## <a name="related-content"></a>관련 내용  
[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
[SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md) 
