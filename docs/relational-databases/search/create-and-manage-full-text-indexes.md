---
title: 전체 텍스트 인덱스 만들기 및 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d51f0b31729d6b061c7e8cfd82b5047796c6daa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758074"
---
# <a name="create-and-manage-full-text-indexes"></a>전체 텍스트 인덱스 만들기 및 관리
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
이 항목에서는 SQL Server에서 전체 텍스트 인덱스를 만들고, 채우고, 관리하는 방법을 설명합니다.
  
## <a name="prerequisite---create-a-full-text-catalog"></a>필수 조건 - 전체 텍스트 카탈로그 만들기
전체 텍스트 인덱스를 만들려면 먼저 전체 텍스트 카탈로그가 있어야 합니다. 카탈로그는 하나 이상의 전체 텍스트 인덱스에 대한 가상 컨테이너입니다. 자세한 내용은 [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)를 참조하세요.
  
##  <a name="create-alter-or-drop-a-full-text-index"></a><a name="tasks"></a> 전체 텍스트 인덱스 만들기, 변경 또는 삭제  
### <a name="create-a-full-text-index"></a>전체 텍스트 인덱스 만들기  
  
-   [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
### <a name="alter-a-full-text-index"></a>전체 텍스트 인덱스 변경
  
-   [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
### <a name="drop-a-full-text-index"></a>전체 텍스트 인덱스 삭제 
  
-   [DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)

## <a name="populate-a-full-text-index"></a>전체 텍스트 인덱스 채우기
전체 텍스트 인덱스를 만들고 유지 관리하는 과정을 *채우기* (또는 *탐색*)라고 합니다. 전체 텍스트 인덱스 채우기에는
-   전체 채우기
-   변경 내용 추적 기반 채우기
-   타임스탬프 기반 증분 채우기의 세 가지 유형이 있습니다.

자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.

##  <a name="view-the-properties-of-a-full-text-index"></a><a name="view"></a> 전체 텍스트 인덱스의 속성 보기
### <a name="view-the-properties-of-a-full-text-index-with-transact-sql"></a>Transact-SQL을 사용하여 전체 텍스트 인덱스의 속성 보기

|카탈로그 뷰 또는 동적 관리 뷰|Description|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|전체 텍스트 인덱스 참조에 대한 각 전체 텍스트 카탈로그에 대해 행을 반환합니다.|  
|[sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|전체 텍스트 인덱스의 일부인 각 열에 대한 행을 포함합니다.|  
|[sys.fulltext_index_fragments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|전체 텍스트 인덱스는 전체 텍스트 인덱스 조각이라고 하는 내부 테이블을 사용하여 반전된 인덱스 데이터를 저장합니다. 이 뷰를 사용하면 이러한 조각에 대한 메타데이터를 쿼리할 수 있습니다. 이 뷰에는 전체 텍스트 인덱스를 포함하는 모든 테이블의 각 전체 인덱스 조각에 대한 행이 들어 있습니다.|  
|[sys.fulltext_indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|테이블 형식 개체의 각 전체 텍스트 인덱스당 한 개의 행을 포함합니다.|  
|[sys.dm_fts_index_keywords&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|지정된 테이블에 대한 전체 텍스트 인덱스 내용에 관한 정보를 반환합니다.|  
|[sys.dm_fts_index_keywords_by_document&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|지정된 테이블에 대한 전체 텍스트 인덱스의 문서 수준 내용에 관한 정보를 반환합니다. 지정된 키워드는 여러 문서에 나타날 수 있습니다.|  
|[sys.dm_fts_index_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|현재 진행 중인 전체 텍스트 인덱스 채우기에 대한 정보를 반환합니다.|  
 
### <a name="view-the-properties-of-a-full-text-index-with-management-studio"></a>Management Studio를 사용하여 전체 텍스트 인덱스의 속성 보기 
1.  Management Studio의 개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 전체 텍스트 인덱스가 포함된 데이터베이스를 확장합니다.  
  
3.  **테이블**을 확장합니다.  
  
4.  전체 텍스트 인덱스가 정의된 테이블을 마우스 오른쪽 단추로 클릭하고 **전체 텍스트 인덱스**를 선택한 다음 **전체 텍스트 인덱스** 상황에 맞는 메뉴에서 **속성**을 클릭합니다. 그러면 **전체 텍스트 인덱스 속성** 대화 상자가 열립니다.  
  
5.  **페이지 선택** 창에서 다음 페이지 중 하나를 선택할 수 있습니다.  
  
    |호출|Description|  
    |----------|-----------------|  
    |**일반**|전체 텍스트 인덱스의 기본 속성을 표시합니다. 이러한 속성으로는 데이터베이스 이름, 테이블 이름 및 전체 텍스트 키 열의 이름과 같이 변경할 수 없는 많은 속성과 여러 가지 수정 가능한 속성이 있습니다. 수정 가능한 속성은 다음과 같습니다.<br /><br /> **전체 텍스트 인덱스 중지 목록**<br /><br /> **전체 텍스트 인덱싱 설정**<br /><br /> **변경 내용 추적**<br /><br /> **검색 속성 목록**|  
    |**열**|전체 텍스트 인덱싱에 사용할 수 있는 테이블 열을 표시합니다. 열을 선택하면 선택한 열이 전체 텍스트 인덱싱됩니다. 이때 전체 텍스트 인덱스에 포함하려는 만큼 사용 가능한 열을 선택할 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](populate-full-text-indexes.md)를 참조하세요.|
    |**일정**|이 페이지를 사용하여 전체 텍스트 인덱스 채우기에 대한 증분 테이블 채우기를 시작하는 SQL Server 에이전트 작업의 일정을 만들거나 관리할 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.<br /><br /> 참고: **전체 텍스트 인덱스 속성** 대화 상자를 닫으면 새로 만든 일정이 SQL Server 에이전트 작업에 연결됩니다(*database_name*.*table_name*에 대한 증분 테이블 채우기 시작).|  
  
6.  변경 내용을 저장하고 **전체 텍스트 인덱스 속성** 대화 상자를 닫으려면 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="view-the-properties-of-indexed-tables-and-columns"></a><a name="props"></a> 인덱싱된 테이블 및 열 속성 보기  
 OBJECTPROPERTYEX와 같은 여러 가지 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하여 다양한 전체 텍스트 인덱싱 속성 값을 얻을 수 있습니다. 이 정보는 전체 텍스트 검색을 관리하고 이러한 검색에서 발생하는 문제를 해결하는 데 유용합니다.  
  
 다음 표에서는 인덱싱된 테이블 및 열과 관련한 전체 텍스트 속성과 관련 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 보여 줍니다.  
  
|속성|Description|함수|  
|--------------|-----------------|--------------|  
|**FullTextTypeColumn**|열의 문서 유형 정보를 보관하는 테이블의 TYPE COLUMN입니다.|[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)|  
|**IsFulltextIndexed**|열에 대한 전체 텍스트 인덱싱 설정 여부를 나타냅니다.|COLUMNPROPERTY|  
|**IsFulltextKey**|인덱스가 테이블에 대한 전체 텍스트 키인지를 나타냅니다.|[INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md)|  
|**TableFulltextBackgroundUpdateIndexOn**|테이블에 대한 전체 텍스트 백그라운드 업데이트 인덱싱 설정 여부를 나타냅니다.|[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)|  
|**TableFulltextCatalogId**|테이블에 대한 전체 텍스트 인덱스 데이터가 상주하는 전체 텍스트 카탈로그 ID입니다.|OBJECTPROPERTYEX|  
|**TableFulltextChangeTrackingOn**|테이블에 전체 텍스트 변경 내용 추적이 설정되어 있는지를 나타냅니다.|OBJECTPROPERTYEX|  
|**TableFulltextDocsProcessed**|전체 텍스트 인덱싱이 시작된 이후에 처리된 행의 수입니다.|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|전체 텍스트 검색이 인덱싱하지 않은 행의 수입니다.|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|성공적으로 전체 텍스트 인덱싱된 행의 수입니다.|OBJECTPROPERTYEX|  
|**TableFulltextKeyColumn**|전체 텍스트 고유 키 열의 열 ID입니다.|OBJECTPROPERTYEX|  
|**TableFullTextMergeStatus**|전체 텍스트 인덱스가 있는 테이블이 현재 병합 중인지를 나타냅니다.|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|처리할 보류 중인 변경 내용 추적 항목의 수입니다.|OBJECTPROPERTYEX|  
|**TableFulltextPopulateStatus**|전체 텍스트 테이블의 채우기 상태입니다.|OBJECTPROPERTYEX|  
|**TableHasActiveFulltextIndex**|테이블에 활성화된 전체 텍스트 인덱스가 있는지를 나타냅니다.|OBJECTPROPERTYEX|  
  
##  <a name="get-info-about-the-full-text-key-column"></a><a name="key"></a> 전체 텍스트 키 열에 대한 정보 얻기  
 일반적으로 CONTAINSTABLE 또는 FREETEXTTABLE 행 집합 반환 함수의 결과는 기본 테이블과 조인되어야 합니다. 이러한 경우 고유 키 열 이름을 알아야 합니다. 그러면 지정된 고유 인덱스가 전체 텍스트 키로 사용되는지 여부를 확인하고 전체 텍스트 키 열의 식별자를 가져올 수 있습니다.  
  
### <a name="determine-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>지정된 고유 인덱스가 전체 텍스트 키 열로 사용되는지 여부 확인  
  
[SELECT](../../t-sql/queries/select-transact-sql.md) 문을 사용하여 [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) 함수를 호출합니다. 함수 호출 시 다음과 같이 OBJECT_ID 함수를 사용하여 테이블 이름(*table_name*)을 테이블 ID로 변환하고 테이블의 고유 인덱스 이름을 지정한 다음 **IsFulltextKey** 인덱스 속성을 지정합니다.  
  
```sql  
SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
```  
  
 이 문은 전체 텍스트 키 열의 고유성을 강제 적용하기 위해 인덱스가 사용되면 1을 반환하고, 그렇지 않으면 0을 반환합니다.  
  
 **예제**  
  
 다음 예에서는 `PK_Document_DocumentNode` 인덱스가 전체 텍스트 키 열의 고유성을 강제 적용하는 데 사용되는지 여부를 확인합니다.  
  
```sql  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentNode',  'IsFulltextKey' )  
```  
  
 이 예에서는 전체 텍스트 키 열의 고유성을 강제 적용하기 위해 `PK_Document_DocumentNode` 인덱스가 사용되면 1을 반환하고, 그렇지 않으면 0 또는 NULL을 반환합니다. NULL은 잘못된 인덱스 이름이 사용 중이거나, 인덱스 이름이 테이블과 일치하지 않거나, 테이블이 존재하지 않음 등을 의미합니다.  
  
### <a name="find-the-identifier-of-the-full-text-key-column"></a>전체 텍스트 키 열의 식별자 찾기  
  
전체 텍스트를 사용하도록 설정된 테이블에는 해당 테이블에 고유 행을 강제 적용하는 데 사용되는 열(*고유**키 열*)이 있습니다. OBJECTPROPERTYEX 함수에서 얻을 수 있는 **TableFulltextKeyColumn** 속성에는 고유 키 열의 열 ID가 포함됩니다.  
 
이 식별자를 가져오려면 SELECT 문을 사용하여 OBJECTPROPERTYEX 함수를 호출하면 됩니다. 다음과 같이 OBJECT_ID 함수를 사용하여 테이블 이름(*table_name*)을 테이블 ID로 변환하고 **TableFulltextKeyColumn** 속성을 지정합니다.  
  
```sql  
SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
```  
  
 **예**  
  
 다음 예에서는 전체 텍스트 키 열의 식별자나 NULL을 반환합니다. NULL은 잘못된 인덱스 이름이 사용 중이거나, 인덱스 이름이 테이블과 일치하지 않거나, 테이블이 존재하지 않음 등을 의미합니다.  
  
```sql
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 다음 예에서는 고유 키 열의 식별자를 사용하여 열의 이름을 가져오는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 이 예에서는 Document 테이블의 고유 키 열 이름인 DocumentNode가 포함된 단일 행을 표시하는 `Unique Key Column`이라는 결과 집합 열을 반환합니다. 이 쿼리에 잘못된 인덱스 이름이 포함되어 있거나, 인덱스 이름이 테이블과 일치하지 않거나, 테이블이 존재하지 않는 경우에는 NULL이 반환됩니다.  

## <a name="index-varbinarymax-and-xml-columns"></a>varbinary(max) 및 xml 열 인덱싱  
 **varbinary(max)** , **varbinary**또는 **xml** 열이 전체 텍스트 인덱싱된 경우 다른 전체 텍스트 인덱싱된 열과 마찬가지로 전체 텍스트 조건자(CONTAINS 및 FREETEXT) 및 함수(CONTAINSTABLE 및 FREETEXTTABLE)를 사용하여 이러한 열을 쿼리할 수 있습니다.
   
### <a name="index-varbinarymax-or-varbinary-data"></a>varbinary(max) 또는 varbinary 데이터 인덱싱  
 단일 **varbinary(max)** 또는 **varbinary** 열에 많은 문서 유형을 저장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 필터가 설치되어 있고 운영 체제에서 사용할 수 있는 문서 유형을 지원합니다. 각 문서의 문서 유형은 문서의 파일 확장명으로 식별됩니다. 예를 들어 .doc 파일 확장명의 경우 전체 텍스트 검색은 Microsoft Word 문서를 지원하는 필터를 사용합니다. 사용 가능한 문서 유형의 목록을 보려면 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) 카탈로그 뷰를 쿼리하세요.  
  
전체 텍스트 엔진은 운영 체제에 설치된 기존 필터를 활용할 수 있습니다. 운영 체제 필터, 단어 분리기, 형태소 분석기를 사용하려면 먼저 다음과 같이 서버 인스턴스에 로드해야 합니다.  
  
```sql  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
**varbinary(max)** 열에 대한 전체 텍스트 인덱스를 만들려면 전체 텍스트 엔진이 **varbinary(max)** 열에 있는 문서의 파일 확장명에 액세스해야 합니다. 이 정보는 전체 텍스트 인덱스의 **varbinary(max)** 열에 연결해야 하는 테이블 열, 즉 유형 열에 저장되어야 합니다. 문서를 인덱싱할 때 전체 텍스트 엔진은 유형 열의 파일 확장명을 사용하여 사용할 필터를 식별합니다.  
   
### <a name="index-xml-data"></a>인덱스 xml 데이터  
 **xml** 데이터 형식 열에는 XML 문서만 저장되고 이러한 문서에는 XML 필터만 사용됩니다. 따라서 유형 열은 필요하지 않습니다. **xml** 열에서 전체 텍스트 인덱스는 XML 요소의 내용은 인덱싱하지만 XML 태그는 무시합니다. 특성 값은 숫자 값이 아니면 전체 텍스트 인덱싱됩니다. 요소 태그는 토큰 경계로 사용됩니다. 여러 언어를 포함하는 올바른 형식의 XML 또는 HTML 문서와 조각이 지원됩니다.  
  
 **xml** 열을 인덱싱 및 쿼리하는 방법에 대한 자세한 내용은 [XML 열에 전체 텍스트 검색 사용](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)을 참조하세요.  
  
##  <a name="disable-or-re-enable-full-text-indexing-for-a-table"></a><a name="disable"></a> 테이블에 대해 전체 텍스트 인덱싱 사용 안 함 또는 다시 사용   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 사용자가 만든 모든 데이터베이스에서 기본적으로 전체 텍스트를 사용할 수 있습니다. 또한 개별 테이블에 전체 텍스트 인덱스를 만들고 이 인덱스에 열을 추가하는 즉시 자동으로 개별 테이블에서 전체 텍스트 인덱싱을 사용할 수 있게 됩니다. 해당 전체 텍스트 인덱스에서 마지막 열을 삭제하면 자동으로 테이블에서 전체 텍스트 인덱싱을 사용할 수 없게 됩니다.  
  
 전체 텍스트 인덱스가 있는 테이블에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블에서의 전체 텍스트 인덱싱을 수동으로 해제하거나 다시 설정할 수 있습니다.  

1.  서버 그룹, **데이터베이스**를 차례로 확장한 다음 전체 텍스트 인덱싱을 설정할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블**을 확장하고 전체 텍스트 인덱싱을 해제하거나 다시 설정할 테이블을 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **전체 텍스트 인덱스**를 선택한 다음 **전체 텍스트 인덱스 사용 안 함** 또는 **전체 텍스트 인덱스 사용**을 클릭합니다.  
  
##  <a name="remove-a-full-text-index-from-a-table"></a><a name="remove"></a> 테이블에서 전체 텍스트 인덱스 제거  
  
1.  개체 탐색기에서 삭제할 전체 텍스트 인덱스가 포함된 테이블을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  **전체 텍스트 인덱스 삭제**를 선택합니다.  
  
3.  전체 텍스트 인덱스를 삭제할 것인지 확인하는 메시지가 표시되면 **확인** 을 클릭합니다.  
  
  
