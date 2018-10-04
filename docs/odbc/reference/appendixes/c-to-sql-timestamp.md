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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a738712a8fb1b032ef8244f579b10fdcc22becee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739901"
---
# <a name="c-to-sql-timestamp"></a>C에서 SQL로: 타임스탬프
Timestamp ODBC C 데이터 형식에 대 한 식별자가 있습니다.  
  
 SQL_C_TYPE_TIMESTAMP  
  
 다음 표에서 ODBC SQL 데이터 형식에는 타임 스탬프 C 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)입니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열의 바이트 길이 > = 문자 바이트 길이<br /><br /> 19 < 열 바이트 길이 = < 문자 바이트 길이<br /><br /> 열의 바이트 길이 < 19<br /><br /> 데이터 값이 유효한 타임 스탬프|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열의 문자 길이 > 데이터의 문자 길이 =<br /><br /> 19 < 열 문자 길이 = < 문자 데이터의 길이<br /><br /> 열 길이 < 19 문자<br /><br /> 데이터 값이 유효한 타임 스탬프|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|시간 필드가 0<br /><br /> 시간 필드가 0이 아닌 값<br /><br /> 데이터 값에 유효한 날짜가 없습니다.|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|소수 자릿수 초 필드가 0이 [a]<br /><br /> 소수 자릿수 초 필드는 0이 아닌 [a]<br /><br /> 데이터 값을 유효한 시간을 포함 하지 않는|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|소수 자릿수 초 필드가 잘리지 않습니다.<br /><br /> 소수 자릿수 초 필드가 잘립니다.<br /><br /> 데이터 값이 유효한 타임 스탬프|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 날짜 타임 스탬프 구조체의 필드는 무시 됩니다.  
  
 SQL_C_TIMESTAMP 구조에서 유효한 값에 대 한 정보를 참조 하세요 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)이 부록 앞부분입니다.  
  
 결과 문자 데이터는 타임 스탬프 C 데이터 문자 SQL 데이터를 변환할 때에 "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.*f...*] "형식입니다.  
  
 드라이버 타임 스탬프 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기는 타임 스탬프 C 데이터 형식의 크기를 가정 합니다. 길이/표시기 값이 전달 합니다 *StrLen_or_Ind* 인수에 **SQLPutData** 에 지정 된 버퍼는 *StrLen_or_IndPtr* 에서인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼를 *DataPtr* 에서 인수 **SQLPutData** 및 *ParameterValuePtr* 인수에서 **SQLBindParameter**.
