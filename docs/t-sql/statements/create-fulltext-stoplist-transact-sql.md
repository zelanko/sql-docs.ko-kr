---
title: CREATE FULLTEXT STOPLIST (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STOPLIST_TSQL
- FULLTEXT STOPLIST
- STOPLIST
- FULLTEXT_STOPLIST_TSQL
- CREATE FULLTEXT STOPLIST
- CREATE_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- CREATE FULLTEXT STOPLIST statement
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 0669b1d0-46cc-4fac-8df7-5f7fa7af5db4
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6877dccd56d4f90a5600b095b1294ec1ccd6eb3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
 중지 단어 라고 하는 개체를 사용 하 여 데이터베이스에서 관리 됩니다 *중지 목록*합니다. 중지 목록은 전체 텍스트 인덱스와 연결된 경우 해당 인덱스의 전체 텍스트 쿼리에 적용되는 중지 단어 목록입니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST 및 DROP FULLTEXT STOPLIST는 호환성 수준이 100인 경우에만 지원됩니다. 호환성 수준이 80 및 90인 경우에는 이러한 문이 지원되지 않습니다. 하지만 모든 호환성 수준에서 시스템 중지 목록은 새로운 전체 텍스트 인덱스와 자동으로 연결됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>인수  
 *stoplist_name*  
 중지 목록의 이름입니다. *stoplist_name* 최대 128 자가 될 수 있습니다. *stoplist_name* 현재 데이터베이스의 모든 중지 목록 가운데 고유 해야 하며 식별자에 대 한 규칙을 따라야 합니다.  
  
 *stoplist_name* 전체 텍스트 인덱스를 만들 때 사용 됩니다.  
  
 *database_name*  
 중지 목록에 지정 된 있는 데이터베이스의 이름인 *source_stoplist_name* 있는 합니다. 지정 하지 않으면 *database_name* 현재 데이터베이스에 대 한 기본값입니다.  
  
 *source_stoplist_name*  
 기존 중지 목록을 복사하여 새 중지 목록을 만들도록 지정합니다. 경우 *source_stoplist_name* 존재 하지 않는 또는 데이터베이스 사용자 올바른 권한이, CREATE FULLTEXT STOPLIST는 오류와 함께 실패 합니다. 원본 중지 목록에 중지 단어로 지정된 언어가 현재 데이터베이스에 등록되지 않은 경우 CREATE FULLTEXT STOPLIST는 성공하지만 경고가 반환되고 해당 중지 단어가 추가되지 않습니다.  
  
 SYSTEM STOPLIST  
 새 중지 목록을 만들어지도록 지정 존재 하는 중지 목록으로에서 기본적으로는 [리소스 데이터베이스](../../relational-databases/databases/resource-database.md)합니다.  
  
 권한 부여 *owner_name*  
 중지 목록을 소유하는 데이터베이스 보안 주체의 이름을 지정합니다. *owner_name* 는 현재 사용자가 멤버, 또는 현재 사용자 대 한 IMPERSONATE 권한이 있어야 주체의 이름 이어야 합니다. *owner_name*합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.  
  
## <a name="remarks"></a>주의  
 중지 목록의 생성자는 해당 소유자입니다.  
  
## <a name="permissions"></a>Permissions  
 STOPLIST를 만들려면 CREATE FULLTEXT CATALOG 권한이 필요합니다. 중지 목록 소유자는 중지 목록에 대한 CONTROL 권한을 명시적으로 부여하여 사용자가 단어를 추가 및 제거하고 중지 목록을 삭제하도록 허용할 수 있습니다.  
  
> [!NOTE]  
>  전체 텍스트 인덱스가 포함된 중지 목록을 사용하려면 REFERENCE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>1. 새로운 전체 텍스트 중지 목록 작성  
 다음 예에서는 `myStoplist`라는 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>2. 기존 전체 텍스트 중지 목록에서 전체 텍스트 중지 목록 복사  
 다음 예에서는 기존 AdventureWorks 중지 목록 `myStoplist2`를 복사하여 새로운 전체 텍스트 중지 목록 `Customers.otherStoplist`를 만듭니다.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>3. 시스템 전체 텍스트 중지 목록에서 전체 텍스트 중지 목록 복사  
 다음 예에서는 시스템 중지 목록에서 전체 텍스트 중지 목록을 복사하여 `myStoplist3`이라는 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER FULLTEXT stoplist&#40; Transact SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT stoplist&#40; Transact SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [구성 및 전체 텍스트 검색에 대 한 중지 단어와 중지 목록 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
