---
title: "원본 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.providesourcequery.f1"
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# 원본 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사)
쿼리를 제공하여 복사할 데이터를 선택하기로 지정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **원본 쿼리 지정**이 표시됩니다. 이 페이지에서는 데이터 원본에서 대상으로 복사할 데이터를 선택하는 SQL 쿼리를 작성하고 테스트합니다. 저장된 쿼리 텍스트를 붙여넣거나 파일에서 로드할 수도 있습니다.

## <a name="screen-shot-of-the-source-query-page"></a>원본 쿼리 페이지의 스크린샷  
다음 스크린샷은 마법사의 **원본 쿼리 지정** 페이지를 보여 줍니다.
 
이 간단한 예에서는 사용자가 **Sales.Customer** 테이블의 모든 행과 모든 열을 복사하려고 합니다.
  
 ![Source query page of the Import and Export Wizard](../../integration-services/import-export-data/media/source-query.png "Source query page of the Import and Export Wizard")  

## <a name="provide-the-query-and-check-its-syntax"></a>쿼리 입력 및 쿼리 구문 확인
**SQL 문**  
 원본 데이터베이스에서 데이터의 특정 행을 검색할 SELECT 쿼리를 입력합니다. 저장된 쿼리 텍스트를 붙여넣거나 **찾아보기**를 클릭하여 파일에서 로드할 수도 있습니다. 
  
 예를 들어 다음 쿼리는 AdventureWorks 데이터베이스에서 커미션 비율이 1.5% 이상인 영업 사원에 대한 **SalesPersonID**, **SalesQuota** 및 **SalesYTD**를 검색합니다.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

데이터 원본이 Excel인 경우 이 항목 뒷부분에서 [Excel에 대한 원본 쿼리 입력](Provide%20a%20Source%20Query%20%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#excelQueries)을 참조하여 쿼리에서 Excel 워크시트 및 범위를 지정하는 방법을 알아봅니다.

 SELECT 쿼리의 추가 예는 [SELECT 예&#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)를 참조하거나 온라인으로 검색해 보세요.  
  
 **구문 분석**  
 **SQL 문** 입력란에 입력한 SQL 문의 구문을 검사합니다.  
  
> [!NOTE] 이 문의 구문을 검사하는 데 필요한 시간이 제한 시간 값인 30초를 초과하면 구문 분석이 중지되고 오류가 발생합니다. 구문 분석이 성공할 때까지는 이 마법사 페이지를 지나서 이동할 수 없습니다. 시간을 초과하지 않는 한 가지 해결 방법은 쿼리 텍스트를 직접 입력하는 대신 사용하려는 쿼리를 기반으로 하는 데이터베이스 뷰를 만든 다음 마법사에서 이 뷰를 쿼리하는 것입니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 문의 텍스트가 포함된 저장된 파일을 선택합니다. 파일을 선택하면 해당 파일의 텍스트가 **SQL 문**의 입력란으로 복사됩니다.  
 
## <a name="a-nameexcelqueriesa-provide-a-source-query-for-excel"></a><a name="excelQueries"></a> Excel에 대한 원본 쿼리 입력
쿼리할 수 있는 Excel 개체는 다음과 같이 세 가지입니다.
-   **워크시트.** 워크시트를 쿼리하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$]**).

    ```
    SELECT * FROM [Sheet1$]
    ```

-   **명명된 범위.** 명명된 범위를 쿼리하려면 범위 이름을 사용하면 됩니다(예: **MyDataRange**).
    
    ```
    SELECT * FROM MyDataRange
    ```

-   **명명되지 않은 범위.** 명명하지 않은 셀의 범위를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$A1:B4]**).

    ```
    SELECT * FROM [Sheet1$A1:B4]
    ```

워크시트 또는 범위를 원본 테이블로 지정하면 드라이버는 워크시트 또는 범위의 가장 왼쪽에서 비어 있지 않은 첫 번째 셀부터 *인접한* 블록의 셀을 읽습니다. 따라서 원본 데이터에 빈 행이 있으면 안 됩니다. 예를 들어 열 머리글과 데이터 행 사이에 빈 행이 있으면 안 됩니다. 워크시트 맨 위에서 데이터 위에 제목 다음에 빈 행이 있으면 워크시트를 쿼리할 수 없습니다. Excel에서 데이터의 범위에 이름을 할당하고 워크시트 대신 명명된 범위를 쿼리해야 합니다.

## <a name="whats-next"></a>다음 단계  
 복사할 데이터를 선택하는 SQL 쿼리를 작성하고 테스트한 후 다음 페이지는 데이터의 대상에 따라 다릅니다.  
  
-   대부분의 대상에 대한 다음 페이지는 **원본 테이블 및 뷰 선택**입니다. 이 페이지에서는 제공한 쿼리를 검토하고 필요에 따라 복사할 열을 선택하고 샘플 데이터를 미리 봅니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
-   대상이 플랫 파일인 경우 다음 페이지는 **플랫 파일 대상 구성**입니다. 이 페이지에서 대상 플랫 파일에 대한 서식 옵션을 지정합니다. (플랫 파일을 구성한 후 다음 페이지는 **원본 테이블 및 뷰 선택**입니다.) 자세한 내용은 [플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)을 참조하세요.  
