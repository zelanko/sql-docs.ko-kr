---
title: 산술 연산자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6fd33150c41b692c803348f3246a165b785f0a1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85990602"
---
# <a name="arithmetic-operators-transact-sql"></a>산술 연산자(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

산술 연산자는 둘 이상의 데이터 형식이 포함된 두 개의 식에서 수치 연산을 실행합니다. 이 연산자는 숫자 데이터 형식 범주에서 실행됩니다. 데이터 형식 범주에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.  
  
|연산자|의미|  
|--------------|-------------|  
|[+(더하기)](../../t-sql/language-elements/add-transact-sql.md)|더하기|  
|[-(빼기)](../../t-sql/language-elements/subtract-transact-sql.md)|빼기|  
|[*(곱하기)](../../t-sql/language-elements/multiply-transact-sql.md)|곱하기|  
|[/(나누기)](../../t-sql/language-elements/divide-transact-sql.md)|나누기|  
|[%(모듈로)](../../t-sql/language-elements/modulo-transact-sql.md)|나누기의 정수 나머지를 반환합니다. 예를 들어 12를 5로 나누면 나머지가 2이므로 12 % 5 = 2를 반환합니다.|  
  
더하기(+)와 빼기(-)는 **datetime** 및 **smalldatetime** 값에 산술 연산을 실행하는 데도 사용할 수 있습니다.  
  
산술 연산 결과의 전체 자릿수와 소수 자릿수에 대한 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
