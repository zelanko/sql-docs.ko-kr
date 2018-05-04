---
title: 'SQL에서 c: 시간 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 079722668c6bce9a7d5ca2012aa947d6a87951d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-time"></a>SQL에서 c: 시간
ODBC SQL 데이터 형식은 시간에 대 한 식별자:  
  
 SQL_TYPE_TIME  
  
 다음 표에서 ODBC C 데이터 형식 시간 SQL 데이터 변환할 수를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 문자 바이트 길이<br /><br /> *9* <= *BufferLength* < = 문자 바이트 길이<br /><br /> *BufferLength* < 9|Data<br /><br /> [A] 잘린된 데이터<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 문자 길이<br /><br /> *9* <= *BufferLength* < = 문자 길이<br /><br /> *BufferLength* < 9|Data<br /><br /> [A] 잘린된 데이터<br /><br /> 정의되지 않음|문자에서 데이터의 길이<br /><br /> 문자에서 데이터의 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|Data<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_TYPE_TIME|없음 [b]|Data|6 [d]|n/a|  
|SQL_C_TYPE_TIMESTAMP|없음 [b]|데이터 [c + +]|16 [d]|n/a|  
  
 [a] 시간의 소수 자릿수 초가 잘립니다.  
  
 [b]의 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버를 가정 하는 크기 **TargetValuePtr* C 데이터 형식 크기입니다.  
  
 [c] 타임 스탬프 구조의 날짜 필드를 현재 날짜로 설정 됩니다 및 타임 스탬프 구조의 소수 자릿수 초 필드를 0으로 설정 되어 있습니다.  
  
 [d] C 데이터 형식에 해당 크기입니다.  
  
 결과 문자열의 형식이 시간 SQL 데이터를 C 문자 데이터로 변환 되 면는 "*hh*:*mm*:*ss*" 형식입니다. 이 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.
