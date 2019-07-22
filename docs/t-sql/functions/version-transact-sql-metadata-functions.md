---
title: VERSION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ed3eab701a8edbbf118e228bd90080a61a214b32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927435"
---
# <a name="version---transact-sql-metadata-functions"></a>Version - Transact SQL 메타 데이터 함수
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 어플라이언스에서 실행되는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]의 버전을 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
이 함수가 결과를 반환하려면 테이블 이름이 이 함수에 대해 [FROM](../../t-sql/queries/from-transact-sql.md) 절에서 지정되어야 합니다. 쿼리에 대한 결과 집합에서 각 행에 대해 결과 행이 반환됩니다. 반환되는 행 수를 제한하려면 [TOP(Transact SQL)](../../t-sql/queries/top-transact-sql.md)을 사용합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 버전 번호를 반환합니다.  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>참고 항목 
[SESSION_ID(Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
