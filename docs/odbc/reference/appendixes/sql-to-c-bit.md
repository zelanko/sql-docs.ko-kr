---
title: 'SQL에서 c: 비트로 | Microsoft Docs'
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
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6862a94cc31bcbee1b931b18c775f03a9e1e58ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-bit"></a>SQL에서 c: 비트로
다음은 비트 ODBC SQL 데이터 형식에 대 한 식별자가입니다.  
  
 SQL_BIT  
  
 다음 표에서 ODBC C 데이터 형식 bit SQL 데이터 변환 될 수 있습니다는 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* < = 1|Data<br /><br /> 정의되지 않음|1.<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|[A] 없음|Data|C 데이터 형식의 크기|n/a|  
|SQL_C_BIT|[A] 없음|Data|1 [b]|n/a|  
|SQL_C_BINARY|*BufferLength* > = 1<br /><br /> *BufferLength* < 1|Data<br /><br /> 정의되지 않음|1.<br /><br /> 정의되지 않음|n/a<br /><br /> 22003|  
  
 [a]의 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버를 가정 하는 크기 **TargetValuePtr* C 데이터 형식 크기입니다.  
  
 [b] C 데이터 형식에 해당 크기입니다.  
  
 SQL 데이터 비트 C 문자 데이터로 변환 되 면 가능한 값은 "0", "1".
