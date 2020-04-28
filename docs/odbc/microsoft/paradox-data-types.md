---
title: Paradox 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290933"
---
# <a name="paradox-data-types"></a>Paradox 데이터 형식
ODBC Paradox 드라이버는 Paradox 데이터 형식을 ODBC SQL 데이터 형식에 매핑합니다. 다음 표에서는 모든 Paradox 데이터 형식을 나열 하 고 매핑되는 ODBC SQL 데이터 형식을 보여 줍니다.  
  
|Paradox 데이터 형식|ODBC 데이터 형식|  
|-----------------------|--------------------|  
|영숫자만|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|바이트 [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|이미지 [2]|SQL_LONGVARBINARY|  
|논리적 [1]|SQL_BIT|  
|LONG [1]|SQL_INTEGER|  
|메모 [2]|SQL_LONGVARCHAR|  
|비용 [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|시간 [1]|SQL_TIMESTAMP|  
|타임 스탬프 [1]|SQL_TIMESTAMP|  
  
 [1] Paradox 버전 5에만 유효 합니다. *x*.  
  
 [2] Paradox 버전 4에 대해서만 유효 합니다. *x* 및 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC SQL 데이터 형식을 반환 합니다. *Odbc 프로그래머 참조* 의 부록 D에 있는 모든 변환은이 항목의 앞부분에 나열 된 odbc SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서는 Paradox 데이터 형식에 대 한 제한 사항을 보여 줍니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|영숫자만|0 또는 지정 되지 않은 길이의 영숫자 열을 만들면 실제로 255 바이트 열이 반환 됩니다.|  
|BYTES|Paradox5 드라이버를 사용 하 여 이진 열에 NULL을 삽입 하는 경우 0으로 변경 됩니다.|  
|LONG|Paradox가 5 인 Long 데이터 형식에 대해 Paradox 드라이버에서 지 원하는 최대 음수 값입니다. *x* 는 LONG 맵이 ODBC 데이터 형식에 SQL_INTEGER 때문에-2 ^ 31 (-2147483648)이 아닙니다. Long에 대해 지원 되는 최대 음수 값은 실제로-2 ^ 31 + 1 (-2147483647)입니다.|  
|timestamp|Paradox 드라이버에서 값을 타임 스탬프 열에 삽입 한 다음 열에서 검색 된 값은 반올림으로 인해 1 초까지 삽입 된 값과 다를 수 있습니다.|  
  
 데이터 형식에 대 한 더 많은 제한은 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)에서 찾을 수 있습니다.
