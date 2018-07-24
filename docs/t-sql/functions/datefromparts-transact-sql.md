---
title: DATEFROMPARTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 705d31a9f97d8c7894cd70e20993cde65a0d361f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38063721"
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

이 함수는 지정된 년, 월, 일 값에 매핑되는 **date** 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>인수  
*year*  
년을 지정하는 정수 식입니다.
  
*month*  
1에서 12까지의 숫자로 월을 지정하는 정수 식입니다.
  
*day*  
일을 지정하는 정수 식입니다.
  
## <a name="return-types"></a>반환 형식
**date**
  
## <a name="remarks"></a>Remarks  
`DATEFROMPARTS`는 날짜 부분이 지정된 년, 월, 일로 설정되고 시간 부분이 기본값으로 설정된 **date** 값을 반환합니다. 잘못된 인수의 경우 `DATEFROMPARTS`에서 오류가 발생합니다. `DATEFROMPARTS`는 적어도 하나 이상의 필수 인수에 null 값이 있는 경우 null을 반환합니다.
  
이 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서버 이상을 원격 처리할 수 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이하 버전의 서버를 원격 처리할 수 없습니다.
  
## <a name="examples"></a>예  
이 예제에서는 동작 중인 `DATEFROMPARTS` 함수를 보여줍니다.
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:
[date&#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  

