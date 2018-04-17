---
title: 원본 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 485faeca41d64c744a091c0efd4be8a05109a6b8
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>원본 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사)
쿼리를 제공하여 복사할 데이터를 선택하기로 지정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **원본 쿼리 지정**이 표시됩니다. 이 페이지에서는 데이터 원본에서 대상으로 복사할 데이터를 선택하는 SQL 쿼리를 작성하고 테스트합니다. 저장된 쿼리 텍스트를 붙여넣거나 파일에서 쿼리 텍스트를 로드할 수도 있습니다.

## <a name="screen-shot-of-the-source-query-page"></a>원본 쿼리 페이지의 스크린샷  
다음 스크린샷은 마법사의 **원본 쿼리 지정** 페이지를 보여 줍니다.
 
이 간단한 예제에서 사용자는 `SELECT * FROM Sales.Customer` 쿼리를 입력하여 원본 데이터베이스의 **Sales.Customer** 테이블에서 모든 행과 모든 열을 복사합니다.
-   `SELECT *`는 모든 열 복사를 의미합니다.
-   `WHERE` 절이 없으면 모든 행을 복사한다는 의미입니다.
  
 ![가져오기 및 내보내기 마법사의 원본 쿼리 페이지](../../integration-services/import-export-data/media/source-query.png "가져오기 및 내보내기 마법사의 원본 쿼리 페이지")  

## <a name="provide-the-query-and-check-its-syntax"></a>쿼리 입력 및 쿼리 구문 확인
**SQL 문**  
 원본 데이터베이스에서 데이터의 특정 행과 열을 검색할 SELECT 쿼리를 입력합니다. 저장된 쿼리 텍스트를 붙여넣거나 **찾아보기**를 클릭하여 파일에서 쿼리를 로드할 수도 있습니다. 
  
 예를 들어 다음 쿼리는 AdventureWorks 샘플 데이터베이스에서 커미션 비율이 1.5% 이상인 영업 사원에 대한 **SalesPersonID**, **SalesQuota** 및 **SalesYTD**를 검색합니다.  
  
```sql
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

SELECT 쿼리의 추가 예는 [SELECT 예&#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)를 참조하거나 온라인으로 검색해 보세요.  

데이터 원본이 Excel인 경우 이 항목 뒷부분에서 [Excel에 대한 원본 쿼리 입력](#excelQueries) 을 참조하여 쿼리에서 Excel 워크시트 및 범위를 지정하는 방법을 알아봅니다.
  
 **구문 분석**  
 **SQL 문** 입력란에 입력한 SQL 문의 구문을 검사합니다.  
  
> [!NOTE]
> 이 문의 구문을 검사하는 데 필요한 시간이 제한 시간 값인 30초를 초과하면 구문 분석이 중지되고 오류가 발생합니다. 구문 분석이 성공할 때까지는 이 마법사 페이지를 지나서 이동할 수 없습니다. 시간을 초과하지 않는 한 가지 해결 방법은 쿼리 텍스트를 직접 입력하는 대신 사용하려는 쿼리를 기반으로 하는 데이터베이스 뷰를 만든 다음 마법사에서 이 뷰를 쿼리하는 것입니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리의 텍스트가 포함된 저장된 파일을 선택합니다. 파일을 선택하면 해당 파일의 텍스트가 **SQL 문** 의 입력란으로 복사됩니다.  
 
## <a name="excelQueries"></a> Excel에 대한 원본 쿼리 입력

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.

쿼리할 수 있는 Excel 개체는 다음과 같이 세 가지입니다.
-   **워크시트.** 워크시트를 쿼리하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$]**).

    ```sql
    SELECT * FROM [Sheet1$]
    ```

-   **명명된 범위.** 명명된 범위를 쿼리하려면 범위 이름을 사용하면 됩니다(예: **MyDataRange**).
    
    ```sql
    SELECT * FROM MyDataRange
    ```

-   **명명되지 않은 범위.** 명명하지 않은 셀의 범위를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$A1:B4]**).

    ```sql
    SELECT * FROM [Sheet1$A1:B4]
    ```

## <a name="whats-next"></a>다음 단계  
 복사할 데이터를 선택하는 SQL 쿼리를 작성하고 테스트한 후 다음 페이지는 데이터의 대상에 따라 다릅니다.  
  
-   대부분의 대상에 대한 다음 페이지는 **원본 테이블 및 뷰 선택**입니다. 이 페이지에서는 제공한 쿼리를 검토하고 필요에 따라 복사할 열을 선택하고 샘플 데이터를 미리 봅니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
-   대상이 플랫 파일인 경우 다음 페이지는 **플랫 파일 대상 구성**입니다. 이 페이지에서 대상 플랫 파일에 대한 서식 옵션을 지정합니다. (플랫 파일을 구성한 후 다음 페이지는 **원본 테이블 및 뷰 선택**입니다.) 자세한 내용은 [플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)을 참조하세요.  


