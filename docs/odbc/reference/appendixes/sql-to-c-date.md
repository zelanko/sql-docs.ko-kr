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
ms.openlocfilehash: d282798a31ac9059ed3c1901ea01f1f3104f09c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056886"
---
# <a name="sql-to-c-date"></a>SQL에서 C로: 날짜
ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_TYPE_DATE  
  
 다음 표에서는 날짜 SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 문자 바이트 길이입니다.<br /><br /> 11 <= *bufferlength* <= 문자 바이트 길이<br /><br /> *Bufferlength* < 11|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|10<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Bufferlength* > 문자 길이입니다.<br /><br /> 11 <= *bufferlength* <= 문자 길이<br /><br /> *Bufferlength* < 11|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|10<br /><br /> 데이터의 길이 (문자)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|data<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_TYPE_DATE|없음 [a]|data|6 [c]|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|없음 [a]|데이터 [b]|16 [c]|해당 없음|  
  
 [a]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [b] 타임 스탬프 구조의 시간 필드는 0으로 설정 됩니다.  
  
 [c] 해당 C 데이터 형식의 크기입니다.  
  
 날짜 SQL 데이터가 문자 C 데이터로 변환 되는 경우 결과 문자열은 "*yyyy*-*mm*-*dd*" 형식입니다. 이 형식은 Windows® country 설정의 영향을 받지 않습니다.
