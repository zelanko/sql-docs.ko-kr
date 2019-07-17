---
title: 'SQL에서 C로: 타임 스탬프 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee3852c688f495d54eb07ca9c2866ac17a1f5a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118839"
---
# <a name="sql-to-c-timestamp"></a>SQL에서 C로: 타임 스탬프

Timestamp ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.

- SQL_TYPE_TIMESTAMP  

다음 표에서 ODBC C 데이터 형식 타임 스탬프 SQL 데이터 변환할 수를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  

|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 문자 바이트 길이<br /><br /> 20 < = *BufferLength* < = 문자 바이트 길이<br /><br /> *BufferLength* < 20|data<br /><br /> 잘린된 데이터 [b]<br /><br /> Undefined|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이<br /><br /> Undefined|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 문자 길이<br /><br /> 20 < = *BufferLength* < = 문자 길이<br /><br /> *BufferLength* < 20|data<br /><br /> 잘린된 데이터 [b]<br /><br /> Undefined|문자에서 데이터의 길이<br /><br /> 문자에서 데이터의 길이<br /><br /> Undefined|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> Undefined|데이터의 바이트 길이<br /><br /> Undefined|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|타임 스탬프의 시간 부분은 0 [a]<br /><br /> 타임 스탬프의 시간 부분은 0이 아닌 [a]|data<br /><br /> 잘린된 데이터 [c]|6[f]<br /><br /> 6[f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|타임 스탬프의 초 소수 부분이 0 [a]<br /><br /> 타임 스탬프 부분 소수 자릿수 초는 0이 아닌 [a]|데이터 [d]<br /><br /> 잘린된 데이터 [d], [e]|6[f]<br /><br /> 6[f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|초 소수 부분 타임 스탬프는 잘리지 않습니다 [a]<br /><br /> 타임 스탬프의 초 소수 부분 잘립니다 [a]|데이터 [e]<br /><br /> 잘린된 데이터 [e]|16[f]<br /><br /> 16[f]|n/a<br /><br /> 01S07|  

 [a] 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버 가정 크기 **TargetValuePtr* C 데이터 형식의 크기입니다.  
  
 [b] 타임 스탬프의 소수 자릿수 초가 잘립니다.  
  
 [c] 타임 스탬프의 시간 부분은 잘립니다.  
  
 [타임 스탬프의 d]에서 날짜 부분은 무시 됩니다.  
  
 [e] 타임 스탬프의 초 소수 부분이 잘립니다.  
  
 [f] C 데이터 형식에 해당 크기입니다.  

결과 문자열은 타임 스탬프 SQL 데이터 C 문자 데이터를 변환할 때에 "*yyyy*-*mm*-*dd* *hh* :*mm*:*ss*[.*f...* ] "형식, 소수 자릿수 초에 대해 최대 9 자리 숫자를 사용할 수 있는 합니다. 이 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다. (소수점 및 소수 자릿수 초를 제외 하 고 전체 형식으로 사용 되어야 합니다, 타임 스탬프 SQL 데이터 형식의 전체 자릿수에 관계 없이.)
