---
title: DATEFROMPARTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c35227dd4593d4d682caea51cc69c6b5dffd3a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119173"
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
  
  

