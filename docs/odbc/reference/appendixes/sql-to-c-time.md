---
title: 'SQL에서 C로: 시간 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99f8219ef53f72b0d7ab1477bba5d24d441a3141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065078"
---
# <a name="sql-to-c-time"></a>SQL에서 C로: Time
ODBC SQL 데이터 형식은 시간에 대 한 식별자.  
  
 SQL_TYPE_TIME  
  
 다음 표에서 ODBC C 데이터 형식을 SQL time 데이터 변환 될 수 있습니다는 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 문자 바이트 길이<br /><br /> *9* <= *BufferLength* < = 문자 바이트 길이<br /><br /> *BufferLength* < 9|data<br /><br /> [A] 잘린된 데이터<br /><br /> Undefined|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이<br /><br /> Undefined|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 문자 길이<br /><br /> *9* <= *BufferLength* < = 문자 길이<br /><br /> *BufferLength* < 9|data<br /><br /> [A] 잘린된 데이터<br /><br /> Undefined|문자에서 데이터의 길이<br /><br /> 문자에서 데이터의 길이<br /><br /> Undefined|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> Undefined|데이터의 바이트 길이<br /><br /> Undefined|n/a<br /><br /> 22003|  
|SQL_C_TYPE_TIME|없음 [b]|data|6[d]|n/a|  
|SQL_C_TYPE_TIMESTAMP|없음 [b]|데이터 [c]|16[d]|n/a|  
  
 [a] 시간의 소수 자릿수 초가 잘립니다.  
  
 [b]의 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버 가정 크기 **TargetValuePtr* C 데이터 형식의 크기입니다.  
  
 [타임 스탬프 구조 c]에서 날짜 필드를 현재 날짜로 설정 됩니다 및 타임 스탬프 구조 소수 자릿수 초 필드가 0으로 설정 됩니다.  
  
 [d] C 데이터 형식에 해당 크기입니다.  
  
 결과 문자열은 시간 SQL 데이터 C 문자 데이터를 변환할 때에 "*hh*:*mm*:*ss*" 형식입니다. 이 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.
