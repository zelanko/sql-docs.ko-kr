---
title: 드라이버 관련 형식-데이터를 정보, 설명자 진단 | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 025ba90e13555eeac1db0d598cb1bf98b40c539d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버 관련 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성
드라이버는 다음에 대 한 드라이버 관련 값을 할당할 수 있습니다.  
  
-   **SQL 데이터 형식 표시기** 이러한ְ *ParameterType* 에 **SQLBindParameter** 및 *DataType* 에 **SQLGetTypeInfo** 반환한 **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**,  **SQLDescribeParam**, **SQLProcedureColumns**, 및 **SQLSpecialColumns**합니다.  
  
-   **설명자 필드** 이러한 *FieldIdentifier* 에 **SQLColAttribute**, **SQLGetDescField**, 및 **SQLSetDescField**.  
  
-   **진단 필드** 이러한ְ *DiagIdentifier* 에 **SQLGetDiagField** 및 **SQLGetDiagRec**합니다.  
  
-   **정보 유형이** 이러한ְ *정보 항목* 에 **SQLGetInfo**합니다.  
  
-   **연결 및 문 특성** 이러한ְ *특성* 에 **SQLGetConnectAttr**, **SQLGetStmtAttr**,  **SQLSetConnectAttr**, 및 **SQLSetStmtAttr**합니다.  
  
 각이 항목에는 두 값 집합이: ODBC를 사용 하도록 예약 되어 값과 드라이버에서 사용 하도록 예약 하는 값입니다. 드라이버 관련 값을 구현 하기 전에 드라이버 작성자 Open 그룹에서 각 드라이버 관련 형식, 필드 또는 특성에 대 한 값을 요청 해야 합니다. 새 드라이버 개발을 위해 아래 표에 설명 된 범위를 사용 합니다. ODBC 3.8 드라이버 관리자 알 수 없는 값 아래에 설명 된 범위에 있지 않은 사용 하는 경우 오류가 발생 하지 않습니다. 그러나 이후 버전의 드라이버 관리자에 알 수 없는 값 수신 범위에 있지 않은 경우 오류가 발생할 수 있습니다.  
  
 이러한 값은 ODBC 함수에 전달 되 면 드라이버는 값이 유효한 지 확인 해야 합니다. 드라이버는 SQLSTATE HYC00 반환 (선택적 기능이 구현 되지 않았습니다) 다른 드라이버에 적용 되는 드라이버 관련 값에 대 한 합니다.  
  
 ODBC 3.8 부터는 드라이버 작성자 예약된 된 범위 내에 드라이버별 특성을 할당할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 3.8 드라이버 관리자의 유효성을 검사 아니고 이전 버전과 호환성을 위해 이러한 범위를 적용 합니다. 그러나 이후 버전의 드라이버 관리자, 적용할 수 있습니다.  
  
|특성 유형|ODBC 데이터 형식|기본 드라이버 관련 범위|드라이버 관련 범위 제한|기본 드라이버의 특정 값 범위에 대 한 ODBC 상수|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 데이터 형식 표시기|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|설명자 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|진단 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|정보 유형|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|연결 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|문 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  드라이버 관련 데이터 형식, 설명자 필드, 진단 필드, 정보 유형, 문 특성 및 연결 특성 드라이버 설명서에서 설명 되어야 합니다. 이러한 값은 ODBC 함수에 전달 되 면 드라이버는 값이 유효한 지 확인 해야 합니다. 드라이버는 SQLSTATE HYC00 반환 (선택적 기능이 구현 되지 않았습니다) 다른 드라이버에 적용 되는 드라이버 관련 값에 대 한 합니다.  
  
 기본 값은 드라이버 개발을 용이 하 게 정의 됩니다. 예를 들어 다음과 같은 형식의 드라이버 특정 진단 특성을 정의할 수 있습니다.  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
