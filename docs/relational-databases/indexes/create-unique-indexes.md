---
title: 고유 인덱스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- unique indexes
- designing indexes [SQL Server], unique
- clustered indexes, unique
- indexes [SQL Server], unique
- nonclustered indexes [SQL Server], unique
- unique indexes, design guidelines
ms.assetid: 56b5982e-cb94-46c0-8fbb-772fc275354a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7129c5feb6bc23a7e72dddfa70a10d4d2bc0811c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898601"
---
# <a name="create-unique-indexes"></a>고유 인덱스 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블에 고유 인덱스를 만드는 방법에 대해 설명합니다. 고유 인덱스는 인덱스 키에 중복 값을 포함할 수 없으므로 테이블의 모든 행이 고유합니다. UNIQUE 제약 조건을 만드는 것과 제약 조건의 영향을 받지 않는 고유 인덱스를 만드는 것에는 큰 차이가 없습니다. 데이터 유효성 검사는 이와 동일한 방식으로 수행됩니다. 쿼리 최적화 프로그램에서는 제약 조건에 따라 생성된 고유 인덱스와 수동으로 만든 고유 인덱스를 동일하게 취급합니다. 하지만 열에 UNIQUE 제약 조건을 만들면 인덱스의 목표가 명확해집니다. UNIQUE 제약 조건에 대한 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
 고유 인덱스를 만들 때 중복 키를 무시하도록 옵션을 설정할 수 있습니다. 이 옵션을 **예** 로 설정하고 INSERT 문을 사용하여 여러 행에 적용되는 데이터 추가 작업을 수행하여 중복 키를 만들려고 하면 중복 키가 포함된 행이 추가되지 않습니다. 이 옵션을 **아니요**로 설정하면 삽입 작업이 모두 실패하고 데이터 전체가 롤백됩니다.  
  
