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
ms.openlocfilehash: 8d00a3c26d842b196e20861da6d8ae3e818d4cbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056899"
---
# <a name="sql-to-c-bit"></a>SQL에서 C로: 비트
Bit ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_BIT  
  
 다음 표에서는 bit SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*Bufferlength* > 1<br /><br /> *Bufferlength* <= 1|data<br /><br /> 정의되지 않음|1<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|없음 [a]|data|C 데이터 형식의 크기|해당 없음|  
|SQL_C_BIT|없음 [a]|data|1 [b]|해당 없음|  
|SQL_C_BINARY|*Bufferlength* >= 1<br /><br /> *Bufferlength* < 1|data<br /><br /> 정의되지 않음|1<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
  
 [a]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.  
  
 Bit SQL 데이터가 문자 C 데이터로 변환 되는 경우 가능한 값은 "0" 및 "1"입니다.
