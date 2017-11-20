---
title: "Date, Time 및 Timestamp 리터럴 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2af859a38f288507ad87564cfbbfffa2b8f6ecf8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="date-time-and-timestamp-literals"></a>Date, Time 및 Timestamp 리터럴
날짜, 시간 및 타임 스탬프 리터럴에 대 한 이스케이프 시퀀스는  
  
 **{***-형식* **'** *값* **'을 (를)**   
  
 여기서 *리터럴 형식이* 값 중 하나는 다음 표에 나열 됩니다.  
  
|*리터럴 형식*|의미|서식을 지정 *값*|  
|---------------------|-------------|-----------------------|  
|**d**|날짜|*yyyy*-*mm*-*dd*|  
|**t**|시간 *|*hh*:*mm*:*ss*[1]|  
|**ts**|타임스탬프|*yyyy*-*mm*-*dd* *hh*:*mm*:*ss* [. *f...* ] [1]|  
  
 [초 구성 요소가 포함 된 리터럴 시간 또는 타임 스탬프 간격에서 소수점 오른쪽 자릿수입니다 1 수는 SQL_DESC_PRECISION 설명자 필드에 포함 된 초 전체 자릿수에 따라 다릅니다. (자세한 내용은 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 날짜, 시간 및 타임 스탬프 이스케이프 시퀀스에 대 한 자세한 내용은 참조 [날짜, 시간 및 타임 스탬프 이스케이프 시퀀스](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) 부록 c: SQL 문법에 있습니다.  
  
 예를 들어 다음 SQL 문을 모두 Orders 테이블의 판매 주문 1023의 시작 날짜를 업데이트합니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용합니다. 두 번째 문은 날짜 열에 대 한 Oracle Rdb 기본 구문을 사용 하 고 상호 운용 되지 않습니다.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 또한 날짜, 시간 또는 리터럴 타임 스탬프에 대 한 이스케이프 시퀀스는 날짜, 시간 또는 타임 스탬프 매개 변수를 바인딩할 문자 변수에서 저장할 수 있습니다. 예를 들어 다음 코드는 문자 변수에 바인딩된 날짜 매개 변수를 사용 하 여 Orders 테이블의 판매 주문 1023의 시작 날짜를 업데이트 하려면:  
  
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
  
 그러나 날짜 구조에 직접 매개 변수를 바인딩하기 위해 일반적으로 더 효율적입니다.  
  
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
  
 응용 프로그램이 호출을 하는 드라이버 날짜, 시간 또는 타임 스탬프 리터럴에 대 한 ODBC 이스케이프 시퀀스를 지원 하는지 확인 하려면 **SQLGetTypeInfo**합니다. 데이터 원본에서 날짜, 시간 또는 타임 스탬프 데이터 형식의 지 원하는 경우 또한 해당 이스케이프 시퀀스를 지원 해야 합니다.  
  
 데이터 원본에는 날짜, 시간 또는 타임 스탬프 리터럴에 대 한 ODBC 이스케이프 시퀀스와에서 다르면는 ANSI sql-92 사양에 정의 된 날짜/시간 리터럴도 지원할 수 있습니다. 데이터 소스에 ANSI 리터럴을 지원 여부를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 옵션을 사용 합니다.  
  
 응용 프로그램이 호출을 드라이버 간격 리터럴에 대 한 ODBC 이스케이프 시퀀스를 지원 하는지 여부를 확인 하려면 **SQLGetTypeInfo**합니다. 데이터 원본에서 날짜/시간 간격 데이터 형식의 지 원하는 경우 또한 해당 이스케이프 시퀀스를 지원 해야 합니다.  
  
 데이터 원본에서 날짜/시간 간격 리터럴에 대 한 ODBC 이스케이프 시퀀스는 ANSI sql-92 사양에 정의 된 날짜/시간 리터럴도 지원할 수 있습니다. 데이터 소스에 ANSI 리터럴을 지원 여부를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 옵션을 사용 합니다.

