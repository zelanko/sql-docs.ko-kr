---
title: ALTER FULLTEXT STOPLIST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 52ed53669eba8706a70cd4605d647b86be4652ca
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783954"
---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 기본 전체 텍스트 중지 목록에서 중지 단어를 삽입 또는 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>인수  
 *stoplist_name*  
 변경할 중지 목록의 이름입니다. *stoplist_name*은 최대 128자까지 가능합니다.  
  
 **'** *stopword* **'**  
 지정된 언어에서 언어적 의미가 있는 단어 또는 언어적 의미가 없는 토큰일 수 있는 문자열입니다. *stopword*는 최대 토큰 길이 64자로 제한됩니다. 중지 단어를 유니코드 문자열로 지정할 수 있습니다.  
  
 LANGUAGE *language_term*  
 추가 또는 삭제할 *stopword*와 연결할 언어를 지정합니다.  
  
 *language_term*은 다음과 같이 언어의 LCID(로캘 ID)에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다.  
  
|형식|설명|  
|------------|-----------------|  
|String|*language_term*은 [sys.syslanguages (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 뷰의 **alias** 열 값에 해당합니다. 문자열은 **'***language_term***'** 과 같이 작은따옴표로 묶어야 합니다.|  
|정수|*language_term*은 언어의 LCID입니다.|  
|Hexadecimal|*language_term*은 0x로 시작하는 16진수 LCID 값입니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다. 값이 DBCS(더블바이트 문자 집합) 형식인 경우 SQL Server에서는 값을 유니코드로 변환합니다.|  
  
 ADD **'***stopword***'** LANGUAGE *language_term*  
 LANGUAGE *language_term*으로 지정된 언어의 중지 목록에 중지 단어를 추가합니다.  
  
 지정된 키워드와 언어 LCID 값 조합이 STOPLIST에서 고유하지 않으면 오류가 반환됩니다.  LCID 값이 등록된 언어와 일치하지 않으면 오류가 발생합니다.  
  
 DROP { **'***stopword***'** LANGUAGE *language_term* | ALL LANGUAGE *language_term* | ALL }  
 중지 목록에서 중지 단어를 삭제합니다.  
  
 **'** *stopword* **'** LANGUAGE *language_term*  
 *language_term*으로 지정된 언어에 대해 지정된 중지 단어를 삭제합니다.  
  
 ALL LANGUAGE *language_term*  
 *language_term*으로 지정된 언어에 대해 지정된 중지 단어를 모두 삭제합니다.  
  
 ALL  
 중지 목록에 있는 모든 중지 단어를 삭제합니다.  
  
## <a name="remarks"></a>Remarks  
 CREATE FULLTEXT STOPLIST는 호환성 수준 100 이상에만 지원됩니다. 호환성 수준 80 및 90의 경우 시스템 중지 목록이 항상 데이터베이스에 할당됩니다.  
  
## <a name="permissions"></a>사용 권한  
 중지 목록을 데이터베이스의 기본 중지 목록으로 지정하려면 ALTER DATABASE 사용 권한이 필요합니다. 그렇지 않고 중지 목록을 변경하려면 중지 목록의 소유자이거나 **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `CombinedFunctionWordList`라는 중지 목록에서 먼저 스페인어에 단어 "en"을 추가한 다음 프랑스어에 단어 'en'을 추가합니다.  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE FULLTEXT STOPLIST&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
