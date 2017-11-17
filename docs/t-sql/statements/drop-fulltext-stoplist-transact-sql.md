---
title: DROP FULLTEXT STOPLIST (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs:
- TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 86431229e26091e2fde6c3f81873523c5f09de68
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스에서 전체 텍스트 중지 목록을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST는 호환성 수준 100 이상에만 지원됩니다. 호환성 수준 80 및 90의 경우 시스템 중지 목록이 항상 데이터베이스에 할당됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
## <a name="arguments"></a>인수  
 *stoplist_name*  
 데이터베이스에서 삭제할 전체 텍스트 중지 목록의 이름입니다.  
  
## <a name="remarks"></a>주의  
 삭제 중인 전체 텍스트 중지 목록을 참조하는 전체 텍스트 인덱스가 있는 경우 DROP FULLTEXT STOPLIST가 실패합니다.  
  
## <a name="permissions"></a>Permissions  
 중지 목록을 삭제 한 중지 목록 또는의 멤버 자격에 대 한 DROP 권한이 필요는 **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `myStoplist`라는 전체 텍스트 중지 목록을 삭제합니다.  
  
```  
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER FULLTEXT stoplist&#40; Transact SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [전체 텍스트 중지 목록 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  

