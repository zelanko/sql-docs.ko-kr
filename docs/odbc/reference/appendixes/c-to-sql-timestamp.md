---
title: 'C에서 SQL로: 타임 스탬프 | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283753"
---
# <a name="c-to-sql-timestamp"></a>C에서 SQL로: 타임스탬프
Timestamp ODBC C 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_C_TYPE_TIMESTAMP  
  
 다음 표에서는 타임 스탬프 C 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열 바이트 길이 >= 문자 바이트 길이<br /><br /> 19 <= 열 바이트 길이 < 문자 바이트 길이<br /><br /> 열 바이트 길이 < 19<br /><br /> 데이터 값이 유효한 타임 스탬프가 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열 문자 길이 >= 데이터의 문자 길이<br /><br /> 19 <= 열 문자 길이 < 데이터의 문자 길이<br /><br /> 열 문자 길이 < 19<br /><br /> 데이터 값이 유효한 타임 스탬프가 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|시간 필드가 0입니다.<br /><br /> 시간 필드가 0이 아닙니다.<br /><br /> 데이터 값에 올바른 날짜가 포함 되어 있지 않습니다.|해당 없음<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|초 소수 필드는 0 [a]입니다.<br /><br /> 소수 자릿수 초 필드는 0이 아닙니다. [a]<br /><br /> 데이터 값에 유효한 시간이 포함 되어 있지 않습니다.|해당 없음<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|소수 자릿수 초 필드는 잘리지 않습니다.<br /><br /> 소수 자릿수 초 필드가 잘렸습니다.<br /><br /> 데이터 값이 유효한 타임 스탬프가 아닙니다.|해당 없음<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 타임 스탬프 구조의 날짜 필드는 무시 됩니다.  
  
 SQL_C_TIMESTAMP 구조에서 유효한 값에 대 한 자세한 내용은이 부록 앞부분의 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)을 참조 하세요.  
  
 타임 스탬프 C 데이터가 문자 SQL 데이터로 변환 되 면 결과 문자 데이터는 "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.* f ...*] " 형식과.  
  
 Timestamp C 데이터 형식에서 데이터를 변환할 때 드라이버는 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 타임 스탬프 C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
