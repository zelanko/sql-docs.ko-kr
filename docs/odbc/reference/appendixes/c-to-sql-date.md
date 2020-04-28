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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa3df8aaee03472076b3241cb9bb60e2a307e28b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298851"
---
# <a name="c-to-sql-date"></a>C에서 SQL로: 날짜
ODBC C 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_C_TYPE_DATE  
  
 다음 표에서는 날짜 C 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열 바이트 길이 >= 10<br /><br /> 열 바이트 길이 < 10<br /><br /> 데이터 값이 올바른 날짜가 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열 문자 길이 >= 10<br /><br /> 열 문자 길이 < 10<br /><br /> 데이터 값이 올바른 날짜가 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|데이터 값이 유효한 날짜입니다.<br /><br /> 데이터 값이 올바른 날짜가 아닙니다.|해당 없음<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|데이터 값이 유효한 날짜 [a]입니다.<br /><br /> 데이터 값이 올바른 날짜가 아닙니다.|해당 없음<br /><br /> 22007|  
  
 [a] 타임 스탬프의 시간 부분은 0으로 설정 됩니다.  
  
 SQL_C_TYPE_DATE 구조에서 유효한 값에 대 한 자세한 내용은이 부록 앞부분의 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)을 참조 하세요.  
  
 날짜 C 데이터가 문자 SQL 데이터로 변환 되 면 결과 문자 데이터는 "*yyyy*-*mm*-*dd*" 형식입니다.  
  
 날짜 C 데이터 형식에서 데이터를 변환할 때 드라이버는 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 날짜 C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
