---
title: 드라이버 별 유형 - 데이터, 설명자, 정보, 진단 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19bb2dd113fbeae871892ea510713c638c886e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305771"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 형식 및 특성
드라이버는 다음에 대해 드라이버별 값을 할당할 수 있습니다.  
  
-   **SQL 데이터 유형 표시기** 이들은 **SQLBindParameter의** *매개 변수 유형및* **SQLGetTypeInfo의** *데이터 타이에서* 사용되며 **SQLColAttribute,** **SQLDescribeCol**, **SQLGetTypeInfo,** **SQLDescribeParaM , SQLDescribeParam**, **SQL프로시전열**및 **SQLDescribeCol** **SQLSpecialColumns에 의해 반환됩니다.**  
  
-   **설명자 필드** 이러한 필드는 **SQLColAttribute,** **SQLGetDescField**및 **SQLSetDescField에서** *필드 식별자에서* 사용됩니다.  
  
-   **진단 필드** SQLGetDiagField 및 **SQLGetDiagRec의** *DiagIdentifier에서* 사용됩니다. **SQLGetDiagField**  
  
-   **정보 유형** **SQLGetInfo의** *인포타입에* 사용됩니다.  
  
-   **연결 및 명령문 특성** 이러한 *특성에서* 사용 되는 **SQLGetConnectAttr,** **SQLGetStmtAttr,** **SQLSetConnectAttr**및 **SQLSetStmtAttr**.  
  
 이러한 각 항목에 대해 ODBC에서 사용하도록 예약된 값과 드라이버에서 사용하도록 예약된 값이라는 두 가지 값 집합이 있습니다. 드라이버 관련 값을 구현하기 전에 드라이버 작성자는 Open Group의 각 드라이버 별 유형, 필드 또는 특성에 대한 값을 요청해야 합니다. 새 드라이버 개발의 경우 아래 표에 설명된 범위를 사용합니다. ODBC 3.8 드라이버 관리자는 아래에 설명된 범위에 없는 알 수 없는 값을 사용 하는 경우 오류를 생성 하지 않습니다. 그러나 이후 버전의 드라이버 관리자는 범위에 없는 알 수 없는 값을 수신하는 경우 오류를 생성할 수 있습니다.  
  
 이러한 값이 ODBC 함수에 전달되면 드라이버는 값이 유효한지 확인해야 합니다. 드라이버는 다른 드라이버에 적용되는 드라이버 별 값에 대해 SQLSTATE HYC00(선택 기능이 구현되지 않음)을 반환합니다.  
  
 ODBC 3.8부터 드라이버 작성기는 예약된 범위 내에서 드라이버 별 특성을 할당할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 3.8 드라이버 관리자는 이전 버전과의 호환성을 위해 이러한 범위를 확인하거나 적용하지 않습니다. 그러나 드라이버 관리자의 이후 버전이 이를 적용할 수 있습니다.  
  
|특성 유형|ODBC 데이터 형식|드라이버별 범위 베이스|드라이버별 범위 제한|드라이버별 값 범위 베이스에 대한 ODBC 상수|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 데이터 유형 표시기|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|설명자 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|진단 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|정보 유형|SQLUSmallINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|연결 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|문 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  드라이버 관련 데이터 형식, 설명자 필드, 진단 필드, 정보 유형, 문 특성 및 연결 특성은 드라이버 설명서에 설명해야 합니다. 이러한 값이 ODBC 함수에 전달되면 드라이버는 값이 유효한지 확인해야 합니다. 드라이버는 다른 드라이버에 적용되는 드라이버 별 값에 대해 SQLSTATE HYC00(선택 기능이 구현되지 않음)을 반환합니다.  
  
 기본 값은 드라이버 개발을 용이하게 하기 위해 정의됩니다. 예를 들어 드라이버 별 진단 특성을 다음 형식으로 정의할 수 있습니다.  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
