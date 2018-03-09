---
title: "C: 누계 SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87a62501d4d03073d8c43b2f791ceffeec9b0b30
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-date"></a>SQL에서 c: 날짜
ODBC SQL 데이터 형식이 날짜에 대 한 식별자:  
  
 SQL_TYPE_DATE  
  
 다음 표에서 ODBC C 데이터 형식에 날짜 SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 문자 바이트 길이<br /><br /> 11 < = *BufferLength* < = 문자 바이트 길이<br /><br /> *BufferLength* < 11|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|10<br /><br /> 데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 문자 길이<br /><br /> 11 < = *BufferLength* < = 문자 길이<br /><br /> *BufferLength* < 11|data<br /><br /> 잘린된 데이터<br /><br /> 정의되지 않음|10<br /><br /> 문자에서 데이터의 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> 정의되지 않음|데이터의 바이트 길이<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|[A] 없음|data|6 [c + +]|n/a|  
|SQL_C_TYPE_TIMESTAMP|[A] 없음|데이터 [b]|16 [c + +]|n/a|  
  
 [a]의 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버를 가정 하는 크기 **TargetValuePtr* C 데이터 형식 크기입니다.  
  
 [b] 타임 스탬프 구조의 시간 필드를 0으로 설정 됩니다.  
  
 [c] C 데이터 형식에 해당 크기입니다.  
  
 에 결과 문자열은 날짜 SQL 데이터를 C 문자 데이터로 변환 되 면는 "*yyyy*-*mm*-*dd*" 형식입니다. 이 형식은 Windows® 국가 설정에 의해 영향을 받지 않습니다.
