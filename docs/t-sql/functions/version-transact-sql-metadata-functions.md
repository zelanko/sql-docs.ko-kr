---
description: Version - Transact SQL 메타 데이터 함수
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 1866248cf8f60f55ab0fd0d809c1ce55f7d24f59
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380528"
---
# <a name="version---transact-sql-metadata-functions"></a>Version - Transact SQL 메타 데이터 함수
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

 어플라이언스에서 실행되는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]의 버전을 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Azure Synapse Analytics and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
이 함수가 결과를 반환하려면 테이블 이름이 이 함수에 대해 [FROM](../../t-sql/queries/from-transact-sql.md) 절에서 지정되어야 합니다. 쿼리에 대한 결과 집합에서 각 행에 대해 결과 행이 반환됩니다. 반환되는 행 수를 제한하려면 [TOP(Transact SQL)](../../t-sql/queries/top-transact-sql.md)을 사용합니다.  
  
## <a name="examples"></a>예제  
다음 예에서는 버전 번호를 반환합니다.  
  
```sql
SELECT VERSION();  
```  
  
## <a name="see-also"></a>참고 항목 
[SESSION_ID(Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
