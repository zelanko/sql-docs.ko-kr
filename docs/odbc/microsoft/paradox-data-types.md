---
title: 역설 데이터 유형 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290933"
---
# <a name="paradox-data-types"></a>Paradox 데이터 형식
ODBC 역설 드라이버는 역설 데이터 형식을 ODBC SQL 데이터 형식에 매핑합니다. 다음 표에서는 모든 역설 데이터 형식을 나열하고 매핑된 ODBC SQL 데이터 형식을 보여 주며 이 형식이 표시됩니다.  
  
|역설 데이터 형식|ODBC 데이터 형식|  
|-----------------------|--------------------|  
|영숫자|SQL_VARCHAR|  
|자동 증가[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|바이트[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|이미지[2]|SQL_LONGVARBINARY|  
|논리적[1]|SQL_BIT|  
|롱[1]|SQL_INTEGER|  
|메모[2]|SQL_LONGVARCHAR|  
|돈[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|시간[1]|SQL_TIMESTAMP|  
|타임스탬프[1]|SQL_TIMESTAMP|  
  
 [1] 역설 버전 5에대해서만 유효합니다. *x*.  
  
 [2] 역설 버전 4에대해서만 유효합니다. *x* 및 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환합니다. *ODBC 프로그래머* 참조부록 D의 모든 변환은 이 항목의 앞에 나열된 ODBC SQL 데이터 형식에 대해 지원됩니다.  
  
 다음 표에서는 역설 데이터 형식에 대한 제한 사항이 보여 있습니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|영숫자|ALPHANUMERIC 열이 0또는 지정되지 않은 길이로 만들면 실제로 255바이트 열이 반환됩니다.|  
|BYTES|Paradox5 드라이버를 사용하여 이진 열에 NULL을 삽입하면 0으로 변경됩니다.|  
|LONG|역설 5의 Long 데이터 형식에 대해 역설 드라이버에서 지원하는 최대 음수 값입니다. *x는* ODBC 데이터 유형에 대한 긴 맵이 SQL_INTEGER 때문에 -2^31(-2147483648)이 아닙니다. Long에 대해 지원되는 최대 음수 값은 실제로 -2^31 + 1(-2147483647)입니다.|  
|timestamp|역설 드라이버에 의해 TIMESTAMP 열에 값을 삽입 한 다음 이후에 열에서 검색하면 검색 된 값은 반올림으로 인해 삽입 된 값과 최대 1 초까지 다를 수 있습니다.|  
  
 데이터 형식에 대한 더 많은 제한 사항은 [데이터 형식 제한에서](../../odbc/microsoft/data-type-limitations.md)찾을 수 있습니다.
