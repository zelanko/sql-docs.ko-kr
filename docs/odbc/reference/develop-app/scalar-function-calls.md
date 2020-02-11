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
ms.openlocfilehash: 37209a75c03a051e3def4d26fa0d4e7f85d0e91d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897745"
---
# <a name="scalar-function-calls"></a>스칼라 함수 호출
스칼라 함수는 각 행에 대 한 값을 반환 합니다. 예를 들어 절대값 스칼라 함수는 숫자 열을 인수로 사용 하 고 열에 있는 각 값의 절대 값을 반환 합니다. 스칼라 함수를 호출 하는 이스케이프 시퀀스는  
  
 **{fn**  _스칼라 함수_ **}**  
  
 여기서 *스칼라 함수* 는 [부록 E: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)에 나열 된 함수 중 하나입니다. 스칼라 함수 이스케이프 시퀀스에 대 한 자세한 내용은 부록 C: SQL 문법의 [스칼라 함수 이스케이프 시퀀스](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) 를 참조 하세요.  
  
 예를 들어 다음 SQL 문은 대문자 고객 이름의 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용 합니다. 두 번째 문은 OS/2에 대 한 기본 구문을 사용 하 여 상호 운용할 수 없습니다.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 응용 프로그램은 네이티브 구문을 사용 하는 스칼라 함수와 ODBC 구문을 사용 하는 스칼라 함수에 대 한 호출을 혼합할 수 있습니다. 예를 들어 Employee 테이블의 이름이 성, 쉼표 및 이름으로 저장 되어 있다고 가정 합니다. 다음 SQL 문은 Employee 테이블에서 직원의 last 이름 결과 집합을 만듭니다. 이 문은 ODBC 스칼라 함수 **SUBSTRING** 및 SQL Server 스칼라 함수 **CHARINDEX** 를 사용 하 고 SQL Server 에서만 올바르게 실행 됩니다.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 상호 운용성을 최대화 하기 위해 응용 프로그램에서는 **CONVERT** 스칼라 함수를 사용 하 여 스칼라 함수의 출력이 필수 형식 인지 확인 해야 합니다. **CONVERT** 함수는 데이터를 한 sql 데이터 형식에서 지정 된 sql 데이터 형식으로 변환 합니다. **CONVERT** 함수의 구문은  
  
 **CONVERT (** _value_exp_ **,** _data_type_**)**  
  
 여기서 *value_exp* 는 열 이름, 다른 스칼라 함수 또는 리터럴 값의 결과, *Data_type* 는 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)에 정의 된 대로 SQL 데이터 형식 식별자에 사용 되는 **#define** 이름과 일치 하는 키워드입니다. 예를 들어 다음 SQL 문은 **CONVERT** 함수를 사용 하 여 **curdate** 함수의 출력이 타임 스탬프 또는 문자 데이터가 아닌 날짜 인지 확인 합니다.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 데이터 소스에서 지원 되는 스칼라 함수를 확인 하기 위해 응용 프로그램은 SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS 및 SQL_TIMEDATE_FUNCTIONS 옵션을 사용 하 여 **SQLGetInfo** 를 호출 합니다. **CONVERT** 함수에서 지원 되는 변환 연산을 확인 하기 위해 응용 프로그램은 SQL_CONVERT로 시작 하는 옵션 중 하나를 사용 하 여 **SQLGetInfo** 를 호출 합니다.
