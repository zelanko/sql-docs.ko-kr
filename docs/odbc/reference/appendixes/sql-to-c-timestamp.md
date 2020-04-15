---
title: 'SQL에서 C까지: 타임스탬프 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296353"
---
# <a name="sql-to-c-timestamp"></a>SQL에서 C로: 타임스탬프

타임스탬프 ODBC SQL 데이터 형식의 식별자는 다음과 같은 것입니다.

- SQL_TYPE_TIMESTAMP  

다음 표에서는 타임스탬프 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  

|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*버퍼길이* > 문자 바이트 길이<br /><br /> 20 <= *버퍼길이* <= 문자 바이트 길이<br /><br /> *버퍼길이* < 20|데이터<br /><br /> 잘린 데이터[b]<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*버퍼길이* > 문자 길이<br /><br /> 20 <= *버퍼길이* <= 문자 길이<br /><br /> *버퍼길이* < 20|데이터<br /><br /> 잘린 데이터[b]<br /><br /> 정의되지 않음|문자로 된 데이터 길이<br /><br /> 문자로 된 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_TYPE_DATE|타임스탬프의 시간 부분은 0[a]<br /><br /> 타임스탬프의 시간 부분이 영해가 아닙니다[a]|데이터<br /><br /> 잘린 데이터[c]|6[f]<br /><br /> 6[f]|해당 없음<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|타임스탬프의 분수 초 부분은 0[a]<br /><br /> 타임스탬프의 분수 초 부분은 영하가 아닙니다[a]|데이터[d]<br /><br /> 잘린 데이터[d], [e]|6[f]<br /><br /> 6[f]|해당 없음<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|타임스탬프의 분수 초 부분이 잘리지 않습니다[a]<br /><br /> 타임스탬프의 분수 초 부분이 잘립니다[a]|데이터[e]<br /><br /> 잘린 데이터[e]|16[f]<br /><br /> 16[f]|해당 없음<br /><br /> 01S07|  

 [a] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [b] 타임스탬프의 소수 초가 잘립니다.  
  
 [c] 타임스탬프의 시간 부분이 잘립니다.  
  
 [d] 타임스탬프의 날짜 부분은 무시됩니다.  
  
 [e] 타임스탬프의 소수 초 부분이 잘립니다.  
  
 [f] 해당 C 데이터 형식의 크기입니다.  

타임스탬프 SQL 데이터가 문자 C 데이터로 변환되면 결과 문자열은 *"yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[에 있습니다.* f...* 최대 9자리 숫자를 분수 초 동안 사용할 수 있습니다. 이 형식은 Windows® 국가 설정의 영향을 받지 않습니다. 소수점과 분수 초를 제외하고 타임스탬프 SQL 데이터 형식의 정밀도에 관계없이 전체 형식을 사용해야 합니다.
