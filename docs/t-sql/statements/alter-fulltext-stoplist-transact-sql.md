---
title: ALTER FULLTEXT STOPLIST (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs: TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20947c0331f9713a937e0a7de8efb1f2fc9f753c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 변경할 중지 목록의 이름입니다. *stoplist_name* 최대 128 자가 될 수 있습니다.  
  
 **'** *중지 단어* **'**  
 지정된 언어에서 언어적 의미가 있는 단어 또는 언어적 의미가 없는 토큰일 수 있는 문자열입니다. *중지 단어* 최대 토큰 길이 64 자로 제한 됩니다. 중지 단어를 유니코드 문자열로 지정할 수 있습니다.  
  
 언어 *language_term*  
 와 연결할 언어를 지정 된 *중지 단어* 목록에 추가 되거나 삭제 합니다.  
  
 *language_term* 로 문자열, 정수 또는 16 진수 값에 해당 하는 언어의 로캘 식별자 (LCID) 다음과 같이 지정할 수 있습니다.  
  
|형식|Description|  
|------------|-----------------|  
|문자열|*language_term* 에 해당 하는 **별칭** 열 값에는 [sys.syslanguages (TRANSACT-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 보기. 와 같이 하나의 따옴표로 묶어야 합니다 문자열 **'***language_term***'**합니다.|  
|정수|*language_term* 는 언어의 LCID입니다.|  
|Hexadecimal|*language_term* 된 LCID의 16 진수 값은 0x 시작 합니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다. 값이 DBCS(더블바이트 문자 집합) 형식인 경우 SQL Server에서는 값을 유니코드로 변환합니다.|  
  
 추가 **'***중지 단어***'** 언어 *language_term*  
 언어에 의해 지정 된 언어에 대 한 중지 목록에 중지 단어 추가 *language_term*합니다.  
  
 지정된 키워드와 언어 LCID 값 조합이 STOPLIST에서 고유하지 않으면 오류가 반환됩니다.  LCID 값이 등록된 언어와 일치하지 않으면 오류가 발생합니다.  
  
 DROP { **'***중지 단어***'** 언어 *language_term* | 모든 언어 *language_term* | 모든}  
 중지 목록에서 중지 단어를 삭제합니다.  
  
 **'** *중지 단어* **'** 언어 *language_term*  
 지정 된 언어에 대 한 지정 된 중지 단어 삭제 *language_term*합니다.  
  
 모든 언어 *language_term*  
 모든 지정 된 언어에 대 한 중지 단어 삭제 *language_term*합니다.  
  
 ALL  
 중지 목록에 있는 모든 중지 단어를 삭제합니다.  
  
## <a name="remarks"></a>주의  
 CREATE FULLTEXT STOPLIST는 호환성 수준 100 이상에만 지원됩니다. 호환성 수준 80 및 90의 경우 시스템 중지 목록이 항상 데이터베이스에 할당됩니다.  
  
## <a name="permissions"></a>Permissions  
 중지 목록을 데이터베이스의 기본 중지 목록으로 지정하려면 ALTER DATABASE 사용 권한이 필요합니다. 그렇지 않고 중지 목록을 변경 하려면 중지 목록의 소유자 이거나의 멤버 자격이 필요는 **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `CombinedFunctionWordList`라는 중지 목록에서 먼저 스페인어에 단어 "en"을 추가한 다음 프랑스어에 단어 'en'을 추가합니다.  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [전체 텍스트 중지 목록 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT stoplist&#40; Transact SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [구성 및 전체 텍스트 검색에 대 한 중지 단어와 중지 목록 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
