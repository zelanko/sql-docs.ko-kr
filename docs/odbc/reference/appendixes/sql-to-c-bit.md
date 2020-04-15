---
title: 'SQL에서 C까지: 비트 | 마이크로 소프트 문서'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57688f34c504b221f77c1b66792bf9ee9398df27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296753"
---
# <a name="sql-to-c-bit"></a>SQL에서 C로: 비트
비트 ODBC SQL 데이터 형식의 식별자는 다음과 같은 것입니다.  
  
 SQL_BIT  
  
 다음 표에서는 비트 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주실 수 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  
  
|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*버퍼길이* > 1<br /><br /> *버퍼길이* <= 1|데이터<br /><br /> 정의되지 않음|1<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|없음[a]|데이터|C 데이터 형식의 크기|해당 없음|  
|SQL_C_BIT|없음[a]|데이터|1[b]|해당 없음|  
|SQL_C_BINARY|*버퍼길이* >= 1<br /><br /> *버퍼길이* < 1|데이터<br /><br /> 정의되지 않음|1<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
  
 [a] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.  
  
 비트 SQL 데이터가 문자 C 데이터로 변환되면 가능한 값은 "0" 및 "1"입니다.
