---
title: 'SQL에서 C로: Bit | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7ff0bd2988460596623eb47ded276392dc3d443
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270976"
---
# <a name="sql-to-c-bit"></a>SQL에서 C로: 비트
ODBC SQL 데이터 형식은 비트 식별자:  
  
 SQL_BIT  
  
 다음 표에서 ODBC C 데이터 형식 bit SQL 데이터 변환 될 수 있습니다는 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* <= 1|data<br /><br /> 정의되지 않음|1<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|[A] 없음|data|C 데이터 형식의 크기|n/a|  
|SQL_C_BIT|[A] 없음|data|1[b]|n/a|  
|SQL_C_BINARY|*BufferLength* >= 1<br /><br /> *BufferLength* < 1|data<br /><br /> 정의되지 않음|1<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
  
 [a] 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버 가정 크기 **TargetValuePtr* C 데이터 형식의 크기입니다.  
  
 [b] C 데이터 형식에 해당 크기입니다.  
  
 SQL 데이터 비트 C 문자 데이터를 변환할 때 가능한 값은 "0" 및 "1".
