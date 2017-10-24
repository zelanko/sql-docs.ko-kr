---
title: "버전 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1905ef3b0f31e91d6cec00c0314770b7686e8c51
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="version---transact-sql-metadata-functions"></a>버전-Transact SQL 메타 데이터 함수
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

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
  
  

