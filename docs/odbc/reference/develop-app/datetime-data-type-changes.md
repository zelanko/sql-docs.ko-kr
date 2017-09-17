---
title: "Datetime 데이터 형식 변경 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b09a6daa19b7a8b22ac5f4b3147e6cefde6ffc60
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="datetime-data-type-changes"></a>날짜/시간 데이터 형식 변경
Odbc 3. *x*, 날짜에 대 한 식별자, SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP에서 time 및 timestamp SQL 데이터 형식 변경 (의 인스턴스와 **#define** 9, 10 및 11의 헤더 파일에서)를 통해 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP (의 인스턴스와 **#define** 91이 고, 92, 및 93 헤더 파일에), 각각. 해당 C 형식 식별자는 각각 SQL_C_TYPE_DATE, SQL_C_TYPE_TIME, 및 SQL_C_TYPE_TIMESTAMP, SQL_C_DATE, SQL_C_TIME, 및 SQL_C_TIMESTAMP에서 변경 되었습니다.  
  
 열 크기 및 소수 자릿수를 ODBC 3에서 SQL 날짜/시간 데이터 형식에 대해 반환 합니다. *x* 는 ODBC 2에서에 반환 되는 자릿수와 소수 자릿수와 동일 합니다.* x*합니다. 이러한 값은 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. (자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 이러한 변경에 영향을 **SQLDescribeCol**, **SQLDescribeParam**, 및 **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, 및 **SQLGetData**; 및 **SQLColumns**, **SQLGetTypeInfo **, **SQLProcedureColumns**, **SQLStatistics**, 및 **SQLSpecialColumns**합니다.  
  
 다음 표는 ODBC 3*.x* 드라이버 관리자에 입력 된 날짜, 시간 및 타임 스탬프 C 데이터 형식 매핑 수행는 *TargetType* 의 인수 **SQLBindCol**및 **SQLGetData** 또는 *ValueType* 의 인수 **SQLBindParameter**합니다.  
  
|데이터 형식<br /><br /> 입력 한 코드|2.*x* 앱을<br /><br /> 2.*x* 드라이버|2.*x* 앱을<br /><br /> 3.*x* 드라이버|3.*x* 앱을<br /><br /> 2.*x* 드라이버|3.*x* 앱을<br /><br /> 3.*x* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|매핑되지 않습니다|SQL_C_TYPE_DATE (91)|매핑이 없습니다 [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|오류 (DM)에서|오류 (DM)에서|SQL_C_DATE (9)|매핑이 없는 [2]|  
|SQL_C_TIME (10)|매핑되지 않습니다|SQL_C_TYPE_TIME (92)|매핑이 없습니다 [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|오류 (DM)에서|오류 (DM)에서|SQL_C_TIME (10)|매핑이 없는 [2]|  
|SQL_C_TIMESTAMP (11)|매핑되지 않습니다|SQL_C_TYPE_TIMESTAMP (93)|매핑이 없습니다 [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|오류 (DM)에서|오류 (DM)에서|SQL_C_TIMESTAMP (11)|매핑이 없는 [2]|  
  
 [1]의 결과로이 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2.* x* 카탈로그 함수에서 반환 되는 결과 집합에서 반환 되는 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.  
  
 [2]의 결과로이 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 3.* x* 카탈로그 함수에서 반환 되는 결과 집합에서 반환 되는 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.  
  
 다음 표는 ODBC 3*.x* 드라이버 관리자에 입력 된 날짜, 시간 및 타임 스탬프 SQL 데이터 형식 매핑 수행는 *ParameterType* 의 인수 **SQLBindParameter ** 또는 *DataType* 의 인수 **SQLGetTypeInfo**합니다.  
  
|데이터 형식<br /><br /> 입력 한 코드|2.*x* 앱을<br /><br /> 2.*x* 드라이버|2.*x* 앱을<br /><br /> 3.*x* 드라이버|3.*x* 앱을<br /><br /> 2.*x* 드라이버|3.*x* 앱을<br /><br /> 3.*x* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|경우 SQL_DATE (9)|매핑되지 않습니다|SQL_TYPE_DATE(91)|매핑이 없습니다 [1]|SQL_TYPE_DATE(91)|  
|SQL_TYPE_DATE(91)|오류 (DM)에서|오류 (DM)에서|경우 SQL_DATE (9)|매핑이 없는 [2]|  
|경우 SQL_TIME (10)|매핑되지 않습니다|SQL_TYPE_TIME (92)|매핑이 없습니다 [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|오류 (DM)에서|오류 (DM)에서|경우 SQL_TIME (10)|매핑이 없는 [2]|  
|SQL_TIMESTAMP (11)|매핑되지 않습니다|SQL_TYPE_TIMESTAMP(93)|매핑이 없습니다 [1]|SQL_TYPE_TIMESTAMP(93)|  
|SQL_TYPE_TIMESTAMP(93)|오류 (DM)에서|오류 (DM)에서|SQL_TIMESTAMP (11)|매핑이 없는 [2]|  
  
 [1]의 결과로이 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2.* x* 카탈로그 함수에서 반환 되는 결과 집합에서 반환 되는 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.  
  
 [2]의 결과로이 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 3.* x* 카탈로그 함수에서 반환 되는 결과 집합에서 반환 되는 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.
