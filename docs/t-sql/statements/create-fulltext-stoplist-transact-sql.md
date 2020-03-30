---
title: CREATE FULLTEXT STOPLIST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7d2061479ac8f93dfcdbc4a8039ef3914d897f87
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73064650"
---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
 중지 단어는 데이터베이스에서 *중지 목록*이라는 개체를 사용하여 관리됩니다. 중지 목록은 전체 텍스트 인덱스와 연결된 경우 해당 인덱스의 전체 텍스트 쿼리에 적용되는 중지 단어 목록입니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST 및 DROP FULLTEXT STOPLIST는 호환성 수준이 100인 경우에만 지원됩니다. 호환성 수준이 80 및 90인 경우에는 이러한 문이 지원되지 않습니다. 하지만 모든 호환성 수준에서 시스템 중지 목록은 새로운 전체 텍스트 인덱스와 자동으로 연결됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>인수  
 *stoplist_name*  
 중지 목록의 이름입니다. *stoplist_name*은 최대 128자까지 가능합니다. *stoplist_name*은 현재 데이터베이스 내의 모든 중지 목록 가운데 고유해야 하고 식별자에 대한 규칙을 따라야 합니다.  
  
 *stoplist_name*은 전체 텍스트 인덱스를 만들 때 사용합니다.  
  
 *database_name*  
 *source_stoplist_name*에 의해 지정된 중지 목록이 있는 데이터베이스의 이름입니다. *database_name*을 지정하지 않으면 기본적으로 현재 데이터베이스가 됩니다.  
  
 *source_stoplist_name*  
 기존 중지 목록을 복사하여 새 중지 목록을 만들도록 지정합니다. *source_stoplist_name*이 없거나 데이터베이스 사용자에게 올바른 권한이 없는 경우 CREATE FULLTEXT STOPLIST는 오류 메시지와 함께 실패합니다. 원본 중지 목록에 중지 단어로 지정된 언어가 현재 데이터베이스에 등록되지 않은 경우 CREATE FULLTEXT STOPLIST는 성공하지만 경고가 반환되고 해당 중지 단어가 추가되지 않습니다.  
  
 SYSTEM STOPLIST  
 [리소스 데이터베이스](../../relational-databases/databases/resource-database.md)에 기본적으로 존재하는 중지 목록으로 새 중지 목록을 만들도록 지정합니다.  
  
 AUTHORIZATION *owner_name*  
 중지 목록을 소유하는 데이터베이스 보안 주체의 이름을 지정합니다. *owner_name*은 현재 사용자가 멤버로 속한 보안 주체의 이름이어야 합니다. 그렇지 않으면 현재 사용자가 *owner_name*에 대한 IMPERSONATE 권한이 있어야 합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.  
  
## <a name="remarks"></a>설명  
 중지 목록의 생성자는 해당 소유자입니다.  
  
## <a name="permissions"></a>사용 권한  
 STOPLIST를 만들려면 CREATE FULLTEXT CATALOG 권한이 필요합니다. 중지 목록 소유자는 중지 목록에 대한 CONTROL 권한을 명시적으로 부여하여 사용자가 단어를 추가 및 제거하고 중지 목록을 삭제하도록 허용할 수 있습니다.  
  
> [!NOTE]  
>  전체 텍스트 인덱스가 포함된 중지 목록을 사용하려면 REFERENCE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>A. 새로운 전체 텍스트 중지 목록 작성  
 다음 예에서는 `myStoplist`라는 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>B. 기존 전체 텍스트 중지 목록에서 전체 텍스트 중지 목록 복사  
 다음 예에서는 기존 AdventureWorks 중지 목록 `myStoplist2`를 복사하여 새로운 전체 텍스트 중지 목록 `Customers.otherStoplist`를 만듭니다.  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>C. 시스템 전체 텍스트 중지 목록에서 전체 텍스트 중지 목록 복사  
 다음 예에서는 시스템 중지 목록에서 전체 텍스트 중지 목록을 복사하여 `myStoplist3`이라는 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
