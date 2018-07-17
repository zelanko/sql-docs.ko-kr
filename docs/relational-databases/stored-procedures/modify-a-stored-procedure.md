---
title: 저장 프로시저 수정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 68070e87ebe97f02d1a9bc52e55e98547b4de36d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332453"
---
# <a name="modify-a-stored-procedure"></a>저장 프로시저 수정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
    
##  <a name="Top"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 저장 프로시저를 수정하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Restrictions), [보안](#Security)  
  
-   **프로시저 변경에 사용되는 도구:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 CLR 저장 프로시저로 수정할 수 없으며 그 반대의 경우도 마찬가지입니다.  
  
 이전 프로시저 정의가 WITH ENCRYPTION 또는 WITH RECOMPILE을 사용하여 만들어진 경우 이러한 옵션은 ALTER PROCEDURE 문에 포함된 경우에만 활성화됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 프로시저에 대한 ALTER PROCEDURE 권한이 필요합니다.  
  
##  <a name="Procedures"></a> 저장 프로시저 수정 방법  
 다음 중 하나를 사용할 수 있습니다.  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **Management Studio의 프로시저를 수정하려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 프로시저가 속한 데이터베이스를 확장한 다음 **프로그래밍 기능**을 확장합니다.  
  
3.  **저장 프로시저**를 확장하고 수정할 프로시저를 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
4.  저장 프로시저의 텍스트를 수정합니다.  
  
5.  구문을 테스트하려면 **쿼리** 메뉴에서 **구문 분석**을 클릭합니다.  
  
6.  프로시저 정의의 수정 내용을 저장하려면 **쿼리** 메뉴에서 **실행**을 클릭합니다.  
  
7.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트로 업데이트된 프로시저 정의를 저장하려면 **파일** 메뉴에서 **다른 이름으로 저장**을 클릭합니다. 해당 파일 이름을 적용하거나 새 이름으로 바꾼 다음 **저장**을 클릭합니다.  
  
> [!IMPORTANT]  
>  모든 사용자 입력에 대해 유효성을 검사합니다. 유효성 검사를 수행하기 전에는 사용자 입력을 연결하지 마세요. 유효성 검사가 수행되지 않은 사용자 입력으로부터 생성된 명령은 실행하지 마세요.  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **쿼리 편집기에서 프로시저를 변경하려면**  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 프로시저가 속한 데이터베이스를 확장합니다. 또는 도구 모음의 사용 가능한 데이터베이스 목록에서 데이터베이스를 선택합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
3.  **파일** 메뉴에서 **새 쿼리**를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 편집기에 붙여 넣습니다. 이 예에서는 `uspVendorAllInfo` 데이터베이스의 모든 공급업체 이름, 해당 공급업체가 공급하는 제품, 신용 등급 및 사용 가능성을 반환하는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 프로시저를 만듭니다.  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  **파일** 메뉴에서 **새 쿼리**를 클릭합니다.  
  
6.  다음 예를 복사하여 쿼리 편집기에 붙여 넣습니다. 다음 예에서는 `uspVendorAllInfo` 프로시저를 변경합니다. EXECUTE AS CALLER 절이 제거되고 지정된 제품을 제공하는 공급업체만 반환하도록 프로시저 본문이 수정됩니다. `LEFT` 및 `CASE` 함수는 결과 집합의 모양을 사용자 지정합니다.  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  프로시저 정의의 수정 내용을 저장하려면 **쿼리** 메뉴에서 **실행**을 클릭합니다.  
  
8.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트로 업데이트된 프로시저 정의를 저장하려면 **파일** 메뉴에서 **다른 이름으로 저장**을 클릭합니다. 해당 파일 이름을 적용하거나 새 이름으로 바꾼 다음 **저장**을 클릭합니다.  
  
9. 변경된 저장 프로시저를 실행하려면 다음 예시를 실행합니다.  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
  
