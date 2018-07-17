---
title: DROP FULLTEXT INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_INDEX_TSQL
- DROP FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- deleting full-text indexes
- removing full-text indexes
- full-text indexes [SQL Server], removing
- DROP FULLTEXT INDEX statement
- dropping full-text indexes
ms.assetid: 7443a4ab-1d43-4a22-bbba-a07f620892cb
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cb5ff7ff811ad7e05d6f8fdc1e54ca6423d7622a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782914"
---
# <a name="drop-fulltext-index-transact-sql"></a>DROP FULLTEXT INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 테이블 또는 인덱싱된 뷰에서 전체 텍스트 인덱스를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP FULLTEXT INDEX ON table_name  
```  
  
## <a name="arguments"></a>인수  
 *table_name*  
 제거할 전체 텍스트 인덱스를 포함하는 테이블 또는 인덱싱된 뷰의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 DROP FULLTEXT INDEX 명령을 사용하기 전에 전체 텍스트 인덱스에서 모든 열을 삭제할 필요는 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 테이블 또는 인덱싱된 뷰에 대한 ALTER 권한을 가지고 있거나 **sysadmin** 고정 서버 역할, **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `JobCandidate` 테이블에 있는 전체 텍스트 인덱스를 삭제합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DROP FULLTEXT INDEX ON HumanResources.JobCandidate;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
