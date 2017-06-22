---
title: "포괄 열을 사용하여 인덱스 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 815756ed3e14540705a1c2cdbab16d5648a6d2ec
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="create-indexes-with-included-columns"></a>포괄 열을 사용하여 인덱스 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 비클러스터형 인덱스의 기능을 확장하도록 포괄 열 또는 키가 아닌 열을 추가하는 방법에 대해 설명합니다. 키가 아닌 열을 포함하여 여러 쿼리를 처리하는 비클러스터형 인덱스를 만들 수 있습니다. 이는 키가 아닌 열에 다음과 같은 장점이 있기 때문입니다.  
  
-   키가 아닌 열은 인덱스 키 열로 사용할 수 없는 데이터 형식입니다.  
  
-   인덱스 키 열의 수 또는 인덱스 키 크기를 계산할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 키가 아닌 열을 고려하지 않습니다.  
  
 쿼리의 모든 열이 키 열 또는 키가 아닌 열로 인덱스에 포함되면 키가 아닌 열이 있는 인덱스는 쿼리 성능을 상당히 향상시킬 수 있습니다. 성능이 향상되는 이유는 쿼리 최적화 프로그램이 테이블 또는 클러스터형 인덱스 데이터에 액세스하지 않고 인덱스 내에서 모든 열 값을 찾을 수 있으므로 디스크 I/O 작업을 줄어들기 때문입니다.  
  
> [!NOTE]  
>  인덱스에 쿼리가 참조하는 모든 열이 들어 있으면 일반적으로 이 인덱스는 *쿼리를 포함*한다고 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [디자인 권장 구성](#DesignRecs)  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **키가 아닌 열이 있는 인덱스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="DesignRecs"></a> 디자인 권장 구성  
  
-   검색 및 조회에 사용된 열만 키 열이 되도록 인덱스 키 크기가 큰 비클러스터형 인덱스를 다시 디자인합니다. 쿼리를 포함한 다른 모든 열을 키가 아닌 열로 만듭니다. 이 방법을 통해 쿼리를 포함하는 데 필요한 모든 열을 가지게 되지만 인덱스 키 자체는 작으며 효과적입니다.  
  
-   비클러스터형 인덱스에 키가 아닌 열을 포함하여 현재 인덱스 크기 제한인 최대 32개의 키 열 및 최대 1,700바이트([!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 이전에는 16개의 키 열 및 900바이트)의 인덱스 키 크기를 초과하지 않도록 할 수 있습니다. 인덱스 키 열의 수 또는 인덱스 키 크기를 계산할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 키가 아닌 열은 계산하지 않습니다.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   키가 아닌 열은 비클러스터형 인덱스에 대해서만 정의할 수 있습니다.  
  
-   **text**, **ntext**및 **image** 를 제외한 모든 데이터 형식을 키가 아닌 열로 사용할 수 있습니다.  
  
-   결정적이면서 정확하거나 정확하지 않은 계산 열은 키가 아닌 열이 될 수 있습니다. 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요.  
  
-   **image**, **ntext**및 **text** 데이터 형식에서 파생된 계산 열은 계산 열 데이터 형식이 키가 아닌 인덱스 열로 허용되는 한 키가 아닌 열이 될 수 있습니다.  
  
-   테이블의 인덱스를 먼저 삭제하지 않으면 키가 아닌 열을 테이블에서 삭제할 수 없습니다.  
  
-   다음 경우를 제외하고 키가 아닌 열은 변경할 수 없습니다.  
  
    -   열의 Null 허용 여부를 NOT NULL에서 NULL로 변경합니다.  
  
    -   **varchar**, **nvarchar**또는 **varbinary** 열의 길이를 늘립니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>키가 아닌 열이 있는 인덱스를 만들려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 키가 아닌 열이 있는 인덱스를 만들 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 키가 아닌 열이 있는 인덱스를 만들 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 인덱스**를 가리킨 다음 **비클러스터형 인덱스...**를 선택합니다.  
  
5.  **새 인덱스** 대화 상자의 **일반** 페이지에서 **인덱스 이름** 상자에 새 인덱스의 이름을 입력합니다.  
  
6.  **인덱스 키 열** 탭 아래에서 **추가...**를 클릭합니다.  
  
7.  **table_name***에서 열 선택* 대화 상자에서 인덱스에 추가할 테이블 열의 확인란을 선택합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **포괄 열** 탭 아래에서 **추가...**를 클릭합니다.  
  
10. **table_name***에서 열 선택* 대화 상자에서 키가 아닌 열로 인덱스에 추가할 테이블 열의 확인란을 선택합니다.  
  
11. **확인**을 클릭합니다.  
  
12. **새 인덱스** 대화 상자에서 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>키가 아닌 열이 있는 인덱스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
  

