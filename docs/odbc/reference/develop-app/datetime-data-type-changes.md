---
title: 일시적 데이터 유형 변경 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f186047dd31aa2c4b66ec1ce73c8cb9fae31c04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304646"
---
# <a name="datetime-data-type-changes"></a>날짜/시간 데이터 형식 변경
ODBC *3.x에서*날짜, 시간 및 타임스탬프 SQL 데이터 형식에 대한 식별자는 각각 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP(9, 10 및 11의 헤더 파일에 **#define** 인스턴스)에서 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP(헤더 파일의 **#define** 인스턴스 포함)으로 각각 변경되었습니다. 해당 C 유형 식별자가 각각 SQL_C_DATE, SQL_C_TIME 및 SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME 및 SQL_C_TYPE_TIMESTAMP 변경되었습니다.  
  
 ODBC *3.x의* SQL datetime 데이터 형식에 대해 반환되는 열 크기와 소수 자릿수는 ODBC *2.x에서*반환되는 정밀도 및 배율과 동일합니다. 이러한 값은 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. 자세한 내용은 열 [크기, 소수 자릿수, 옥텟 길이 전송 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.  
  
 이러한 변경 사항은 **SQLDescribeCol,** **SQLDescribeParam**및 **SQLColAttribute에**영향을 미칩니다. **SQLBindCol**, **SQLBind매개 변수**및 **SQLGetData**; 및 **SQLColumns,** **SQLGetTypeInfo,** **SQLProcedure열,** **SQLStatistics**및 **SQLSpecialColumns**.  
  
 다음 표에서는 ODBC *3.x* 드라이버 관리자가 **SQLBindCol** 및 **SQLGetData의** *TargetType* 인수 또는 **SQLBindParameter의** *ValueType* 인수에 입력된 날짜, 시간 및 타임스탬프 C 데이터 형식의 매핑을 수행하는 방법을 보여 주며 있습니다.  
  
|데이터 형식<br /><br /> 입력한 코드|*2.x* 앱에서<br /><br /> *2.x* 드라이버|*2.x* 앱에서<br /><br /> *3.x* 드라이버|*3.x* 앱에서<br /><br /> *2.x* 드라이버|*3.x* 앱에서<br /><br /> *3.x* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|매핑 없음|SQL_C_TYPE_DATE (91)|매핑 없음[1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|오류(DM에서)|오류(DM에서)|SQL_C_DATE (9)|매핑 없음[2]|  
|SQL_C_TIME (10)|매핑 없음|SQL_C_TYPE_TIME (92)|매핑 없음[1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|오류(DM에서)|오류(DM에서)|SQL_C_TIME (10)|매핑 없음[2]|  
|SQL_C_TIMESTAMP (11)|매핑 없음|SQL_C_TYPE_TIMESTAMP (93)|매핑 없음[1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|오류(DM에서)|오류(DM에서)|SQL_C_TIMESTAMP (11)|매핑 없음[2]|  
  
 [1] 결과적으로 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램은 카탈로그 함수에서 반환되는 결과 집합에서 반환되는 날짜, 시간 또는 타임스탬프 코드를 사용할 수 있습니다.  
  
 [2] 결과적으로 ODBC *3.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램은 카탈로그 함수에서 반환되는 결과 집합에서 반환되는 날짜, 시간 또는 타임스탬프 코드를 사용할 수 있습니다.  
  
 다음 표에서는 ODBC *3.x* 드라이버 관리자가 **SQLBindParameter의** *ParameterType* 인수 또는 **SQLGetTypeInfo의** *DataType* 인수에 입력된 날짜, 시간 및 타임스탬프 SQL 데이터 형식의 매핑을 수행하는 방법을 보여 주며 있습니다.  
  
|데이터 형식<br /><br /> 입력한 코드|*2.x* 앱에서<br /><br /> *2.x* 드라이버|*2.x* 앱에서<br /><br /> *3.x* 드라이버|*3.x* 앱에서<br /><br /> *2.x* 드라이버|*3.x* 앱에서<br /><br /> *3.x* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|매핑 없음|SQL_TYPE_DATE(91)|매핑 없음[1]|SQL_TYPE_DATE(91)|  
|SQL_TYPE_DATE(91)|오류(DM에서)|오류(DM에서)|SQL_DATE (9)|매핑 없음[2]|  
|SQL_TIME (10)|매핑 없음|SQL_TYPE_TIME (92)|매핑 없음[1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|오류(DM에서)|오류(DM에서)|SQL_TIME (10)|매핑 없음[2]|  
|SQL_TIMESTAMP (11)|매핑 없음|SQL_TYPE_TIMESTAMP(93)|매핑 없음[1]|SQL_TYPE_TIMESTAMP(93)|  
|SQL_TYPE_TIMESTAMP(93)|오류(DM에서)|오류(DM에서)|SQL_TIMESTAMP (11)|매핑 없음[2]|  
  
 [1] 결과적으로 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램은 카탈로그 함수에서 반환되는 결과 집합에서 반환되는 날짜, 시간 또는 타임스탬프 코드를 사용할 수 있습니다.  
  
 [2] 결과적으로 ODBC *3.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램은 카탈로그 함수에서 반환되는 결과 집합에서 반환되는 날짜, 시간 또는 타임스탬프 코드를 사용할 수 있습니다.
