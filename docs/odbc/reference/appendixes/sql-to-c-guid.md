---
description: 'SQL에서 C로: GUID'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a0285850372d78bbe0a24c8707e14e4f5672fb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456504"
---
# <a name="sql-to-c-guid"></a>SQL에서 C로: GUID
GUID ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_GUID  
  
 다음 표에서는 GUID SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 문자 바이트 길이입니다.|데이터|36|해당 없음|  
||*Bufferlength* < 37|Undefined|Undefined|22003|  
|SQL_C_WCHAR|*Bufferlength* > 문자 길이입니다.|데이터|36|해당 없음|  
||*Bufferlength* < 37|Undefined|Undefined|22003|  
|SQL_C_BINARY|데이터 \< =  *bufferlength* 의 바이트 길이|데이터|데이터의 길이 (바이트)|해당 없음|  
||*Bufferlength* > 데이터의 바이트 길이|Undefined|Undefined|22003|  
|SQL_C_GUID|없음 [a]|데이터|16 [b]|해당 없음|  
  
 [a]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.
