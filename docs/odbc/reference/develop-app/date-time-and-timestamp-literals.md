---
title: 날짜, 시간 및 타임스탬프 리터럴 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d899938be4689daab50a773f189219a797794006
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288299"
---
# <a name="date-time-and-timestamp-literals"></a>날짜, 시간, 타임스탬프 리터럴
날짜, 시간 및 타임스탬프 리터럴의 이스케이프 시퀀스는  
  
 **{**  _-type_ **'** _값_ **'}**  
  
 *여기서 리터럴 유형은* 다음 표에 나열된 값 중 하나입니다.  
  
|*리터럴 타입*|의미|*값의* 형식|  
|---------------------|-------------|-----------------------|  
|**D**|Date|*yyyy*-*mm*-*DD*|  
|**T**|시간*|*hh*:*mm*:*ss*[1]|  
|**Ts**|타임스탬프|*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*] [1]|  
  
 [1] 초 구성요소를 포함하는 시간 또는 타임스탬프 간격 리터럴의 소수점 오른쪽에 있는 자릿수는 SQL_DESC_PRECISION 설명자 필드에 포함된 바와 같이 초 정밀도에 의존한다. (자세한 내용은 [SQLSetDescField를](../../../odbc/reference/syntax/sqlsetdescfield-function.md)참조하십시오.)  
  
 날짜, 시간 및 타임스탬프 이스케이프 시퀀스에 대한 자세한 내용은 부록 C: SQL 문법의 [날짜, 시간 및 타임스탬프 이스케이프 시퀀스를](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) 참조하십시오.  
  
 예를 들어 다음 SQL 문은 모두 Orders 테이블에서 판매 주문 1023의 열린 날짜를 업데이트합니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용합니다. 두 번째 문은 DATE 열에 Oracle Rdb 네이티브 구문을 사용 하며 상호 운용 가능 하지 않습니다.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 날짜, 시간 또는 타임스탬프 리터럴에 대한 이스케이프 시퀀스를 날짜, 시간 또는 타임스탬프 매개 변수에 바인딩된 문자 변수에 배치할 수도 있습니다. 예를 들어 다음 코드는 문자 변수에 바인딩된 날짜 매개 변수를 사용하여 Orders 테이블에서 판매 주문 1023의 열린 날짜를 업데이트합니다.  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 그러나 일반적으로 매개 변수를 날짜 구조에 직접 바인딩하는 것이 더 효율적입니다.  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 드라이버가 날짜, 시간 또는 타임스탬프 리터럴에 대한 ODBC 이스케이프 시퀀스를 지원하는지 여부를 확인하려면 응용 프로그램이 **SQLGetTypeInfo**를 호출합니다. 데이터 원본이 날짜, 시간 또는 타임스탬프 데이터 형식을 지원하는 경우 해당 이스케이프 시퀀스도 지원해야 합니다.  
  
 데이터 원본은 날짜, 시간 또는 타임스탬프 리터럴에 대한 ODBC 이스케이프 시퀀스와 다른 ANSI SQL-92 사양에 정의된 날짜 시간 리터럴도 지원할 수 있습니다. 데이터 원본이 ANSI 리터럴을 지원하는지 여부를 확인하기 위해 응용 프로그램은 SQL_ANSI_SQL_DATETIME_LITERALS 옵션으로 **SQLGetInfo를** 호출합니다.  
  
 드라이버가 간격 리터럴에 대한 ODBC 이스케이프 시퀀스를 지원하는지 여부를 확인하기 위해 응용 프로그램은 **SQLGetTypeInfo**를 호출합니다. 데이터 원본이 날짜 간격 데이터 형식을 지원하는 경우 해당 이스케이프 시퀀스도 지원해야 합니다.  
  
 데이터 원본은 ANSI SQL-92 사양에 정의된 날짜 시간 리터럴을 지원할 수도 있으며, 이는 datetime 간격 리터럴에 대한 ODBC 이스케이프 시퀀스와 다릅니다. 데이터 원본이 ANSI 리터럴을 지원하는지 여부를 확인하기 위해 응용 프로그램은 SQL_ANSI_SQL_DATETIME_LITERALS 옵션으로 **SQLGetInfo를** 호출합니다.
