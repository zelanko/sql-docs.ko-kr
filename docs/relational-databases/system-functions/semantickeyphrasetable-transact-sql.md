---
title: semantickeyphrasetable (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b033342e8e6e7d3fb55d51d03705b2168d72209f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785331"
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 테이블의 지정된 열과 연관된 키 구에 대한 0개 이상의 행으로 구성된 테이블을 반환합니다.  
  
 SELECT 문의 FROM 절에서 이 행 집합 함수를 일반 테이블 이름과 마찬가지로 참조할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
    )  
```  
  
##  <a name="Arguments"></a> 인수  
 **table**  
 전체 텍스트 및 의미 체계 인덱싱을 사용하도록 설정된 테이블의 이름입니다.  
  
 이 이름은 1~4개의 부분으로 구성된 이름일 수 있지만 원격 서버 이름은 사용할 수 없습니다.  
  
 **column**  
 결과가 반환될 인덱싱된 열의 이름입니다. 열에 의미 체계 인덱싱이 사용하도록 설정되어 있어야 합니다.  
  
 **column_list**  
 쉼표로 구분되고 괄호로 묶인 여러 열을 나타냅니다. 모든 열에 의미 체계 인덱싱이 사용하도록 설정되어 있어야 합니다.  
  
 **\***  
 의미 체계 인덱싱이 사용하도록 설정된 모든 열이 포함되어 있음을 나타냅니다.  
  
 **source_key**  
 특정 행에 대한 결과를 요청할 행의 고유 키입니다.  
  
 이 키는 가능한 경우 원본 테이블의 전체 텍스트 고유 키와 같은 형식으로 암시적으로 변환됩니다. 상수나 변수로 키를 지정할 수 있지만 식 또는 스칼라 하위 쿼리의 결과를 키로 지정할 수는 없습니다. source_key를 생략하면 모든 행에 대한 결과가 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 다음 표에서는 이 행 집합 함수가 반환하는 키 구에 대해 설명합니다.  
  
|Column_name|형식|Description|  
|------------------|----------|-----------------|  
|**column_id**|**int**|현재 키 구가 추출되고 인덱싱된 원본 열의 ID입니다.<br /><br /> column_id에서 열 이름을 검색하거나 열 이름에서 column_id를 검색하는 방법에 대한 자세한 내용은 COL_NAME 및 COLUMNPROPERTY 함수를 참조하십시오.|  
|**document_key**|**\***<br /><br /> 이 키는 원본 테이블의 고유 키 유형과 일치합니다.|현재 키 구가 인덱싱된 문서 또는 행의 고유 키 값입니다.|  
|**keyphrase**|**NVARCHAR**|column_id로 식별되는 열에 있고 document_key에 지정된 문서와 연관된 키 구입니다.|  
|**score**|**REAL**|동일한 문서의 인덱싱된 열에 있는 다른 모든 키 구를 기준으로 한 이 키 구의 상대적 값입니다.<br /><br /> 이 값은 [0.0, 1.0] 범위의 소수 10진수 값입니다. 점수가 높을수록 유사성이 높으며 1.0이 최대 점수입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색을 사용 하 여 문서의 키 구 찾기](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)합니다.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 키 구 추출 및 채우기에 대한 정보와 상태를 보려면 다음 동적 관리 뷰를 쿼리합니다.  
  
-   [sys.dm_db_fts_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 전체 텍스트 및 의미 체계 인덱스를 만든 기본 테이블에 대한 SELECT 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
###  <a name="HowToTopPhrases"></a> 예제 1: 특정 문서에서 상위 키 구 찾기  
 다음 예제에서는 AdventureWorks 예제 데이터베이스에 있는 Production.Document 테이블의 Document 열에서 @DocumentId 변수를 통해 지정된 문서에서 상위 10개의 키 구를 검색합니다. @DocumentId 변수는 전체 텍스트 인덱스의 키 열에 있는 값을 나타냅니다. **SEMANTICKEYPHRASETABLE** 함수는 테이블 검색 대신 인덱스 검색을 사용하여 이러한 결과를 효율적으로 검색합니다. 이 예에서는 열이 전체 텍스트 및 의미 체계 인덱싱에 대해 구성되어 있는 것으로 가정합니다.  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="HowToTopDocuments"></a> 예제 2: 특정 키 구가 포함 된 상위 문서 찾기  
 다음 예에서는 AdventureWorks 예제 데이터베이스에 있는 Production.Document 테이블의 Document 열에서 “Bracket” 키 구가 포함된 상위 25개의 문서를 검색합니다. 이 예에서는 열이 전체 텍스트 및 의미 체계 인덱싱에 대해 구성되어 있는 것으로 가정합니다.  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
  
```  
  
  
