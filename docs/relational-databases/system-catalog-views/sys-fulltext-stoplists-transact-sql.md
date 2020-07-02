---
title: sys. fulltext_stoplists (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_stoplists
- sys.fulltext_stoplists_TSQL
- fulltext_stoplists_TSQL
- fulltext_stoplists
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- sys.fulltext_stoplists catalog view
- stopwords [full-text search]
ms.assetid: eb69fb8f-f6d9-446e-83c0-67afd05dfba0
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2514fed43b764b51806b78db68e1ae6840059ab
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760398"
---
# <a name="sysfulltext_stoplists-transact-sql"></a>sys.fulltext_stoplists(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  데이터베이스의 전체 텍스트 중지 목록당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**stoplist_id**|**int**|데이터베이스 내에서 고유한 중지 목록 ID입니다.|  
|**name**|**sysname**|중지 목록의 이름입니다.|  
|**create_date**|**datetime**|중지 목록이 만들어진 날짜입니다.|  
|**modify_date**|**datetime**|ALTER 문을 사용하여 중지 목록을 마지막으로 수정한 날짜입니다.|  
|**Principal_id**|**int**|중지 목록을 소유하는 데이터베이스 보안 주체의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [fulltext_system_stopwords &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)   
 [fulltext_stopwords &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [전체 텍스트 검색에 대 한 중지 단어 및 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Transact-sql&#41;&#40;전체 텍스트 중지 목록 만들기](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [Transact-sql&#41;&#40;전체 텍스트 중지 목록 변경](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST&#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
  
