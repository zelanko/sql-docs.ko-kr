---
description: 드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 형식 및 특성
title: 드라이버 특정 유형-데이터, 설명자, 정보, 진단 | Microsoft Docs
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
ms.openlocfilehash: 9a0ac3fd67e07f23f14420ee46ccda5cd409f87a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483006"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 형식 및 특성
드라이버는 다음에 대 한 드라이버 관련 값을 할당할 수 있습니다.  
  
-   **SQL 데이터 형식 표시기** 이는 **SQLBindParameter** 의 *ParameterType* 및 **SQLGetTypeInfo** 의 *DataType* 에서 사용 되며 **sqlcolattribute**, **Sqlcolumns**, **SQLDescribeCol**, **SQLGetTypeInfo**, **SQLDescribeParam**, **SQLProcedureColumns**및 **SQLSpecialColumns**에 의해 반환 됩니다.  
  
-   **설명자 필드** **Sqlcolattribute**, **SQLGetDescField**및 **SQLSetDescField**에서 *FieldIdentifier* 에 사용 됩니다.  
  
-   **진단 필드** **SQLGetDiagField** 및 **SQLGetDiagRec**의 *DiagIdentifier* 에 사용 됩니다.  
  
-   **정보 유형** 이러한 기능은 **SQLGetInfo**의 *InfoType* 에 사용 됩니다.  
  
-   **연결 및 문 특성** 이러한 속성은 **SQLGetConnectAttr**, **SQLGetStmtAttr**, **SQLSetConnectAttr**및 **SQLSetStmtAttr**의 *특성* 에 사용 됩니다.  
  
 이러한 각 항목에 대해 ODBC에서 사용 하도록 예약 된 값과 드라이버에서 사용 하도록 예약 된 값의 두 가지 값 집합이 있습니다. 드라이버 관련 값을 구현 하기 전에 드라이버 작성자는 Open Group에서 각 드라이버별 형식, 필드 또는 특성에 대 한 값을 요청 해야 합니다. 새 드라이버 개발의 경우 아래 표에 설명 된 범위를 사용 합니다. ODBC 3.8 드라이버 관리자는 알 수 없는 값을 사용 하는 경우 아래 설명 된 범위에 없는 경우 오류를 생성 하지 않습니다. 그러나 범위에 없는 알 수 없는 값이 수신 되 면 이후 버전의 드라이버 관리자에서 오류를 생성할 수 있습니다.  
  
 이러한 값이 ODBC 함수에 전달 되 면 드라이버는 값이 유효한 지 여부를 확인 해야 합니다. 드라이버는 다른 드라이버에 적용 되는 드라이버별 HYC00 (선택적 기능이 구현 되지 않음)를 반환 합니다.  
  
 ODBC 3.8부터 드라이버 작성자는 예약 된 범위 내에서 드라이버별 특성을 할당할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 3.8 드라이버 관리자는 이전 버전과의 호환성을 위해 이러한 범위의 유효성을 검사 하거나 적용 하지 않습니다. 그러나 이후 버전의 드라이버 관리자는 이러한 항목을 적용할 수 있습니다.  
  
|특성 유형|ODBC 데이터 형식|드라이버별 범위 기준|드라이버별 범위 제한|드라이버별 값 범위 기준에 대 한 ODBC 상수|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 데이터 형식 표시기|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|설명자 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|진단 필드|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|정보 유형|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|연결 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|문 특성|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  드라이버 관련 데이터 형식, 설명자 필드, 진단 필드, 정보 유형, 문 특성 및 연결 특성은 드라이버 설명서에 설명 되어 있어야 합니다. 이러한 값이 ODBC 함수에 전달 되 면 드라이버는 값이 유효한 지 여부를 확인 해야 합니다. 드라이버는 다른 드라이버에 적용 되는 드라이버별 HYC00 (선택적 기능이 구현 되지 않음)를 반환 합니다.  
  
 기준 값은 드라이버 개발을 용이 하 게 하기 위해 정의 됩니다. 예를 들어 드라이버별 진단 특성은 다음 형식으로 정의할 수 있습니다.  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
