---
title: 테이블 및 열에 대한 의미 체계 검색 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server], enabling
ms.assetid: 895d220c-6749-4954-9dd3-2ea4c6a321ff
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34a86f82512dc2f469031aa84d13e6c84ad021c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="enable-semantic-search-on-tables-and-columns"></a>테이블 및 열에 대한 의미 체계 검색 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  문서 또는 텍스트가 들어 있는 선택한 열에서 통계 의미 체계 인덱싱을 사용하거나 사용하지 않도록 설정하는 방법에 대해 설명합니다.  
  
 통계 의미 체계 검색에서는 전체 텍스트 검색을 통해 생성되는 인덱스를 사용하고 추가 인덱스를 만듭니다. 전체 텍스트 검색에 대한 이 종속성의 결과로 새 전체 텍스트 인덱스를 정의하거나 기존 전체 텍스트 인덱스를 변경할 때는 새 의미 체계 인덱스를 만듭니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하거나 이 항목에서 설명하는 대로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 전체 텍스트 인덱싱 마법사와 다른 대화 상자를 사용하여 새 의미 체계 인덱스를 만들 수 있습니다.  
  
##  <a name="BasicEnabling"></a> 의미 체계 인덱스 만들기  
  
###  <a name="reqenable"></a> 의미 체계 인덱스를 만들기 위한 요구 사항 및 제한 사항  
  
-   전체 텍스트 인덱싱이 지원되는 데이터베이스 개체(테이블 및 인덱싱된 뷰 포함)에 대한 인덱스를 만들 수 있습니다.  
  
-   특정 열에 대해 의미 체계 인덱싱을 사용하도록 설정하려면 다음 사전 요구 사항을 충족해야 합니다.  
  
    -   데이터베이스에 대한 전체 텍스트 카탈로그가 있어야 합니다.  
  
    -   테이블에 전체 텍스트 인덱스가 있어야 합니다.  
  
    -   선택한 열이 전체 텍스트 인덱스에 참여해야 합니다.  
  
     이러한 모든 요구 사항을 동시에 만들고 사용하도록 설정할 수 있습니다.  
  
-   전체 텍스트 인덱싱이 지원되는 데이터 형식의 열에 대한 의미 체계 인덱스를 만들 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)를 참조하세요.  
  
-   **varbinary(max)** 열에 대해 전체 텍스트 인덱싱이 지원되는 문서 종류를 지정할 수 있습니다. 자세한 내용은 이 항목의 [방법: 인덱싱할 수 있는 문서 유형 결정](#doctypes) 을 참조하세요.  
  
-   의미 체계 인덱싱에서는 선택한 열에 대한 두 가지 유형의 인덱스, 즉 키 구 인덱스와 문서 유사성 인덱스가 만들어집니다. 의미 체계 인덱싱을 사용하도록 설정할 때 둘 중 한 가지 인덱스 유형만 선택할 수는 없습니다. 그러나 이러한 두 인덱스는 독립적으로 쿼리할 수 있습니다. 자세한 내용은 [의미 체계 검색을 사용하여 문서의 키 구 찾기](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) 및 [의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)를 참조하세요.  
  
-   의미 체계 인덱스의 LCID를 명시적으로 지정하지 않으면 기본 언어와 관련 언어의 통계만 의미 체계 인덱싱에 사용됩니다.  
  
-   언어 모델을 사용할 수 없는 열에 대해 언어를 지정하면 인덱스 만들기가 실패하고 오류 메시지가 반환됩니다.  
  
##  <a name="HowToEnableCreate"></a> 전체 텍스트 인덱스가 없을 때 의미 체계 인덱스 만들기  
 **CREATE FULLTEXT INDEX** 문을 사용하여 새 전체 텍스트 인덱스를 만들 때 열 정의의 일부로 **STATISTICAL_SEMANTICS** 키워드를 지정하여 열 수준에서 의미 체계 인덱싱을 사용하도록 설정할 수 있습니다. 전체 텍스트 인덱싱 마법사를 사용하여 새 전체 텍스트 인덱스를 만들 때 의미 체계 인덱싱을 사용하도록 설정할 수도 있습니다.  
  
 ### <a name="create-a-new-semantic-index-by-using-transact-sql"></a>Transact-SQL을 사용하여 새 의미 체계 인덱스 만들기  
 
 **CREATE FULLTEXT INDEX** 문을 호출하고 의미 체계 인덱스를 만들 각 열에 대해 **STATISTICAL_SEMANTICS**를 지정합니다. 이 문의 모든 옵션에 대한 자세한 내용은 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)를 참조하세요.  
  
 **예제 1: 고유 인덱스, 전체 텍스트 인덱스 및 의미 체계 인덱스 만들기**  
  
 다음 예에서는 기본 전체 텍스트 카탈로그 **ft**를 만들고, AdventureWorks2012 예제 데이터베이스의 **HumanResources.JobCandidate** 테이블에 있는 **JobCandidateID** 열에 대해 고유 인덱스를 만듭니다. 이 고유 인덱스는 전체 텍스트 인덱스에 대한 키 열로 필요합니다. 그런 다음 **Resume** 열에 대한 전체 텍스트 인덱스와 의미 체계 인덱스를 만듭니다.  
  
