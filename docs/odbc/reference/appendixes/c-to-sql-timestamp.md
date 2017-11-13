---
title: "C에서 SQL로: 타임 스탬프 | Microsoft Docs"
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
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bbb6396dc1a49d984834ec6f105b3a9ba42d95c4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-timestamp"></a>C에서 SQL로: 타임 스탬프
다음은 timestamp ODBC C 데이터 형식에 대 한 식별자가입니다.  
  
 SQL_C_TYPE_TIMESTAMP  
  
 다음 표에서 ODBC SQL 데이터 형식에는 타임 스탬프 C 데이터를 변환 될 수 있습니다를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열의 바이트 길이 > = 문자 바이트 길이<br /><br /> 19 < 열 바이트 길이 = < 문자 바이트 길이<br /><br /> 열의 바이트 길이 < 19<br /><br /> 데이터 값이 유효한 타임 스탬프|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열의 문자 길이 > = 데이터의 문자 길이<br /><br /> 19 < 열 문자 길이 = < 문자 데이터의 길이<br /><br /> 열 길이 < 19 문자<br /><br /> 데이터 값이 유효한 타임 스탬프|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|시간 필드가 0<br /><br /> 시간 필드가 0이 아닌<br /><br /> 데이터 값에는 유효한 날짜|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|소수 자릿수 초 필드가 0이 [a]<br /><br /> 소수 자릿수 초 필드는 0이 아닌 [a]<br /><br /> 데이터 값이 유효한 시간을 포함 하지 않습니다.|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|소수 자릿수 초 필드가 잘리지 않습니다.<br /><br /> 소수 자릿수 초 필드가 잘립니다.<br /><br /> 데이터 값이 유효한 타임 스탬프|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 날짜 타임 스탬프 구조 필드가 무시 됩니다.  
  
 SQL_C_TIMESTAMP 구조에서 유효한 값에 대 한 정보를 참조 하십시오. [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md)이 부록 앞부분에 나오는 합니다.  
  
 결과 문자 데이터에는 C 타임 스탬프 데이터를 문자 SQL 데이터로 변환 되 면는 "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[. *f...* ] "형식입니다.  
  
 드라이버 타임 스탬프 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기 C 타임 스탬프 데이터 형식의 크기 있다고 가정 합니다. 에 길이/표시기 값이 전달 되는 *StrLen_or_Ind* 인수 **SQLPutData** 및 지정 된 버퍼는 *StrLen_or_IndPtr* 인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼는 *DataPtr* 인수에 **SQLPutData** 및 *ParameterValuePtr* 인수에 **SQLBindParameter**.

