---
title: 비트 연산자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d96dbfc519a831508b7e56fad1b6909a37f672d3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004006"
---
# <a name="bitwise-operators-transact-sql"></a>비트 연산자(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  비트 연산자는 두 식 사이의 비트 조작을 수행합니다. 이 때 식에는 정수 데이터 형식에 속하는 모든 데이터 형식을 사용할 수 있습니다.  
  비트 연산자는 두 개의 정수 값을 이진 비트로 변환하고, AND, OR 또는 NOT 연산을 각 비트에서 수행하여 결과를 생성합니다. 그런 다음, 결과를 정수로 변환합니다.  
  
  예를 들어 정수 170을 이진 1010 1010으로 변환합니다.
정수 75를 이진 0100 1011로 변환합니다.

|operator|비트 수치 연산|
|---- |---- |
|AND <br> 모든 위치에서 비트가 모두 1이면 결과는 1입니다. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|또는 <br> 모든 위치에서 어느 한쪽 비트가 1이면 결과는 1입니다. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> 모든 비트 위치에서 비트 값을 반대로 바꿉니다. |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
다음 항목을 참조하세요.   
* [&&#40;비트 AND&#41;](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [&=&#40;비트 AND 대입&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124;&#40;비트 OR&#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124;=&#40;비트 OR 대입&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^&#40;배타적 비트 OR&#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^=&#40;배타적 비트 OR 대입&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~&#40;비트 NOT&#41;](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 비트 연산자의 피연산자는 정수 또는 이진 문자열 데이터 형식(**image** 데이터 형식은 제외)에 속하는 모든 데이터 형식이 될 수 있습니다. 단, 두 피연산자가 모두 이진 문자열 데이터 형식이어서는 안 됩니다. 다음 표에서는 지원되는 피연산자 데이터 형식을 보여 줍니다.  
  
|왼쪽 피연산자|오른쪽 피연산자|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint** 또는 **tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**, **smallint**, **tinyint** 또는 **bit**|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**bigint**, **int**, **smallint**, **tinyint**, **binary** 또는 **varbinary**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** 또는 **varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** 또는 **varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** 또는 **varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint** 또는 **tinyint**|  
  
## <a name="see-also"></a>참고 항목  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)