```sql  
CREATE FULLTEXT CATALOG ft AS DEFAULT  
GO  
  
CREATE UNIQUE INDEX ui_ukJobCand  
    ON HumanResources.JobCandidate(JobCandidateID)  
GO  
  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate  
    (Resume  
        Language 1033  
        Statistical_Semantics  
    )   
    KEY INDEX JobCandidateID   
    WITH STOPLIST = SYSTEM  
GO  
```  
  
 **예제 2: 여러 열에 대한 전체 텍스트 및 의미 체계 인덱스 만들고 나중에 인덱스 채우기 수행**  
  
 다음 예에서는 AdventureWorks2012 예제 데이터베이스에 전체 텍스트 카탈로그인 **documents_catalog**를 만듭니다. 그런 다음 이 새 카탈로그를 사용하는 전체 텍스트 인덱스를 만듭니다. 전체 텍스트 인덱스는 **Production.Document**테이블의 **Title**, **DocumentSummary** 및 **Document** 열에 만들어지는 반면 의미 체계 인덱스는 **Document** 열에만 만들어집니다. 이 전체 텍스트 인덱스는 새로 만든 전체 텍스트 카탈로그와 기존 고유 키 인덱스 **PK_Document_DocumentID**를 사용합니다. 권장한 대로 이 인덱스 키는 정수 열 **DocumentID**에 만들어집니다. 이 예에서는 열의 데이터 언어인 영어의 LCID 1033을 지정합니다.  
  
 또한 이 예에서는 채우기 작업을 수행하지 않고 변경 내용 추적이 해제되도록 지정합니다. 나중에 사용률이 낮은 시간에 **ALTER FULLTEXT INDEX** 문을 사용하여 새 인덱스에 대해 전체 채우기를 시작하고 변경 내용 자동 추적을 사용하도록 설정합니다.  
  
```sql  
CREATE FULLTEXT CATALOG documents_catalog  
GO  
  
CREATE FULLTEXT INDEX ON Production.Document  
    (   
    Title  
        Language 1033,   
    DocumentSummary  
        Language 1033,   
    Document   
        TYPE COLUMN FileExtension  
        Language 1033  
        Statistical_Semantics  
    )  
    KEY INDEX PK_Document_DocumentID  
        ON documents_catalog  
        WITH CHANGE_TRACKING OFF, NO POPULATION  
GO  
```  
  
 다음과 같이 나중에 사용률이 낮은 시간에 인덱스가 채워집니다.  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO  
