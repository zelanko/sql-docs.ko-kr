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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296383"
---
# <a name="sql-to-c-time"></a>SQL에서 C로: 시간
Time ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_TYPE_TIME  
  
 다음 표에서는 SQL 데이터를 변환 하는 데 사용할 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 문자 바이트 길이입니다.<br /><br /> *9* <= *bufferlength* <= 문자 바이트 길이<br /><br /> *Bufferlength* < 9|데이터<br /><br /> 잘린 데이터 [a]<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Bufferlength* > 문자 길이입니다.<br /><br /> *9* <= *bufferlength* <= 문자 길이<br /><br /> *Bufferlength* < 9|데이터<br /><br /> 잘린 데이터 [a]<br /><br /> 정의되지 않음|데이터의 길이 (문자)<br /><br /> 데이터의 길이 (문자)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_TYPE_TIME|없음 [b]|데이터|6 [d]|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|없음 [b]|데이터 [c]|16 [d]|해당 없음|  
  
 [a] 시간의 소수 자릿수 초는 잘립니다.  
  
 [b]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [c] 타임 스탬프 구조의 날짜 필드가 현재 날짜로 설정 되 고 타임 스탬프 구조의 초 소수 필드가 0으로 설정 됩니다.  
  
 [d] 해당 C 데이터 형식의 크기입니다.  
  
 SQL 데이터가 문자 C 데이터로 변환 되는 경우 결과 문자열은 "*hh*:*mm*:*ss*" 형식입니다. 이 형식은 Windows® country 설정의 영향을 받지 않습니다.
