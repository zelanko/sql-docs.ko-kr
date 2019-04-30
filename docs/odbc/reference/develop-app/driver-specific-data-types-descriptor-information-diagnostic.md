---
title: 데이터, 드라이버 관련 형식 설명자, 정보, 진단 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c310e6c6b2833da6e1d9167faee2e979bb4616
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238814"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 형식 및 특성
드라이버 다음에 대 한 드라이버 관련 값을 할당할 수 있습니다.  
  
-   **SQL 데이터 형식 표시기** 이러한, *ParameterType* 에 **SQLBindParameter** 및 *DataType* 에 **SQLGetTypeInfo** 반환한 **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**,  **SQLDescribeParam**, **SQLProcedureColumns**, 및 **SQLSpecialColumns**합니다.  
  
-   **설명자 필드** 이들은 **SQLColAttribute**, **SQLGetDescField** 및 **SQLSetDescField** 에서 *FieldIdentifier* 에서 사용됩니다.  
  
-   **진단 필드** **SQLGetDiagField** 및 **SQLGetDiagRec** 에서 *DiagIdentifier* 에 사용됩니다.  
  
-   **정보 유형** 이것은 **InfoGateInfo** 의 *InfoType* 에서 사용됩니다.  
  
-   **연결 및 명령문 속성** **SQLGetConnectAttr**, **SQLGetStatusAttr**, **SQLSetConnectAttr** 및 **SQLSetStmtAttr** 의 *속성* 에 사용됩니다.  
  
 각이 항목에 대 한 가지 값의 두 집합: ODBC에서 사용 하도록 예약 하는 값 및 드라이버에서 사용 하도록 예약 하는 값입니다. 드라이버 관련 값을 구현 하기 전에 드라이버 작성자는 Open Group에서 각 드라이버 관련 형식, 필드 또는 특성에 대 한 값을 요청 해야 합니다. 새 드라이버 개발을 위해 아래 표에 설명 된 범위를 사용 합니다. ODBC 3.8 드라이버 관리자는 알 수 없는 값을 아래에 설명 된 범위에 있지 않은 경우 오류를 생성 하지 않습니다. 그러나 이후 버전의 드라이버 관리자에 알 수 없는 값은 수신 된 범위에 있지 않은 경우 오류를 생성할 수 있습니다.  
  
 이러한 값은 ODBC 함수에 전달 되 면 드라이버는 값이 유효한 지 확인 해야 합니다. 드라이버는 SQLSTATE HYC00 반환 (선택적 기능이 구현 되지 않았습니다) 다른 드라이버에 적용 되는 드라이버 관련 값에 대 한 합니다.  
  
 ODBC 3.8 이상에서는 드라이버 작성자 예약된 된 범위 내에서 드라이버별 특성을 할당할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 3.8 드라이버 관리자의 유효성을 검사 아니고 이전 버전과 호환성에 대 한 이러한 범위를 적용 합니다. 그러나 이후 버전의 드라이버 관리자, 적용할 수 있습니다.  
  
|특성 유형|ODBC 데이터 형식|기본 드라이버 관련 범위|드라이버 관련 범위 제한|기본 드라이버 관련 값 범위에 대 한 ODBC 상수|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 데이터 형식 표시기|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|설명자 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|진단 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|정보 유형|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|연결 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|문 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  드라이버 설명서의 드라이버별 데이터 형식, 설명자 필드, 진단 필드, 정보 유형, 문 특성 및 연결 특성을 설명 해야 합니다. 이러한 값은 ODBC 함수에 전달 되 면 드라이버는 값이 유효한 지 확인 해야 합니다. 드라이버는 SQLSTATE HYC00 반환 (선택적 기능이 구현 되지 않았습니다) 다른 드라이버에 적용 되는 드라이버 관련 값에 대 한 합니다.  
  
 기본 값은 드라이버 개발을 용이 하 게 정의 됩니다. 예를 들어, 다음 형식으로 드라이버 관련 진단 특성을 정의할 수 있습니다.  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