GO  
```  
  
### <a name="create-a-new-semantic-index-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 새 의미 체계 인덱스 만들기  
 전체 텍스트 인덱싱 마법사를 실행하고 **테이블 열 선택** 페이지에서 의미 체계 인덱스를 만들 각 열에 대해 **통계 의미 체계** 를 사용하도록 설정합니다. 전체 텍스트 인덱싱 마법사를 시작하는 방법을 비롯한 자세한 내용은 [전체 텍스트 인덱싱 마법사 사용](../../relational-databases/search/use-the-full-text-indexing-wizard.md)을 참조하세요.  
  
##  <a name="HowToEnableAlter"></a> 기존 전체 텍스트 인덱스가 있을 때 의미 체계 인덱스 만들기  
 **ALTER FULLTEXT INDEX** 문을 사용하여 기존 전체 텍스트 인덱스를 변경할 때 의미 체계 인덱싱을 추가할 수 있습니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다양한 대화 상자를 사용하여 의미 체계 인덱싱을 추가할 수 있습니다.  
  
### <a name="add-a-semantic-index-by-using-transact-sql"></a>Transact-SQL을 사용하여 의미 체계 인덱스 추가  
 의미 체계 인덱스를 추가할 각 열에 대해 아래에서 설명하는 옵션을 사용하여 **ALTER FULLTEXT INDEX** 문을 호출합니다. 이 문의 모든 옵션에 대한 자세한 내용은 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)를 참조하세요.  
  
 별도로 지정하지 않는 한 **ALTER**를 호출하면 전체 텍스트 인덱스와 의미 체계 인덱스가 모두 다시 채워집니다.  
  
-   열에 전체 텍스트 인덱싱만 추가하려면 **ADD** 구문을 사용합니다.  
  
-   열에 전체 텍스트 및 의미 체계 인덱싱을 모두 추가하려면 **ADD** 구문과 함께 **STATISTICAL_SEMANTICS** 옵션을 사용합니다.  
  
-   이미 전체 텍스트 인덱싱을 사용하도록 설정된 열에 의미 체계 인덱싱을 추가하려면 **ADD STATISTICAL_SEMANTICS** 옵션을 사용합니다. 단일 **ALTER** 문에서는 하나의 열에만 의미 체계 인덱싱을 추가할 수 있습니다.  
  
 **예제: 전체 텍스트 인덱싱이 이미 있는 열에 의미 체계 인덱싱 추가**  
  
 다음 예에서는 AdventureWorks2012 예제 데이터베이스의 **Production.Document** 테이블에 대한 기존 전체 텍스트 인덱스를 변경합니다. 이 예에서는 전체 텍스트 인덱스가 이미 있는 **Production.Document** 테이블의 **Document** 열에 의미 체계 인덱스를 추가합니다. 또한 자동으로 다시 채워지지 않는 인덱스를 지정합니다.  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document  
    ALTER COLUMN Document  
        ADD Statistical_Semantics  
    WITH NO POPULATION  
GO  
```  
  
### <a name="add-a-semantic-index-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 의미 체계 인덱스 추가  
 **전체 텍스트 인덱스 속성** 대화 상자의 **전체 텍스트 인덱스 열** 페이지에서 의미 체계 및 전체 텍스트 인덱싱을 사용하도록 설정된 열을 변경할 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 관리](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1)를 참조하세요.  

## <a name="alter-a-semantic-index"></a>의미 체계 인덱스 변경
  
###  <a name="addreq"></a> 기존 인덱스 변경을 위한 요구 사항 및 제한 사항  
  
-   인덱스 채우기가 진행 중인 동안에는 기존 인덱스를 변경할 수 없습니다. 인덱스 채우기의 진행률을 모니터링하는 방법은 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)을 참조하세요.  
  
-   **ALTER FULLTEXT INDEX** 문을 한 번 호출하는 것으로 열에 인덱싱을 추가하고 동일한 열의 인덱싱을 변경하거나 삭제할 수는 없습니다.  
  
##  <a name="dropping"></a> 의미 체계 인덱스 삭제  
**ALTER FULLTEXT INDEX** 문을 사용하여 기존 전체 텍스트 인덱스를 변경할 때 의미 체계 인덱싱을 삭제할 수 있습니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다양한 대화 상자를 사용하여 의미 체계 인덱싱을 삭제할 수 있습니다.  
  
 ### <a name="drop-a-semantic-index-by-using-transact-sql"></a>Transact-SQL을 사용하여 의미 체계 인덱스 삭제  
