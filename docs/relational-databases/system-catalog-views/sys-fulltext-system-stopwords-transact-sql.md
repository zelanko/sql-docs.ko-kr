---
title: sys. fulltext_system_stopwords (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_system_stopwords_TSQL
- fulltext_system_stopwords
- fulltext_system_stopwords_TSQL
- sys.fulltext_system_stopwords
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- sys.fulltext_system_stopwords catalog view
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 487de53f-c637-4d78-85f6-fef5e768cd0c
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ebc1eaee0e34451a7f0bada85deafa90ff4f5d3a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68220330"
---
# <a name="sysfulltext_system_stopwords-transact-sql"></a>sys.fulltext_system_stopwords(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  시스템 중지 목록에 대한 액세스를 제공합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**중지 단어**|**nvarchar (64)**|중지 단어 일치 항목으로 간주되는 용어입니다.|  
|**language_id**|**int**|언어의 LCID(로캘 ID)입니다. 이 LCID는 단어 분리에 사용됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [fulltext_stoplists &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [fulltext_stopwords &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
