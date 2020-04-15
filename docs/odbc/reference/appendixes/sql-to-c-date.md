---
title: 'SQL에서 C까지: 날짜 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe9656c0c02c0ff5a10029525da3d38280530cc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296533"
---
# <a name="sql-to-c-date"></a>SQL에서 C로: 날짜
ODBC SQL 데이터 형식날짜의 식별자는 다음과 같은 것입니다.  
  
 SQL_TYPE_DATE  
  
 다음 표에서는 SQL 데이터를 변환할 수 있는 날짜의 ODBC C 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  
  
|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*버퍼길이* > 문자 바이트 길이<br /><br /> 11 <= *버퍼길이* <= 문자 바이트 길이<br /><br /> *버퍼길이* < 11|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|10<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*버퍼길이* > 문자 길이<br /><br /> 11 <= *버퍼길이* <= 문자 길이<br /><br /> *버퍼길이* < 11|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|10<br /><br /> 문자로 된 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_TYPE_DATE|없음[a]|데이터|6[c]|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|없음[a]|데이터[b]|16[c]|해당 없음|  
  
 [a] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [b] 타임스탬프 구조의 시간 필드가 0으로 설정됩니다.  
  
 [c] 해당 C 데이터 형식의 크기입니다.  
  
 날짜 SQL 데이터가 문자 C 데이터로 변환되면 결과 문자열은 *"yyyy*-*mm*-*dd"* 형식입니다. 이 형식은 Windows® 국가 설정의 영향을 받지 않습니다.