열에서 의미 체계 인덱싱만 삭제하려면 **ALTER COLUMN***column_name***DROP STATISTICAL_SEMANTICS** 옵션을 사용하여 **ALTER FULLTEXT INDEX** 문을 호출합니다. 단일 **ALTER** 문으로 여러 열의 인덱싱을 삭제할 수도 있습니다.  
  
```sql  
USE database_name  
GO  

ALTER FULLTEXT INDEX  
    ALTER COLUMN column_name  
    DROP STATISTICAL_SEMANTICS  
GO  
```  
  
열에서 전체 텍스트 인덱스와 의미 체계 인덱싱을 모두 삭제하려면 **ALTER COLUMN***column_name***DROP** 옵션을 사용하여 **ALTER FULLTEXT INDEX** 문을 호출합니다.  
  
```sql  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX  
    ALTER COLUMN column_name  
    DROP  
GO  
```  
  
 ### <a name="drop-a-semantic-index-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 의미 체계 인덱스 삭제  
 **전체 텍스트 인덱스 속성** 대화 상자의 **전체 텍스트 인덱스 열** 페이지에서 의미 체계 및 전체 텍스트 인덱싱을 사용하도록 설정된 열을 변경할 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 관리](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1)를 참조하세요.  
  
###  <a name="dropreq"></a> Requirements and restrictions for dropping a semantic index  
  
-   의미 체계 인덱싱을 유지하는 동안에는 열에서 전체 텍스트 인덱싱을 삭제할 수 없습니다. 의미 체계 인덱싱에서는 전체 텍스트 인덱싱에 의존하여 문서 유사성 결과를 얻습니다.  
  
-   테이블에서 의미 체계 인덱싱을 사용하도록 설정된 마지막 열의 의미 체계 인덱싱을 삭제할 경우 **NO POPULATION** 옵션을 지정할 수 없습니다. 이전에 인덱싱된 결과를 제거하려면 채우기 주기가 필요합니다.  
  
## <a name="check-whether-semantic-search-is-enabled-on-database-objects"></a>데이터베이스 개체에 의미 체계 검색이 사용하도록 설정되어 있는지 확인  
### <a name="is-semantic-search-enabled-for-a-database"></a>데이터베이스에 대해 의미 체계 검색이 사용하도록 설정되어 있는지 확인
  
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) 메타데이터 함수의 **IsFullTextEnabled** 속성을 쿼리합니다.  
  
 반환 값이 1이면 데이터베이스에 대해 전체 텍스트 검색과 의미 체계 검색이 사용하도록 설정되어 있음을 나타내고, 반환 값이 0이면 그렇지 않음을 나타냅니다.  
  
```sql  
SELECT DATABASEPROPERTYEX('database_name', 'IsFullTextEnabled')  
GO  
```  
  
### <a name="is-semantic-search-enabled-for-a-table"></a>테이블에 대해 의미 체계 검색이 사용하도록 설정되어 있는지 확인  
 
 [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md) 메타데이터 함수의 **TableFullTextSemanticExtraction** 속성을 쿼리합니다.  
  
 반환 값이 1이면 테이블에 대해 의미 체계 검색이 사용하도록 설정되어 있음을 나타내고, 반환 값이 0이면 그렇지 않음을 나타냅니다.  
  
```scr  
SELECT OBJECTPROPERTYEX(OBJECT_ID('table_name'), 'TableFullTextSemanticExtraction')  
GO  
```  
  
 ### <a name="is-semantic-search-enabled-for-a-column"></a>열에 대해 의미 체계 검색이 사용하도록 설정되어 있는지 확인
   
 특정 열에 대해 의미 체계 검색이 사용하도록 설정되어 있는지 확인하려면  
  
