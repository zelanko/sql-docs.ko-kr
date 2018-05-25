---
title: sys.dm_fts_parser (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_parser_TSQL
- dm_fts_parser
- dm_fts_parser_TSQL
- sys.dm_fts_parser
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_parser dynamic management function
- troubleshooting [SQL Server], full-text search
ms.assetid: 2736d376-fb9d-4b28-93ef-472b7a27623a
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 717e97ca38fdc68b0ba807f546a253793234375b
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmftsparser-transact-sql"></a>sys.dm_fts_parser(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  적용 한 후 최종 토큰화 결과 반환 된 주어진 [단어 분리기](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md), [동의어 사전](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md), 및 [중지 목록](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) 쿼리 문자열 입력을 조합 합니다. 토큰화 결과는 지정된 쿼리 문자열에 대한 전체 텍스트 엔진의 출력과 같습니다.  
  
 sys.dm_fts_parser는 동적 관리 함수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_fts_parser('query_string', lcid, stoplist_id, accent_sensitivity)  
```  
  
## <a name="arguments"></a>인수  
 *query_string*  
 구문 분석할 쿼리입니다. *query_string* 하는 문자열 체인 일 수 있습니다 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 구문 지원 합니다. 예를 들어 활용 형태, 동의어 사전 및 논리 연산자를 포함할 수 있습니다.  
  
 *lcid*  
 LCID (로캘 식별자) 구문 분석에 사용할 단어 분리기의 *query_string*합니다.  
  
 *stoplist_id*  
 로 식별 되는 단어 분리기에서 사용할 수 있는 경우 중지 목록의 ID *lcid*합니다. *stoplist_id* 은 **int**합니다. 'NULL'을 지정하면 중지 목록이 사용되지 않으며, 0을 지정하면 시스템 STOPLIST가 사용됩니다.  
  
 중지 목록 ID는 데이터베이스 내에서 고유합니다. 지정 된 테이블 사용에 대 한 전체 텍스트 인덱스에 대 한 중지 목록 ID를 확인 하려면는 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 *accent_sensitivity*  
 전체 텍스트 검색에서 분음 부호를 구분할지 여부를 제어하는 부울 값입니다. *accent_sensitivity* 은 **비트**, 다음 값 중 하나를 사용 합니다.  
  
|Value|악센트 구분 여부|  
|-----------|----------------------------|  
|0|구분 안 함<br /><br /> "Café"와 "café" 같은 단어가 동일 하 게 처리 됩니다.|  
|1.|값<br /><br /> "Café"와 "café" 같은 단어가 다르게 처리 됩니다.|  
  
> [!NOTE]  
>  전체 텍스트 카탈로그에 대 한이 값의 현재 설정을 보려면 다음을 실행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을: `SELECT fulltextcatalogproperty('` *catalog_name*`', 'AccentSensitivity');`합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|키워드(keyword)|**varbinary(128)**|단어 분리기에서 반환된 특정 키워드의 16진수 표현입니다. 이러한 표현은 키워드를 전체 텍스트 인덱스에 저장하는 데 사용됩니다. 이 값은 사람이 읽을 수, 되지 않지만 등의 전체 텍스트 인덱스의 내용을 반환 하는 다른 동적 관리 뷰에 의해 반환 된 출력에 지정 된 키워드와 관련 된에 대 한 유용 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md) 및 [ sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)합니다.<br /><br /> **참고:** OxFF는 파일 또는 데이터 집합의 끝을 나타내는 특수 문자를 나타냅니다.|  
|group_id|**int**|지정된 용어가 생성된 논리 그룹을 차별화하는 데 유용한 정수 값을 포함합니다. 예를 들어 '`Server AND DB OR FORMSOF(THESAURUS, DB)"`'는 다음 group_id 값을 영어로 생성합니다.<br /><br /> 1: 서버<br />2: DB<br />3: DB|  
|phrase_id|**int**|단어 분리기에서 full-text와 같은 복합 단어의 대체 형태가 실행되는 경우를 차별화하는 데 유용한 정수 값을 포함합니다. 경우에 따라 복합 단어('multi-million')가 있으면 단어 분리기에서 대체 형태가 실행되기도 하는데, 이러한 대체 형태(구)는 차별화해야 하는 경우가 있습니다.<br /><br /> 예를 들어 '`multi-million`'은 다음 phrase_id 값을 영어로 생성합니다.<br /><br /> 에 대 한 1 `multi`<br />에 대 한 1 `million`<br />에 대 한 2 `multimillion`|  
|occurrence|**int**|구문 분석 결과에 있는 각 용어의 순서를 나타냅니다. 예를 들어 "`SQL Server query processor`" 구의 경우 occurrence에 이 구의 용어에 대해 다음 occurrence 값이 영어로 포함될 수 있습니다.<br /><br /> 에 대 한 1 `SQL`<br />에 대 한 2 `Server`<br />에 대 한 3 `query`<br />에 대 한 4 `processor`|  
|special_term|**nvarchar(4000)**|단어 분리기에서 실행되는 용어의 특징에 대한 정보를 포함합니다. 예를 들면 다음과 같습니다.<br /><br /> 정확히 일치<br /><br /> 의미 없는 단어<br /><br /> 문장의 끝<br /><br /> 단락의 끝<br /><br /> 장의 끝|  
|display_term|**nvarchar(4000)**|사람이 인식할 수 있는 키워드 형식을 포함합니다. 전체 텍스트 인덱스의 내용에 액세스하도록 디자인된 함수를 사용하기 때문에 표시된 용어가 비정규화 제한으로 인해 원래 용어와 동일하지 않을 수 있지만, 원래 입력에서 식별할 수 있을 만큼은 정확해야 합니다.|  
|expansion_type|**int**|지정된 용어의 확장 특성에 대한 정보를 포함합니다. 예를 들면 다음과 같습니다.<br /><br /> 0 = 단일 단어<br /><br /> 2 = 활용 형태상의 확장<br /><br /> 4 = 동의어 사전 확장/대체<br /><br /> 예를 들어 동의어 사전이 다음과 같이 run을 `jog`의 확장으로 정의하는 경우를 고려해 보십시오.<br /><br /> `<expansion>`<br /><br /> `<sub>run</sub>`<br /><br /> `<sub>jog</sub>`<br /><br /> `</expansion>`<br /><br /> `FORMSOF (FREETEXT, run)` 용어는 다음 출력을 생성합니다.<br /><br /> `run`, expansion_type=0<br /><br /> `runs`, expansion_type=2<br /><br /> `running`, expansion_type=2<br /><br /> `ran`, expansion_type=2<br /><br /> `jog`, expansion_type=4|  
|source_term|**nvarchar(4000)**|지정된 용어가 생성되거나 구문 분석되는 용어 또는 구입니다. 예를 들어 '"`word breakers" AND stemmers'`에 대한 쿼리는 다음 source_term 값을 영어로 생성합니다.<br /><br /> `word breakers` display_term에 대 한`word`<br />`word breakers` display_term에 대 한`breakers`<br />`stemmers` display_term에 대 한`stemmers`|  
  
## <a name="remarks"></a>주의  
 **sys.dm_fts_parser** 와 같은 구문 및 전체 텍스트 조건자의 기능을 지 원하는 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 및 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md), 및 함수와 같은 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)및 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)합니다.  
  
## <a name="using-unicode-for-parsing-special-characters"></a>유니코드를 사용하여 특수 문자 구문 분석  
 쿼리 문자열을 구문 분석 하면 **sys.dm_fts_parser** 쿼리 문자열을 유니코드로 지정 하지 않는 한, 연결 되어 있는 데이터베이스의 데이터 정렬을 사용 합니다. 따라서 ü 또는 ç 같은 특수 문자가 포함 된 비유니코드 문자열에 대 한 출력 못할 수도 있습니다는 데이터베이스의 데이터 정렬에 따라 예상 합니다. 데이터베이스 데이터 정렬과 별도로 쿼리 문자열을 처리 하려면 문자열 앞 `N`, 즉, `N'` *query_string*`'`합니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 "3. 특수 문자가 포함된 문자열의 출력 표시"를 참조하십시오.  
  
## <a name="when-to-use-sysdmftsparser"></a>sys.dm_fts_parser를 사용하는 경우  
 **sys.dm_fts_parser** 디버깅을 위해 매우 강력 할 수 있습니다. 몇 가지 주요 사용 시나리오는 다음과 같습니다.  
  
-   지정된 단어 분리기가 주어진 입력을 처리하는 방법을 이해하려면  
  
     쿼리가 예기치 않은 결과를 반환하는 것은 단어 분리기가 데이터를 구문 분석하고 분리하는 방법 때문일 수 있습니다. sys.dm_fts_parser를 사용하면 단어 분리기가 전체 텍스트 인덱스에 전달하는 결과를 확인할 수 있습니다. 또한 전체 텍스트 인덱스에서 검색되지 않는 용어와 중지 단어를 확인할 수 있습니다. 지정된 된 언어에 의해 지정 된 중지 목록에 있는지에 따라 다릅니다. 지정 하는 단어는 중지 단어 인지 여부는 *stoplist_id* 함수에서 선언 된 값입니다.  
  
     또한 악센트 구분 플래그를 사용하면 단어 분리기가 해당 악센트 구분 정보를 포함하는 입력을 구문 분석하는 방법을 알 수 있습니다.  
  
-   형태소 분석기가 지정된 입력에 미치는 영향을 이해하려면  
  
     다음 FORMSOF 절이 포함된 CONTAINS 또는 CONTAINSTABLE 쿼리를 지정하면 단어 분리기와 형태소 분석기가 쿼리 용어와 해당 형태소 분석 형태를 구문 분석하는 방법을 확인할 수 있습니다.  
  
    ```  
    FORMSOF( INFLECTIONAL, query_term )  
    ```  
  
     이 결과는 전체 텍스트 인덱스에 전달되는 용어를 보여 줍니다.  
  
-   동의어 사전이 입력의 전부 또는 일부를 확장하거나 대체하는 방법을 이해하려면  
  
     다음을 지정할 수도 있습니다.  
  
    ```  
    FORMSOF( THESAURUS, query_term )  
    ```  
  
     이 쿼리의 결과는 단어 분리기와 동의어 사전이 쿼리 용어를 위해 상호 작용하는 방법을 보여 줍니다. 동의어 사전의 확장 또는 대체를 확인하고 전체 텍스트 인덱스에 대해 실제로 실행되는 결과 쿼리를 식별할 수 있습니다.  
  
     다음을 실행할 수 있습니다.  
  
    ```  
    FORMSOF( FREETEXT, query_term )  
    ```  
  
     그러면 활용 및 동의어 사전 기능이 자동으로 수행됩니다.  
  
 위의 사용 시나리오 외에도 sys.dm_fts_parser를 사용하면 전체 텍스트 쿼리와 관련된 다른 많은 문제를 이해하고 해결하는 데 많은 도움이 됩니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 고정 서버 역할 및 액세스 권한이 지정된 된 중지 목록에 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-the-output-of-a-given-word-breaker-for-a-keyword-or-phrase"></a>1. 키워드 또는 구에 대해 지정된 단어 분리기의 출력 표시  
 다음 예에서는 아래의 쿼리 문자열에 대해 LCID가 1033인 영어 단어 분리기를 사용하여 출력을 반환합니다. 여기서 중지 목록은 사용되지 않습니다.  
  
 `The Microsoft business analysis`  
  
 악센트 구분은 사용하지 않습니다.  
  
```  
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis" ', 1033, 0, 0);  
```  
  
### <a name="b-displaying-the-output-of-a-given-word-breaker-in-the-context-of-stoplist-filtering"></a>2. 중지 목록 필터링 컨텍스트에서 지정된 단어 분리기의 출력 표시  
 다음 예에서는 아래의 쿼리 문자열에 대해 LCID가 1033인 영어 단어 분리기와 ID가 77인 영어 중지 목록을 사용하여 출력을 반환합니다.  
  
 `"The Microsoft business analysis" OR "MS revenue"`  
  
 악센트 구분은 사용하지 않습니다.  
  
```  
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis"  OR " MS revenue" ', 1033, 77, 0);  
```  
  
### <a name="c-displaying-the-output-of-a-string-that-contains-special-characters"></a>3. 특수 문자가 포함된 문자열의 출력 표시  
 다음 예에서는 유니코드를 사용하여 아래의 프랑스어 문자열을 구문 분석합니다.  
  
 `français`  
  
 이 예에서는 프랑스어의 LCID인 `1036`과 사용자 정의 중지 목록의 ID인 `5`를 지정하고 악센트 구분을 사용합니다.  
  
```  
SELECT * FROM sys.dm_fts_parser(N'français', 1036, 5, 1);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [구성 하 고 전체 텍스트 검색에 대 한 동의어 사전 파일을 관리 합니다.](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [구성 및 전체 텍스트 검색에 대 한 중지 단어와 중지 목록 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [보안 개체](../../relational-databases/security/securables.md)  
  
  
