---
title: 'C에서 SQL로: 타임스탬프 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3102e5043527a1aa9463980c9dd546839cb92f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283753"
---
# <a name="c-to-sql-timestamp"></a>C에서 SQL로: 타임스탬프
타임스탬프 ODBC C 데이터 형식의 식별자는 다음과 입니다.  
  
 SQL_C_TYPE_TIMESTAMP  
  
 다음 표에서는 타임스탬프 C 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열 바이트 길이 >= 문자 바이트 길이<br /><br /> 19 <= 열 바이트 길이 < 문자 바이트 길이<br /><br /> 열 바이트 길이 < 19<br /><br /> 데이터 값이 유효한 타임스탬프가 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열 문자 길이 >= 데이터의 문자 길이<br /><br /> 19 <= 데이터의 문자 길이< 열 문자 길이<br /><br /> 열 문자 길이 < 19<br /><br /> 데이터 값이 유효한 타임스탬프가 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|시간 필드는 0입니다.<br /><br /> 시간 필드가 영하지 않습니다.<br /><br /> 데이터 값에 유효한 날짜가 포함되지 않음|해당 없음<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|분수 초 필드는 0[a]<br /><br /> 분수 초 필드는 영하가 아닙니다[a]<br /><br /> 데이터 값에 유효한 시간이 포함되어 있지 않습니다.|해당 없음<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|분수 초 필드는 잘리지 않습니다.<br /><br /> 분수 초 필드가 잘립니다.<br /><br /> 데이터 값이 유효한 타임스탬프가 아닙니다.|해당 없음<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 타임스탬프 구조의 날짜 필드는 무시됩니다.  
  
 SQL_C_TIMESTAMP 구조에서 유효한 값에 대한 자세한 내용은 이 부록의 이전 C [데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md)참조하십시오.  
  
 타임스탬프 C 데이터가 문자 SQL 데이터로 변환되면 결과 문자 데이터는 *"yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[에 있습니다.* f...* 형식.  
  
 드라이버는 타임스탬프 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시하고 데이터 버퍼의 크기가 타임스탬프 C 데이터 형식의 크기라고 가정합니다. 길이/표시기 값은 **SQLPutData의** *StrLen_or_Ind* 인수와 **SQLBindParameter**에서 *StrLen_or_IndPtr* 인수로 지정된 버퍼에서 전달됩니다. 데이터 버퍼는 **SQLPutData의** *DataPtr* 인수와 **SQLBind매개**변수 매개 변수의 *매개 변수 값 Ptr* 인수로 지정됩니다.
