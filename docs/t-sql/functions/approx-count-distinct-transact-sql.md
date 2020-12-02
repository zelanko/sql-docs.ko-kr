---
description: APPROX_COUNT_DISTINCT(Transact-SQL)
title: APPROX_COUNT_DISTINCT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e980e97adc29cda45dbedb0640f46d0a444c4b2
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96119491"
---
# <a name="approx_count_distinct-transact-sql"></a>APPROX_COUNT_DISTINCT(Transact-SQL)

[!INCLUDE [sqlserver2019-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2019-asdb-asdbmi-asa.md)]

이 함수는 그룹에 있는 고유한 null이 아닌 값의 대략적인 개수를 반환합니다. 
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
APPROX_COUNT_DISTINCT ( expression )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*expression*  
**image**, **sql_variant**, **ntext** 또는 **text** 를 제외한 모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 

## <a name="return-types"></a>반환 형식
 **bigint**  
  
## <a name="remarks"></a>설명  
`APPROX_COUNT_DISTINCT( expression )`는 그룹의 각 행에 대한 식을 계산하고 그룹에 있는 고유한 null이 아닌 값의 대략적인 개수를 반환합니다. 이 함수는 절대적인 정밀도보다 응답성이 더 중요한 큰 데이터 집합을 기반으로 집계를 제공하도록 디자인되었습니다.  

`APPROX_COUNT_DISTINCT`는 빅 데이터 시나리오에서 사용하도록 디자인되고 다음 조건에 최적화됩니다.
- 수백만 개 이상의 행을 나타내는 데이터 집합의 액세스 *및*
- 많은 고유 값이 포함된 열의 집계

함수 구현은 최대 97% 확률 중에 최대 2% 오류 비율을 보장합니다. 

`APPROX_COUNT_DISTINCT`에는 완전한 COUNT DISTINCT 작업보다 적은 메모리가 필요합니다.  메모리 사용 공간이 작을 경우 `APPROX_COUNT_DISTINCT`는 정확한 COUNT DISTINCT 작업에 비해 메모리를 디스크에 분산시킬 가능성이 적습니다. 이를 수행하는 데 사용되는 알고리즘에 대한 자세한 내용은 [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog)를 참조하세요.

> [!NOTE]
> 데이터 정렬이 중요한 문자열을 사용하면 APPROX_COUNT_DISTINCT는 이진 일치를 사용하고 BIN2가 아닌 BIN 데이터 정렬에서 생성된 결과를 제공합니다. 
  
## <a name="examples"></a>예제  
  
### <a name="a-using-approx_count_distinct"></a>A. APPROX_COUNT_DISTINCT 사용 
이 예제에서는 orders 테이블에서 다양한 주문 키의 대략적인 개수를 반환합니다.
  
```sql
SELECT APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders;
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Approx_Distinct_OrderKey
------------------------
15164704
```
  
### <a name="b-using-approx_count_distinct-with-group-by"></a>B. GROUP BY와 함께 APPROX_COUNT_DISTINCT 사용 
이 예제에서는 orders 테이블에서 주문 상태별로 다양한 주문 키의 대략적인 개수를 반환합니다. 
  
```sql
SELECT O_OrderStatus, APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders
GROUP BY O_OrderStatus
ORDER BY O_OrderStatus; 
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
O_OrderStatus                                                    Approx_Distinct_OrderKey
---------------------------------------------------------------- ------------------------
F                                                                7397838
O                                                                7387803
P                                                                388036
```
    
## <a name="see-also"></a>참고 항목
[집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT&#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md) 
