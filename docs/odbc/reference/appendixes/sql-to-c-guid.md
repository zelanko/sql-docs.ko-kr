---
title: 'SQL에서 C까지: GUID | 마이크로 소프트 문서'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0f247bc4cb411d535050d7c78e0ea42cc144b0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296463"
---
# <a name="sql-to-c-guid"></a>SQL에서 C로: GUID
GUID ODBC SQL 데이터 형식의 식별자는 다음과 입니다.  
  
 SQL_GUID  
  
 다음 표에서는 GUID SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주실 수 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  
  
|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*버퍼길이* > 문자 바이트 길이|데이터|36|해당 없음|  
||*버퍼길이* < 37|정의되지 않음|정의되지 않음|22003|  
|SQL_C_WCHAR|*버퍼길이* > 문자 길이|데이터|36|해당 없음|  
||*버퍼길이* < 37|정의되지 않음|정의되지 않음|22003|  
|SQL_C_BINARY|데이터 \< =  *버퍼길이의* 바이트 길이|데이터|바이트 내 데이터 길이|해당 없음|  
||*버퍼길이>* 데이터의 바이트 길이|정의되지 않음|정의되지 않음|22003|  
|SQL_C_GUID|없음[a]|데이터|16[b]|해당 없음|  
  
 [a] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.
