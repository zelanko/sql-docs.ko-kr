---
title: 스칼라 함수 호출 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304264"
---
# <a name="scalar-function-calls"></a>스칼라 함수 호출
Scalar 함수는 각 행에 대한 값을 반환합니다. 예를 들어 절대 값 스칼라 함수는 숫자 열을 인수로 지정하고 열의 각 값의 절대 값을 반환합니다. 스칼라 함수를 호출하기 위한 이스케이프 시퀀스는  
  
 **{fn**  _스칼라 기능_ **}**  
  
 여기서 *스칼라 함수는* [부록 E: 스칼라 함수에](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)나열된 함수 중 하나입니다. 스칼라 함수 이스케이프 시퀀스에 대한 자세한 내용은 부록 C: SQL 문법의 [스칼라 함수 이스케이프 시퀀스를](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) 참조하십시오.  
  
 예를 들어 다음 SQL 문은 대문자 고객 이름의 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용합니다. 두 번째 문은 OS/2에 대한 Ingres에 대한 기본 구문을 사용하며 상호 운용할 수 없습니다.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 응용 프로그램은 기본 구문을 사용하는 스칼라 함수에 대한 호출과 ODBC 구문을 사용하는 스칼라 함수에 대한 호출을 혼합할 수 있습니다. 예를 들어 Employee 테이블의 이름이 성, 쉼표 및 이름으로 저장된다고 가정합니다. 다음 SQL 문은 Employee 테이블에서 직원의 성 집합을 만듭니다. 이 문은 ODBC 스칼라 함수 **SUBSTRING** 및 SQL Server 스칼라 함수 **CHARINDEX를** 사용하며 SQL Server에서만 올바르게 실행됩니다.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 최대 상호 운용성을 위해 응용 프로그램은 **CONVERT** 스칼라 함수를 사용하여 스칼라 함수의 출력이 필수 유형인지 확인해야 합니다. **CONVERT** 함수는 하나의 SQL 데이터 형식의 데이터를 지정된 SQL 데이터 유형으로 변환합니다. **CONVERT** 함수의 구문은  
  
 **변환 (value_exp** _value_exp_ **,** _data_type)_**)**  
  
 *value_exp* 열 이름, 다른 스칼라 함수의 결과 또는 리터럴 값이며 *data_type* [부록 D: 데이터 형식에](../../../odbc/reference/appendixes/appendix-d-data-types.md)정의된 SQL 데이터 형식 식별자에서 사용되는 **#define** 이름과 일치하는 키워드입니다. 예를 들어 다음 SQL 문은 **CONVERT** 함수를 사용하여 **CURDATE** 함수의 출력이 타임스탬프 나 문자 데이터 대신 날짜인지 확인합니다.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 데이터 원본에서 지원되는 스칼라 함수를 결정하기 위해 응용 프로그램은 SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS 및 SQL_TIMEDATE_FUNCTIONS 옵션을 사용하여 **SQLGetInfo를** 호출합니다. **CONVERT** 함수에서 지원되는 변환 작업을 결정하기 위해 응용 프로그램은 SQL_CONVERT 시작하는 옵션 중 어느 것이라도 **SQLGetInfo를** 호출합니다.
