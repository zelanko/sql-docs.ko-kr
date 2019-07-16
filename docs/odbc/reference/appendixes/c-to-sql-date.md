---
title: 'C에서 SQL로: 날짜 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02ee7c1fb396dc1c9c0708cf6c0e7a52ff1c11ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019413"
---
# <a name="c-to-sql-date"></a>C에서 SQL로: Date
Date ODBC C 데이터 형식에 대 한 식별자가 있습니다.  
  
 SQL_C_TYPE_DATE  
  
 다음 표에서 ODBC SQL 데이터 형식에는 날짜 C 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)입니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열의 바이트 길이 > = 10<br /><br /> 열의 바이트 길이 < 10<br /><br /> 데이터 값을 유효한 날짜가 아닙니다.|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열의 문자 길이 > = 10<br /><br /> 열의 문자 길이 < 10<br /><br /> 데이터 값을 유효한 날짜가 아닙니다.|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|데이터 값이 유효한 날짜<br /><br /> 데이터 값을 유효한 날짜가 아닙니다.|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|데이터 값이 유효한 날짜 [a]<br /><br /> 데이터 값을 유효한 날짜가 아닙니다.|n/a<br /><br /> 22007|  
  
 [a] 타임 스탬프의 시간 부분은 0으로 설정 됩니다.  
  
 SQL_C_TYPE_DATE 구조에서 유효한 값에 대 한 정보를 참조 하세요 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)이 부록 앞부분입니다.  
  
 결과 문자 데이터는 날짜 C 데이터 문자 SQL 데이터를 변환할 때에 "*yyyy*-*mm*-*dd*" 형식입니다.  
  
 드라이버 날짜 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 C 날짜 데이터 형식의 크기를 가정 합니다. 길이/표시기 값이 전달 합니다 *StrLen_or_Ind* 인수에 **SQLPutData** 에 지정 된 버퍼는 *StrLen_or_IndPtr* 에서인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼를 *DataPtr* 에서 인수 **SQLPutData** 및 *ParameterValuePtr* 인수에서 **SQLBindParameter**.
