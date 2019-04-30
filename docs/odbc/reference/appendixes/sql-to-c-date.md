---
title: 'SQL에서 C로: 날짜 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe0c30f0f0fbf0ea695d79387fdec3694a54ebca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151269"
---
# <a name="sql-to-c-date"></a>SQL에서 C로: Date
ODBC SQL 데이터 형식은 날짜에 대 한 식별자:  
  
 SQL_TYPE_DATE  
  
 다음 표에서 ODBC C 데이터 형식에는 날짜 SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 문자 바이트 길이<br /><br /> 11 < = *BufferLength* < = 문자 바이트 길이<br /><br /> *BufferLength* < 11|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|10<br /><br /> 데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 문자 길이<br /><br /> 11 < = *BufferLength* < = 문자 길이<br /><br /> *BufferLength* < 11|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|10<br /><br /> 문자에서 데이터의 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|[A] 없음|data|6[c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|[A] 없음|데이터 [b]|16[c]|n/a|  
  
 [a] 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버 가정 크기 **TargetValuePtr* C 데이터 형식의 크기입니다.  
  
 [b] 타임 스탬프 구조체의 시간 필드는 0으로 설정 됩니다.  
  
 [c] C 데이터 형식에 해당 크기입니다.  
  
 결과 문자열은 날짜 SQL 데이터 C 문자 데이터를 변환할 때에 "*yyyy*-*mm*-*dd*" 형식입니다. 이 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.
