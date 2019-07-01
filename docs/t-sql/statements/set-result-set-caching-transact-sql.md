---
title: SET RESULT SET CACHING  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f9750cdc2dea7049bde77d31c275789691abf1b0
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67313821"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

현재 클라이언트 세션에 대한 결과 집합 동작을 제어합니다.  

적용 대상: Azure SQL Data Warehouse(미리 보기) 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

**ON**   
현재 클라이언트 세션에 대한 결과 집합 캐싱을 설정합니다.  데이터베이스 수준에서 결과 집합 캐싱이 OFF인 경우 세션에서 ON으로 설정할 수 없습니다.

**OFF**   
현재 클라이언트 세션에 대한 결과 집합 캐싱을 사용하지 않도록 설정합니다.

## <a name="permissions"></a>사용 권한

public 역할의 멤버 자격이 필요

## <a name="see-also"></a>관련 항목:

[SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)