---
title: "비트 연산자 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b0706080c0a878987fab8d2cc5f0c1677f43309b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="bitwise-operators-transact-sql"></a>비트 연산자(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  비트 연산자는 두 식 사이의 비트 조작을 수행합니다. 이 때 식에는 정수 데이터 형식에 속하는 모든 데이터 형식을 사용할 수 있습니다.  
  비트 연산자 이진 비트를 두 개의 정수 값을 변환, 수행 AND, OR, 또는 결과 생성 각 비트 NOT 연산을 합니다. 그런 다음 결과 정수로 변환합니다.  
  
  예를 들어 정수 170 이진 1010 1010 변환합니다.
이진 0100 1011 75 정수로 변환합니다.

|적용한 후|비트 수학|
|---- |---- |
|및 <br> 모든 위치에서 비트 모두 모두 1 이면 결과 1입니다. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|OR <br> 모든 위치에서 어느 한쪽 비트가 1 이면 결과 1입니다. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> 모든 비트 위치에서 비트 값을 반대로 바꿉니다. |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
다음 항목을 참조 합니다.   
* [& &#40; 비트 AND &#41;](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = &#40; 비트 AND 대입 &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124; &#40; 비트 OR &#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = &#40; 비트 OR 할당 &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ &#40; 비트 배타적 OR &#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = &#40; 비트 배타적 OR 할당 &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ &#40; 비트 NOT &#41;](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 비트 연산자의 피연산자는 정수 또는 이진 문자열 데이터 형식 범주의 데이터 형식 중 하나가 될 수 있습니다 (제외 하 고는 **이미지** 데이터 형식) 제외 하 고 두 피연산자 모두 이진 문자열 데이터 형식 중 하나를 사용할 수 없습니다 데이터 형식 범주입니다. 다음 표에서는 지원되는 피연산자 데이터 형식을 보여 줍니다.  
  
|왼쪽 피연산자|오른쪽 피연산자|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint**, 또는 **tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**, **smallint**, **tinyint**, 또는 **비트**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **이진**, 또는 **varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **이진**, 또는 **varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **이진**, 또는 **varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint**, 또는 **tinyint**|  
  
## <a name="see-also"></a>관련 항목:  
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
