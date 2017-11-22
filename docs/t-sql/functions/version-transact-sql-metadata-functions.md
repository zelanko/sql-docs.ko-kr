---
title: "버전 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa9dec84a07189eb3b2c6c9c3d9342db4eac1df6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="version---transact-sql-metadata-functions"></a>버전-Transact SQL 메타 데이터 함수
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 버전을 반환 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 기기에서 실행 합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
테이블 이름에 지정 해야 합니다는 [FROM](../../t-sql/queries/from-transact-sql.md) 결과 반환 하려면이 함수에 대 한 절. 쿼리 한 결과 집합의 각 행에 대 한 결과 행이 반환 됩니다. 사용 하 여 [TOP (Transact SQL)](../../t-sql/queries/top-transact-sql.md) 반환 된 행의 수를 제한 합니다.  
  
## <a name="examples"></a>예  
다음 예제에서는 버전 번호를 반환 합니다.  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>관련 항목: 
[세션 ID (Transact SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40; Transact SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
