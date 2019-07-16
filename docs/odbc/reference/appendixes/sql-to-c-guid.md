---
title: 'SQL에서 C로: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a2ed3cffcb196cb09841df3b54fbfab53e22477
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056868"
---
# <a name="sql-to-c-guid"></a>SQL에서 C로: GUID
GUID ODBC SQL 데이터 형식에 대 한 식별자가 있습니다.  
  
 SQL_GUID  
  
 다음 표에서 ODBC C 데이터 형식에는 GUID SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 문자 바이트 길이|data|36|n/a|  
||*BufferLength* < 37|Undefined|Undefined|22003|  
|SQL_C_WCHAR|*BufferLength* > 문자 길이|data|36|n/a|  
||*BufferLength* < 37|Undefined|Undefined|22003|  
|SQL_C_BINARY|데이터의 바이트 길이 \< =  *BufferLength*|data|데이터의 바이트 길이|n/a|  
||데이터의 바이트 길이 > *BufferLength*|Undefined|Undefined|22003|  
|SQL_C_GUID|[A] 없음|data|16[b]|n/a|  
  
 [a] 값 *BufferLength* 이 변환에 대해 무시 됩니다. 드라이버 가정 크기 **TargetValuePtr* C 데이터 형식의 크기입니다.  
  
 [b] C 데이터 형식에 해당 크기입니다.
