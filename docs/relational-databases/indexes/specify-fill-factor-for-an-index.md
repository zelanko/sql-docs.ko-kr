---
title: 인덱스의 채우기 비율 지정 | Microsoft 문서
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- fill factor [SQL Server]
- page splits [SQL Server]
ms.assetid: 237a577e-b42b-4adb-90cf-aa7fb174f3ab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a80d893cd942e7d8c1e9bb12b6fa21a3247d7e52
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401628"
---
# <a name="specify-fill-factor-for-an-index"></a>인덱스의 채우기 비율 지정
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 채우기 비율의 역할에 대해 설명하고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 인덱스의 채우기 비율 값을 지정하는 방법에 대해 설명합니다.  
  
 채우기 비율 옵션은 미세 조정 인덱스 데이터 저장소와 성능을 위해 제공됩니다. 인덱스를 만들거나 다시 작성할 때 채우기 비율에 따라 각 리프 수준 페이지에서 데이터로 채울 공간 비율이 결정되므로 각 페이지에서 나머지 부분을 이후 인덱스 증가에 대비한 여유 공간으로 확보할 수 있습니다. 예를 들어 채우기 비율 값을 80으로 지정하면 기본 테이블의 데이터 추가에 따른 인덱스 확장을 위해 각 리프 수준 페이지의 20%가 비게 됩니다. 빈 공간은 인덱스의 끝이 아닌 인덱스 행 간에 예약됩니다.  
  
 채우기 비율 값은 0%에서 100% 사이이며 서버 차원의 기본값은 0입니다. 이 값은 리프 수준 페이지가 꽉 채워짐을 의미합니다.  
  
> [!NOTE]  
>  채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [성능 고려 사항](#Performance)  
  
     [보안](#Security)  
  
-   **인덱스의 채우기 비율을 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Performance"></a> 성능 고려 사항  
  
#### <a name="page-splits"></a>페이지 분할  
 채우기 비율 값을 적절히 선택하여 기본 테이블에 데이터가 추가될 때 인덱스 확장을 위한 충분한 공간을 제공함으로써 페이지 분할 가능성을 줄일 수 있습니다. 가득찬 인덱스 페이지에 새 행이 추가되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 행의 절반 정도를 새 페이지로 옮겨 새 행을 위한 공간을 만듭니다. 이러한 재구성을 페이지 분할이라고 합니다. 페이지 분할은 새 레코드를 위한 공간을 만들지만 수행하는 데 시간이 걸리고 리소스를 많이 사용하는 작업입니다. 또한 I/O 작업을 늘리는 조각화의 원인이 되기도 합니다. 페이지가 자주 분할되면 새 채우기 비율 값이나 기존 채우기 비율 값으로 데이터를 재배포하여 인덱스를 다시 작성할 수 있습니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
 채우기 비율 값을 0이 아닌 낮은 값으로 설정하면 인덱스 증가에 따른 페이지 분할을 줄일 수 있지만 인덱스에 더 많은 저장 공간이 필요하게 되고 읽기 성능이 저하될 수 있습니다. 삽입 및 업데이트 작업이 많은 애플리케이션에서도 대개 데이터베이스 읽기 횟수가 데이터베이스 쓰기 횟수보다 10 대 5 정도로 훨씬 많습니다. 따라서 기본값 이외의 채우기 비율을 지정하면 채우기 비율 설정에 반비례하는 양만큼 데이터베이스 읽기 성능이 저하됩니다. 예를 들어 채우기 비율 값을 50으로 지정하면 데이터베이스 읽기 성능이 두 배 떨어집니다. 인덱스에 더 많은 페이지가 포함되므로 읽기 성능이 저하되어 데이터 검색에 필요한 디스크 IO 작업이 늘어납니다.  
  
#### <a name="adding-data-to-the-end-of-the-table"></a>테이블 끝에 데이터 추가  
 새 데이터가 테이블에 균일하게 분포된 경우 0이나 100이 아닌 채우기 비율을 지정하면 성능이 향상될 수 있습니다. 그러나 모든 데이터를 테이블 끝에 추가한 경우 인덱스 페이지의 빈 공간이 꽉 채워지지 않습니다. 예를 들어 인덱스 키 열이 IDENTITY 열이면 새 행의 키는 항상 증가하며 인덱스 행은 인덱스 끝에 논리적으로 추가됩니다. 행의 크기를 늘리는 데이터로 기존 행을 업데이트하려는 경우 100 미만의 채우기 비율을 사용합니다. 각 페이지에 추가 바이트를 설정하면 길어지는 행으로 인해 발생하는 페이지 분할을 최소화하는 데 도움이 됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-specify-a-fill-factor-by-using-table-designer"></a>테이블 디자이너를 사용하여 채우기 비율을 지정하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스의 채우기 비율을 지정할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  인덱스의 채우기 비율을 지정할 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
4.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
5.  채우기 비율을 지정할 인덱스를 선택합니다.  
  
6.  **채우기 사양**을 확장하고 **채우기 비율** 행을 선택한 다음 원하는 채우기 비율을 입력합니다.  
  
7.  **닫기**를 클릭합니다.  
  
8.  **파일** 메뉴에서 **Save***table_name*을 선택합니다.  
  
#### <a name="to-specify-a-fill-factor-in-an-index-by-using-object-explorer"></a>개체 탐색기를 사용하여 인덱스의 채우기 비율을 지정하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스의 채우기 비율을 지정할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스의 채우기 비율을 지정할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **인덱스** 폴더를 확장합니다.  
  
5.  채우기 비율을 지정할 인덱스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
6.  **페이지 선택**아래에서 **옵션**을 선택합니다.  
  
7.  **채우기 비율** 행에 원하는 채우기 비율을 입력합니다.  
  
8.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-specify-a-fill-factor-in-an-existing-index"></a>기존 인덱스의 채우기 비율을 지정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 기존 인덱스를 다시 작성하고 다시 작성하는 동안 지정한 채우기 비율을 적용합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Rebuilds the IX_Employee_OrganizationLevel_OrganizationNode index   
    -- with a fill factor of 80 on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD WITH (FILLFACTOR = 80);   
    GO  
    ```  
  
#### <a name="another-way-to-specify-a-fill-factor-in-an-index"></a>인덱스의 채우기 비율을 지정하는 다른 방법  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    /* Drops and re-creates the IX_Employee_OrganizationLevel_OrganizationNode index on the HumanResources.Employee table with a fill factor of 80.  
    */  
  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)   
    WITH (DROP_EXISTING = ON, FILLFACTOR = 80);   
    GO  
    ```  
  
 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
  
