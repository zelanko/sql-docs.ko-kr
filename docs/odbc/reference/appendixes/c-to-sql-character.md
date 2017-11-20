---
title: "C에서 SQL로: 문자 | Microsoft Docs"
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
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8d6ab676fc351afd7819c1fe60d59a58bfe7207
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-character"></a>C에서 SQL로: 문자
ODBC C 데이터 형식 문자에 대 한 식별자는.  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 다음 표에서 ODBC SQL 데이터 형식을 C 문자 데이터가 변환 될 수 있습니다는 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
> [!NOTE]  
>  C 문자 데이터가 유니코드 SQL 데이터 변환 되 면 유니코드 데이터의 길이 짝수 여야 합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|데이터의 바이트 길이 < = 열 길이입니다.<br /><br /> 데이터의 바이트 길이 > 열 길이입니다.|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|문자 데이터의 길이 < = 열 길이입니다.<br /><br /> 문자 데이터의 길이 > 열 길이입니다.|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|데이터 잘림 없이 변환<br /><br /> 데이터 잘림 [e] 소수 자릿수로 변환<br /><br /> 데이터 변환 [e] \(소수) 대비 전체 자릿수 손실 될 수 있습니다.<br /><br /> 데이터 값이는 *숫자 리터럴*|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|숫자를 변환 하는 데이터 형식 범위 내에서 데이터를<br /><br /> 데이터는 숫자를 변환 하는 데이터 형식의 범위를 벗어납니다.<br /><br /> 데이터 값이는 *숫자 리터럴*|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|데이터는 0 또는 1<br /><br /> 데이터 0, 2, 보다 작음 및 1과 같지 않은 보다 큽니다.<br /><br /> 데이터는 0 보다 작거나 또는 2 보다 크거나<br /><br /> 데이터를 한 *숫자 리터럴*|n/a<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(데이터의 바이트 길이) / 2 < = 바이트 길이 열<br /><br /> (데이터의 바이트 길이) / 2 > 열의 바이트 길이<br /><br /> 데이터 값이 16 진수 값|n/a<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|데이터 값은 올바른 *ODBC 날짜 리터럴*<br /><br /> 데이터 값은 올바른 *ODBC 타임 스탬프 리터럴*; 시간 부분은 0<br /><br /> 데이터 값은 올바른 *ODBC 타임 스탬프 리터럴*; 시간 부분을 0이 아닌 [a]<br /><br /> 데이터 값이 유효한 *ODBC 날짜 리터럴* 또는 *ODBC 타임 스탬프 리터럴*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|데이터 값은 올바른 *ODBC 시간 리터럴*<br /><br /> 데이터 값은 올바른 *ODBC 타임 스탬프 리터럴*; 소수 자릿수 초 부분은 0 [b]<br /><br /> 데이터 값은 올바른 *ODBC 타임 스탬프 리터럴*; 소수 자릿수 초 부분을 0이 아닌 [b]<br /><br /> 데이터 값이 유효한 *ODBC 시간 리터럴* 또는 *ODBC 타임 스탬프 리터럴*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|데이터 값은 올바른 *ODBC 타임 스탬프 리터럴*; 소수 자릿수 초 부분 잘리지<br /><br /> 데이터 값은 올바른 *ODBC 타임 스탬프 리터럴*; 소수 자릿수 초 부분 잘립니다<br /><br /> 데이터 값은 올바른 *ODBC 날짜 리터럴*[c + +]<br /><br /> 데이터 값은 올바른 *ODBC 시간 리터럴*[d]<br /><br /> 데이터 값이 유효한 *ODBC 날짜 리터럴*, *ODBC 시간 리터럴*, 또는 *ODBC 타임 스탬프 리터럴*|n/a<br /><br /> 22008<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|모든 SQL 간격 유형|데이터 값은 올바른 *간격 값*; 잘림을 방지<br /><br /> 데이터 값은 올바른 *간격 값*; 필드 중 하나에 해당 값이 잘립니다<br /><br /> 데이터 값이 리터럴 유효한 간격을|n/a<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 타임 스탬프의 시간 부분 잘립니다.  
  
 [타임 스탬프의 b]에서 날짜 부분은 무시 됩니다.  
  
 [c] 타임 스탬프의 시간 부분을 0으로 설정 됩니다.  
  
 [d] 타임 스탬프의 날짜 부분을 현재 날짜로 설정 됩니다.  
  
 [e] 드라이버/데이터 원본에서 효과적으로 전체 문자열 수신 될 때까지 대기 (문자 데이터가 조각을 호출 하 여 전송 하는 경우에 **SQLPutData**) 변환을 수행 하기 전에.  
  
 C 문자 데이터가 변환 된 숫자, 날짜, 시간 또는 타임 스탬프 SQL 데이터 이면 선행 및 후행 공백을 무시 됩니다.  
  
 C 문자 데이터는 이진 SQL 데이터 변환 되 면 각 2 바이트 문자 데이터의 이진 데이터의 단일 바이트 (8 비트)으로 변환 됩니다. 문자 데이터의 각 2 바이트의 16 진수 숫자를 나타냅니다. 예를 들어 "01"은 이진 00000001 변환 하 고 "FF" 이진 11111111으로 변환 됩니다.  
  
 드라이버는 항상 개별 바이트 16 진수 숫자의 쌍으로 변환 하 고 null 종료 바이트를 무시 합니다. 이 인해 문자열의 길이가 홀수 이면 문자열 (null 종료 바이트 제외)의 마지막 바이트 변환 되지 않습니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 C 문자 데이터를 이진 SQL 데이터 형식에 바인딩 해서는 안 됩니다. 이 변환은 일반적으로 비효율적인 및 느립니다.

