---
title: sys.fulltext_stopwords (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_stopwords_TSQL
- fulltext_stopwords
- sys.fulltext_stopwords
- sys.fulltext_stopwords_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stopwords
- sys.fulltext_stopwords catalog view
- stopwords [full-text search]
ms.assetid: 79787bb7-d729-448e-b56a-0a467bbb304f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fd799d99d92607363f0203c5c288cbd5a0da6838
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945650"
---
# <a name="sysfulltextstopwords-transact-sql"></a>sys.fulltext_stopwords(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스의 모든 중지 목록에 속한 중지 단어당 한 개의 행을 포함합니다.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**stoplist_id**|**int**|**stopword** 가 속한 중지 목록의 ID입니다. 이 ID는 데이터베이스 내에서 고유합니다.|  
|**stopword**|**nvarchar(64)**|중지 단어 일치 항목으로 간주되는 용어입니다.|  
|**language**|**sysname**|별칭 값 이거나 [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)로캘 식별자의 값에 해당 하 (**LCID**), 숫자로 된 LCID의 문자열 표현입니다.|  
|**language_id**|**int**|단어 분리에 사용되는 LCID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_system_stopwords&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)  
  
  