-   [COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md) 메타데이터 함수의 **StatisticalSemantics** 속성을 쿼리합니다.  
  
     반환 값이 1이면 열에 대해 의미 체계 검색이 사용하도록 설정되어 있음을 나타내고, 반환 값이 0이면 그렇지 않음을 나타냅니다.  
  
    ```sql  
    SELECT COLUMNPROPERTY(OBJECT_ID('table_name'), 'column_name', 'StatisticalSemantics')  
    GO  
    ```  
  
-   전체 텍스트 인덱스에 대한 카탈로그 뷰 [sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)를 쿼리합니다.  
  
     **statistical_semantics** 열의 값이 1이면 지정된 열에 전체 텍스트 인덱싱과 의미 체계 인덱싱이 사용하도록 설정되어 있음을 나타냅니다.  
  
    ```sql  
    SELECT * FROM sys.fulltext_index_columns WHERE object_id = OBJECT_ID('table_name')  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 개체 탐색기에서 열을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **열 속성** 대화 상자의 **일반** 페이지에서 **통계 의미 체계** 속성 값을 확인합니다.  
  
     값이 True이면 지정된 열에 전체 텍스트 인덱싱과 의미 체계 인덱싱이 사용하도록 설정되어 있음을 나타냅니다.  
  
## <a name="determine-what-can-be-indexed-for-semantic-search"></a>의미 체계 검색을 위해 인덱싱할 수 있는 항목 결정  
  
###  <a name="HowToCheckLanguages"></a> 의미 체계 검색에 지원되는 언어 확인  
  
> [!IMPORTANT]  
>  의미 체계 인덱싱에 지원되는 언어는 전체 텍스트 인덱싱에 지원되는 언어보다 적습니다. 따라서 전체 텍스트 검색을 위해 인덱싱할 수 있지만 의미 체계 검색을 위해서는 인덱싱할 수 없는 열이 있을 수 있습니다.  
  
 카탈로그 뷰 [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)를 쿼리합니다.  
  
```sql  
SELECT * FROM sys.fulltext_semantic_languages  
GO  
```  
  
 의미 체계 인덱싱에 지원되는 언어는 다음과 같습니다. 이 목록은 LCID로 정렬된 카탈로그 뷰 [sys.fulltext_semantic_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)의 출력을 보여 줍니다.  
  
|언어|LCID|  
|--------------|----------|  
|독일어|1031|  
|영어(미국)|1033|  
|프랑스어|1036|  
|이탈리아어|1040|  
|포르투갈어(브라질)|1046|  
|러시아어|1049|  
|스웨덴어|1053|  
|영어(영국)|2057|  
|포르투갈어(포르투갈)|2070|  
|스페인어|3082|  
  
###  <a name="doctypes"></a> 인덱싱할 수 있는 문서 유형 결정  
 카탈로그 뷰 [sys.fulltext_document_types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)를 쿼리합니다.  
  
 인덱싱할 문서 형식이 지원되는 형식 목록에 없는 경우 추가 필터를 찾은 다음 다운로드하여 설치해야 할 수 있습니다. 자세한 내용은 [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)을 참조하세요.  
  
##  <a name="BestPracticeFilegroup"></a> Best practice: Consider creating a separate filegroup for the full-text and semantic indexes  
 디스크 공간 할당이 중요한 경우 전체 텍스트 및 의미 체계 인덱스에 대한 별도의 파일 그룹을 만드는 것이 좋습니다. 의미 체계 인덱스는 전체 텍스트 인덱스와 동일한 파일 그룹에 만들어집니다. 완전히 채워진 의미 체계 인덱스에는 많은 양의 데이터가 포함될 수 있습니다.  
 
##  <a name="IssueNoResults"></a> 문제: 특정 열에 대해 검색할 때 결과가 반환되지 않음  
 **유니코드 언어에 대해 비유니코드 LCID가 지정되었습니까?**  
 비유니코드 열에 대해 의미 체계 인덱싱을 사용하도록 설정할 때 러시아어의 LCID 1049와 같이 유니코드 단어만 있는 언어의 LCID를 사용할 수 있습니다. 그러나 이 경우에는 이 열에 대한 의미 체계 인덱스에서 결과가 반환되지 않습니다.  
  
  
