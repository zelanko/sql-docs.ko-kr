---
title: 'SQL에서 C까지: 시간 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296383"
---
# <a name="sql-to-c-time"></a>SQL에서 C로: 시간
ODBC SQL 데이터 형식의 식별자는 다음과 입니다.  
  
 SQL_TYPE_TIME  
  
 다음 표에서는 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며, 이 형식은 다음과 같은 것입니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  
  
|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*버퍼길이* > 문자 바이트 길이<br /><br /> *9* <= *버퍼길이* <= 문자 바이트 길이<br /><br /> *버퍼길이* < 9|데이터<br /><br /> 잘린 데이터[a]<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*버퍼길이* > 문자 길이<br /><br /> *9* <= *버퍼길이* <= 문자 길이<br /><br /> *버퍼길이* < 9|데이터<br /><br /> 잘린 데이터[a]<br /><br /> 정의되지 않음|문자로 된 데이터 길이<br /><br /> 문자로 된 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_TYPE_TIME|없음[b]|데이터|6[d]|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|없음[b]|데이터[c]|16[d]|해당 없음|  
  
 [a] 시간의 소수 초가 잘립니다.  
  
 [b] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [c] 타임스탬프 구조의 날짜 필드가 현재 날짜로 설정되고 타임스탬프 구조의 분수 초 필드가 0으로 설정됩니다.  
  
 [d] 해당 C 데이터 형식의 크기입니다.  
  
 시간 SQL 데이터가 문자 C 데이터로 변환되면 결과 문자열은 *"hh*:*mm*:*ss*" 형식입니다. 이 형식은 Windows® 국가 설정의 영향을 받지 않습니다.