> [!NOTE]  
>  두 개 이상의 행에 NULL이 포함된 열이 있으면 단일 열에 대한 고유 인덱스를 만들 수 없습니다. 마찬가지로, 두 개 이상의 행에 NULL이 포함된 열 조합이 있으면 여러 열에 대한 고유 인덱스를 만들 수 없습니다. 이러한 경우는 인덱싱과 관련하여 중복 값으로 취급됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [고유 인덱스의 이점](#Benefits)  
  
     [일반적인 구현 방법](#Implementations)  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **테이블에 고유 인덱스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Benefits"></a> 고유 인덱스의 이점  
  
-   여러 열로 구성된 고유 인덱스를 사용하면 인덱스 키의 각 값 조합이 고유해집니다. 예를 들어 **LastName**, **FirstName**및 **MiddleName** 열의 조합에 대해 고유 인덱스를 만들면 테이블에 있는 각 행에서 이러한 열의 값 조합이 모두 서로 다릅니다.  
  
-   따라서 각 열의 데이터가 고유하면 같은 테이블에서 하나의 고유 클러스터형 인덱스와 여러 개의 고유 비클러스터형 인덱스를 만들 수 있습니다.  
  
-   고유 인덱스를 사용하면 정의된 열의 데이터 무결성이 보장됩니다.  
  
-   고유 인덱스가 제공하는 유용한 추가 정보를 통해 쿼리 최적화 프로그램은 더 효율적인 실행 계획을 생성할 수 있습니다.  
  
###  <a name="Implementations"></a> 일반적인 구현 방법  
 고유 인덱스는 다음과 같은 방법으로 구현됩니다.  
  
-   **PRIMARY KEY 또는 UNIQUE 제약 조건**  
  
     PRIMARY KEY 제약 조건을 만들 때 테이블에 클러스터형 인덱스가 없으며 고유 비클러스터형 인덱스를 지정하지 않은 경우 열에 고유 클러스터형 인덱스가 자동으로 생성됩니다. 기본 키 열에는 NULL 값이 허용되지 않습니다.  
  
     UNIQUE 제약 조건을 만들면 고유 비클러스터형 인덱스가 생성되어 기본적으로 UNIQUE 제약 조건을 적용합니다. 테이블에 클러스터형 인덱스가 없는 경우 고유 클러스터형 인덱스를 지정할 수 있습니다.  
  
     자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 및 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)를 참조하세요.  
  
-   **제약 조건의 영향을 받지 않는 인덱스**  
  
     한 테이블에 고유 비클러스터형 인덱스를 여러 개 정의할 수 있습니다.  
  
     자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
-   **인덱싱된 뷰**  
  
     인덱싱된 뷰를 만들기 위해 하나 이상의 뷰 열에 고유 클러스터형 인덱스가 정의됩니다. 뷰가 실행되고 클러스터형 인덱스에 테이블 데이터가 저장되는 것과 동일한 방법으로 결과 집합이 인덱스의 리프 수준에 저장됩니다. 자세한 내용은 [인덱싱된 뷰 만들기](../../relational-databases/views/create-indexed-views.md)를 참조하세요.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   데이터에 중복된 키 값이 있으면 고유 인덱스, UNIQUE 제약 조건 또는 PRIMARY KEY 제약 조건을 만들 수 없습니다.  
  
-   고유 비클러스터형 인덱스에는 키가 아닌 포괄 열이 포함될 수 있습니다. 자세한 내용은 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-unique-index-by-using-the-table-designer"></a>테이블 디자이너를 사용하여 고유 인덱스를 만들려면  
  
1.  개체 탐색기에서 고유 인덱스를 만들 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  고유 인덱스를 만들 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
4.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 선택합니다.  
  
5.  **인덱스/키** 대화 상자에서 **추가**를 클릭합니다.  
  
6.  **선택한 기본/고유 키 또는 인덱스** 입력란에서 새 인덱스를 선택합니다.  
  
7.  주 표의 **(일반)** 에서 **유형** 을 선택한 다음 목록에서 **인덱스** 를 선택합니다.  
  
8.  **열**을 선택한 다음, 줄임표 **(...)** 를 클릭합니다.  
  
9. **인덱스 열** 대화 상자의 **열 이름**에서 인덱스를 작성할 열을 선택합니다. 최대 16개의 열을 선택할 수 있습니다. 최상의 성능을 얻으려면 인덱스별로 열을 한두 개만 선택하는 것이 좋습니다. 선택한 각 열에 대해 해당 열의 인덱스 값을 오름차순으로 정렬할지 내림차순으로 정렬할지 지정합니다.  
  
10. 인덱스의 모든 열을 선택한 후 **확인**을 클릭합니다.  
  
11. 표의 **(일반)** 에서 **고유 여부** 를 선택한 다음 목록에서 **예** 를 선택합니다.  
  
12. 선택 사항: 주 그리드의 **테이블 디자이너**에서 **중복 키 무시** 를 선택한 다음, 목록에서 **예** 를 선택합니다. 고유 인덱스에 중복 키를 만드는 데이터를 추가하려는 시도를 무시하려는 경우 이와 같이 선택합니다.  
  
13. **닫기**를 클릭합니다.  
  
14. **파일** 메뉴에서 _table\_name_ **저장**을 클릭합니다.  
  
#### <a name="create-a-unique-index-by-using-object-explorer"></a>개체 탐색기를 사용하여 고유 인덱스 만들기  
  
1.  개체 탐색기에서 고유 인덱스를 만들 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  고유 인덱스를 만들 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 인덱스**를 가리킨 다음, **비클러스터형 인덱스...** 를 선택합니다.  
  
5.  **새 인덱스** 대화 상자의 **일반** 페이지에서 **인덱스 이름** 상자에 새 인덱스의 이름을 입력합니다.  
  
6.  **고유** 확인란을 선택합니다.  
  
7.  **인덱스 키 열** 아래에서 **추가...** 를 클릭합니다.  
  
8.  _table\_name_**에서 열 선택** 대화 상자에서 고유 인덱스에 추가할 테이블 열의 확인란을 선택합니다.  
  
9. **확인**을 클릭합니다.  
  
10. **새 인덱스** 대화 상자에서 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-unique-index-on-a-table"></a>테이블에 고유 인덱스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named AK_UnitMeasure_Name and delete it if found  
    IF EXISTS (SELECT name from sys.indexes  
               WHERE name = N'AK_UnitMeasure_Name')   
       DROP INDEX AK_UnitMeasure_Name ON Production.UnitMeasure;   
    GO  
    -- Create a unique index called AK_UnitMeasure_Name  
    -- on the Production.UnitMeasure table using the Name column.  
    CREATE UNIQUE INDEX AK_UnitMeasure_Name   
       ON Production.UnitMeasure (Name);   
    GO  
    ```  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
  
