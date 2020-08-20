---
description: 동작 변경
title: 동작 변경 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fb5501d362cb46f3616e58c5a4994bab86e00ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461625"
---
# <a name="behavioral-changes"></a>동작 변경
동작 변경은 인터페이스의 *구문이* 동일 하 게 유지 되지만 *의미 체계가* 변경 된 변경 내용입니다. 이러한 변경의 경우 ODBC 2에서 사용 되는 기능입니다. *x* 는 ODBC 3의 동일한 기능과 다르게 동작 합니다. *x*.  
  
 응용 프로그램에서 ODBC 2를 표시할지 여부입니다. *x* 동작 또는 ODBC 3. *x* 동작은 SQL_ATTR_ODBC_VERSION 환경 특성에 의해 결정 됩니다. 이 32 비트 값은 ODBC 2를 나타내는 SQL_OV_ODBC2로 설정 됩니다. *x* 동작 및 ODBC 3에 SQL_OV_ODBC3 합니다. *x* 동작입니다.  
  
 SQL_ATTR_ODBC_VERSION 환경 특성은 **SQLSetEnvAttr**에 대 한 호출로 설정 됩니다. 응용 프로그램에서 **SQLAllocHandle** 를 호출 하 여 환경 핸들을 할당 한 후에는**SQLSetEnvAttr** 를 즉시 호출 하 여 발생 하는 동작을 설정 해야 합니다. 결과적으로, 할당 되었지만 versionless 상태에서 환경 핸들을 설명 하는 새 환경 상태가 있습니다. 자세한 내용은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.  
  
 응용 프로그램은 SQL_ATTR_ODBC_VERSION 환경 특성을 사용 하 여 어떤 동작을 수행 하지만, 특성은 ODBC 2를 사용 하는 응용 프로그램의 연결에는 영향을 주지 않습니다. *x* 또는 ODBC 3. *x* 드라이버. ODBC 3. *x* 응용 프로그램은 ODBC 2에 연결할 수 있습니다. *x* 또는 3. *x* 드라이버, 환경 특성의 설정에 관계 없이  
  
 ODBC 3. *x* 응용 프로그램은 **sqlallocenv**를 호출 하면 안 됩니다. 따라서 드라이버 관리자는 **Sqlallocenv**호출을 받으면 응용 프로그램을 ODBC 2로 인식 합니다. *x* 응용 프로그램.  
  
 SQL_ATTR_ODBC_VERSION 특성은 ODBC 3의 세 가지 측면에 영향을 줍니다. *x* 드라이버의 동작:  
  
-   SQLSTATE  
  
-   날짜, 시간 및 타임 스탬프에 대 한 데이터 형식  
  
-   **Sqltables** 의 *CATALOGNAME* 인수는 ODBC 3의 검색 패턴을 허용 합니다. *x*이지만 ODBC 2에서는 그렇지 않습니다. *x*  
  
 SQL_ATTR_ODBC_VERSION 환경 특성의 설정은 **SQLSetParam** 또는 **sqlbindparam 함수와**에 영향을 주지 않습니다. **Sqlcolattribute** 도이 비트의 영향을 받지 않습니다. **Sqlcolattribute** 는 ODBC 버전 (날짜 유형, 전체 자릿수, 소수 자릿수 및 길이)의 영향을 받는 특성을 반환 하지만, 의도 된 동작은 *FieldIdentifier* 인수의 값에 따라 결정 됩니다. *FieldIdentifier* 가 SQL_DESC_TYPE와 같으면 **SQLCOLATTRIBUTE** 는 ODBC 3을 반환 합니다. 날짜, 시간 및 타임 스탬프에 대 한 *x* 코드 *FieldIdentifier* 가 SQL_COLUMN_TYPE와 같으면 **SQLCOLATTRIBUTE** 는 ODBC 2를 반환 합니다. 날짜, 시간 및 타임 스탬프에 대 한 *x* 코드  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSTATE 매핑(SQLSTATE Mappings)](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [날짜/시간 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
