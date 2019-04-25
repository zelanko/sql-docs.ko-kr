---
title: 스칼라 함수 호출 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24b62c2b5cd449b6e7201d413b315e48fbd570f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468800"
---
# <a name="scalar-function-calls"></a>스칼라 함수 호출
스칼라 함수는 각 행에 대 한 값을 반환합니다. 예를 들어, 절대 값 스칼라 함수는 숫자 열을 인수로 받고 열의 각 값의 절대값을 반환 합니다. 스칼라 함수 호출에 대 한 이스케이프 시퀀스는  
  
 **{fn**  _scalar-function_ **}**  
  
 여기서 *스칼라 함수* 에 나열 된 함수 중 하나인 [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)합니다. 스칼라 함수 이스케이프 시퀀스에 대 한 자세한 내용은 참조 하세요. [스칼라 함수 이스케이프 시퀀스](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) 부록 c: SQL 문법입니다.  
  
 예를 들어, 다음 SQL 문의 이름을 대문자로 고객의 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스가 구문을 사용 합니다. 두 번째 문은 Ingres OS/2에 대 한 기본 구문을 사용 하 고 상호 운용은 불가능 합니다.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 응용 프로그램 기본 구문을 사용 하는 스칼라 함수를 호출 하 고 ODBC 구문을 사용 하는 스칼라 함수에 대 한 호출을 혼합할 수 있습니다. 예를 들어, Employee 테이블의 이름은 성, 쉼표 및 이름으로 저장 됩니다 하는 것으로 가정 합니다. 다음 SQL 문은 Employee 테이블에 직원의 성을 결과 집합을 만듭니다. ODBC 스칼라 함수를 사용 하 여 문을 **SUBSTRING** 및 SQL Server 스칼라 함수 **CHARINDEX** SQL 서버에만 올바르게 실행 됩니다.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 최대 상호 운용성을 위해 응용 프로그램 사용 해야 합니다 **변환** 스칼라 함수는 스칼라 함수의 출력을 필수 형식 인지 확인 합니다. 합니다 **변환** 함수 한 SQL 데이터 형식에서 지정된 된 SQL 데이터 형식으로 데이터를 변환 합니다. 구문의 합니다 **변환** 함수는  
  
 **CONVERT(** _value_exp_ **,** _data_type_**)**  
  
 여기서 *value_exp* 열 이름, 다른 스칼라 함수 또는 리터럴 값의 결과 및 *data_type* 일치 하는 키워드를 **#define** 에서 사용 되는 이름은 SQL 데이터 형식 식별자에 정의 된 대로 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다. 예를 들어, 다음 SQL 문을 사용 하 여는 **변환** 되도록 하는 함수 출력을 **CURDATE** 함수는 날짜, 타임 스탬프 나 문자 데이터를 대신:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 데이터 소스에 의해 지원 되는 스칼라 함수를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS, 및 SQL_TIMEDATE_ 함수 옵션입니다. 지원 되는 변환 작업을 결정 하는 **변환** 함수를 응용 프로그램 호출 **SQLGetInfo** SQL_CONVERT로 시작 하는 옵션 중 하나를 사용 하 여 합니다.
