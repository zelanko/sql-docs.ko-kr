---
title: "데이터 형식 paradox | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9099d9a84fb79132249c74d1d24cc240bcf8aae0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="paradox-data-types"></a>Paradox 데이터 형식
ODBC Paradox 드라이버 Paradox 데이터 형식을 ODBC SQL 데이터 형식을 매핑합니다. 다음 표에서 모든 Paradox 데이터 형식을 나열 하 고 ODBC SQL 데이터 형식에 매핑되는지를 보여 줍니다.  
  
|Paradox 데이터 형식|ODBC 데이터 형식|  
|-----------------------|--------------------|  
|영숫자|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|바이트 [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|이미지 [2]|SQL_LONGVARBINARY|  
|논리 [1]|SQL_BIT|  
|장기 [1]|SQL_INTEGER|  
|메모-[2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|짧은|SQL_SMALLINT|  
|시간 [1]|SQL_TIMESTAMP|  
|타임 스탬프 [1]|SQL_TIMESTAMP|  
  
 Paradox 버전 5에 대 한 유효 기간 [1]입니다. *x*합니다.  
  
 Paradox 버전 4에 대 한 올바른 ' [2]. *x* 5. *x*합니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환 합니다. 부록 d의 모든 변환이 *ODBC Programmer's Reference* 이 항목의 앞부분에 나열 된 ODBC SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 Paradox 데이터 형식에 대해 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|영숫자|0의 영숫자 열 만들기 또는 실제로 지정 되지 않은 길이 255 바이트 열을 반환 합니다.|  
|BYTES|Paradox5 드라이버 이진 열에 NULL을 삽입 하면 0으로 변경 됩니다.|  
|LONG|Paradox 5에 대 한 Long 데이터 형식에 대 한 Paradox 드라이버에서 지 원하는 최대 음수 값입니다. *x* 가-2 ^31 (-2147483648), ODBC 데이터에 긴 지도 이후 것 처럼 입력 SQL_INTEGER 합니다. 장기에 대 한 지원 되는 최대 음수 값은 실제로-2 ^31 + 1 (-2147483647).|  
|timestamp|값은 Paradox 드라이버에 의해 타임 스탬프 열에 삽입 한 다음 이후에 열에서 검색 하는 경우 검색 된 값 따라 다를 수는 삽입 된 값에서 1 초를 반올림으로 인해 합니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 확인할 수 있습니다 [데이터 형식 제한](../../odbc/microsoft/data-type-limitations.md)합니다.

