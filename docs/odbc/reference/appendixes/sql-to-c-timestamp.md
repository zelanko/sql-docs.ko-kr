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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296353"
---
# <a name="sql-to-c-timestamp"></a>SQL에서 C로: 타임스탬프

Timestamp ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.

- SQL_TYPE_TIMESTAMP  

다음 표에서는 타임 스탬프 SQL 데이터를 변환 하는 데 사용할 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  

|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 문자 바이트 길이입니다.<br /><br /> 20 <= *bufferlength* <= 문자 바이트 길이<br /><br /> *Bufferlength* < 20|데이터<br /><br /> 잘린 데이터 [b]<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Bufferlength* > 문자 길이입니다.<br /><br /> 20 <= *bufferlength* <= 문자 길이<br /><br /> *Bufferlength* < 20|데이터<br /><br /> 잘린 데이터 [b]<br /><br /> 정의되지 않음|데이터의 길이 (문자)<br /><br /> 데이터의 길이 (문자)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_TYPE_DATE|타임 스탬프의 시간 부분이 0 [a]입니다.<br /><br /> 타임 스탬프의 시간 부분은 0이 아닙니다. [a]|데이터<br /><br /> 잘린 데이터 [c]|6 [f]<br /><br /> 6 [f]|해당 없음<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|타임 스탬프의 초 소수 부분이 0 [a]입니다.<br /><br /> Timestamp의 소수 자릿수 초 부분은 0이 아닙니다. [a]|데이터 [d]<br /><br /> 잘린 데이터 [d], [e]|6 [f]<br /><br /> 6 [f]|해당 없음<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|타임 스탬프의 초 소수 부분이 잘리지 않습니다 [a]<br /><br /> 타임 스탬프의 초 소수 부분이 잘렸습니다 [a]|데이터 [e]<br /><br /> 잘린 데이터 [e]|16 [f]<br /><br /> 16 [f]|해당 없음<br /><br /> 01S07|  

 [a]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [b] 타임 스탬프의 소수 자릿수 초는 잘립니다.  
  
 [c] 타임 스탬프의 시간 부분이 잘립니다.  
  
 [d] 타임 스탬프의 날짜 부분은 무시 됩니다.  
  
 [e] 타임 스탬프의 초 소수 부분을 자릅니다.  
  
 [f] 해당 C 데이터 형식의 크기입니다.  

Timestamp SQL 데이터가 문자 C 데이터로 변환 되는 경우 결과 문자열은 "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.* f ...*] " 형식. 소수 자릿수 초에는 최대 9 자리 숫자를 사용할 수 있습니다. 이 형식은 Windows® country 설정의 영향을 받지 않습니다. (소수점 및 소수 자릿수 초를 제외 하 고, timestamp SQL 데이터 형식의 전체 자릿수에 관계 없이 전체 형식을 사용 해야 합니다.)
