---
title: 통계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: statistics
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.stat.properties.f1
- sql13.swb.statistics.filter.f1
- sql13.swb.stat.columns.f1
- sql13.swb.statistics.propertis.f1
helpviewer_keywords:
- creating statistics
- statistics [SQL Server], creating
ms.assetid: 95a455fb-664d-4c95-851e-c6b62d7ebe04
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f4a06d45ab3fa089f07e31ac8b8fd9a3162e820f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32972568"
---
# <a name="create-statistics"></a>통계 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블 또는 인덱싱된 뷰의 하나 이상의 열에 대한 쿼리 최적화 통계를 만들 수 있습니다. 대부분의 쿼리에서 쿼리 최적화 프로그램은 고품질의 쿼리 계획에 필요한 통계를 이미 생성하므로 경우에 따라서 추가 통계를 만들어야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 통계를 만들려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   CREATE STATISTICS 문을 사용하여 통계를 만들기 전에 AUTO_CREATE_STATISTICS 옵션이 데이터베이스 수준에서 설정되었는지 확인합니다. 이렇게 하면 쿼리 최적화 프로그램이 정기적으로 쿼리 조건자 열에 대한 단일 열 통계를 계속 만들 수 있습니다.  
  
-   정적 개체당 최대 32개의 열을 나열할 수 있습니다.  
  
-   필터링된 통계 조건자에 정의된 테이블 열의 정의에 대해 삭제, 이름 변경 또는 변경을 수행할 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 사용자가 테이블 또는 인덱싱된 뷰의 소유자이거나 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할 중 하나의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-statistics"></a>통계를 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 새 통계를 만들 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 새 통계를 만들 테이블을 확장합니다.  
  
4.  **통계** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 통계...** 를 선택합니다.  
  
     **테이블에 대한 새 통계***table_name* 대화 상자의 **일반** 페이지에 다음 속성이 표시됩니다.  
  
     **테이블 이름**  
     통계에서 설명하는 테이블 이름을 표시합니다.  
  
     **통계 이름**  
     통계가 저장되는 데이터베이스 개체 이름을 표시합니다.  
  
     **통계 열**  
     이 통계 집합에서 설명하는 열을 보여 주는 표입니다. 표의 모든 값은 읽기 전용입니다.  
  
     **이름**  
     통계에서 설명하는 열 이름을 표시합니다. 하나의 열일 수도 있고 단일 테이블의 열 조합일 수도 있습니다.  
  
     **데이터 형식**  
     통계에서 설명하는 열의 데이터 형식을 나타냅니다.  
  
     **크기**  
     각 열에 대한 데이터 형식의 크기를 표시합니다.  
  
     **ID**  
     선택 시 ID 열을 나타냅니다.  
  
     **Null 허용**  
     열에 NULL 값을 사용할 수 있는지 여부를 나타냅니다.  
  
     **추가**  
     테이블의 추가 열을 통계 표에 추가합니다.  
  
     **제거**  
     선택한 열을 통계 표에서 제거합니다.  
  
     **위로 이동**  
     선택한 열을 통계 표에서 이전 위치로 이동합니다. 표에서의 위치는 통계 유용성에 큰 영향을 줄 수 있습니다.  
  
     **아래로 이동**  
     선택한 열을 통계 표에서 이후 위치로 이동합니다.  
  
     **이 열에 대한 통계 마지막 업데이트:**  
     통계가 얼마나 오래되었는지를 나타냅니다. 통계는 최신 상태일 때 더욱 가치가 있습니다. 데이터가 크게 변경되거나 부정형 데이터를 추가한 후에는 통계를 업데이트합니다. 데이터가 일관성 있게 배포된 테이블 통계는 자주 업데이트할 필요가 없습니다.  
  
     **이 열에 대한 통계 업데이트**  
     대화 상자를 닫을 때 통계를 업데이트하려면 선택합니다.  
  
     **테이블에 대한 새 통계***table_name* 대화 상자의 **필터** 페이지에 다음 속성이 표시됩니다.  
  
     **필터 식**  
     필터링된 통계에 포함할 데이터 행을 정의합니다. 예를 들어 IPv4 주소를 사용하는 경우 `Production.ProductSubcategoryID IN ( 1,2,3 )`  
  
5.  **테이블에 대한 새 통계***table_name* 대화 상자의 **일반** 페이지에서 **추가**를 클릭합니다.  
  
     **열 선택** 대화 상자에 표시되는 속성은 다음과 같습니다. 이 정보는 읽기 전용입니다.  
  
     **이름**  
     통계에서 설명하는 열 이름을 표시합니다. 하나의 열일 수도 있고 단일 테이블의 열 조합일 수도 있습니다.  
  
     **데이터 형식**  
     통계에서 설명하는 열의 데이터 형식을 나타냅니다.  
  
     **크기**  
     각 열에 대한 데이터 형식의 크기를 표시합니다.  
  
     **ID**  
     선택 시 ID 열을 나타냅니다.  
  
     **Allow NULLs**  
     열에 NULL 값을 사용할 수 있는지 여부를 나타냅니다.  
  
6.  **열 선택** 대화 상자에서 통계를 만들려는 각 열의 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
7.  **테이블에 대한 새 통계***table_name* 대화 상자에서 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-statistics"></a>통계를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Create new statistic object called ContactMail1  
    -- on the BusinessEntityID and EmailPromotion columns in the Person.Person table.   
  
    CREATE STATISTICS ContactMail1  
        ON Person.Person (BusinessEntityID, EmailPromotion);   
    GO  
    ```  
  
4.  위에서 만든 통계는 다음 쿼리의 결과를 향상시킬 수 있습니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT LastName, FirstName  
    FROM Person.Person  
    WHERE EmailPromotion = 2  
    ORDER BY LastName, FirstName;   
    GO  
    ```  
  
 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
  
