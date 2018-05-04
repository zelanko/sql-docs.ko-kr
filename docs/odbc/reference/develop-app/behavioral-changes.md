---
title: 변경 된 동작 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51737ccc21f8ee4d3d1943433f88393d4847ea8a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="behavioral-changes"></a>동작 변경 내용
동작 변경 내용이 있는 변경 내용이 반영은 *구문* 인터페이스의 똑같이 유지 하지만 *의미 체계* 변경 되었습니다. 이러한 변경 내용을 ODBC 2에서 사용 되는 기능입니다. *x* ODBC 3에 동일한 기능 다르게 동작 합니다. *x*합니다.  
  
 여부는 응용 프로그램에서 ODBC 2를 보여 줍니다. *x* 동작이 나 ODBC 3. *x* 동작은 SQL_ATTR_ODBC_VERSION 환경 특성에 의해 결정 됩니다. 이 32 비트 값을 ODBC 2 보이는 SQL_OV_ODBC2에 설정 됩니다. *x* 동작과 SQL_OV_ODBC3을 보이는 ODBC 3. *x* 동작 합니다.  
  
 호출 하 여 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되어 **SQLSetEnvAttr**합니다. 응용 프로그램이 호출 후 **SQLAllocHandle** 환경 핸들을 할당을 호출 해야**SQLSetEnvAttr** 것을 보여 동작을 설정 하는 즉시 합니다. (결과적으로 새 환경 상태는 할당 된에 있지만 versionless, 환경 핸들을 설명 하기 위해 상태입니다.) 자세한 내용은 참조 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 응용 프로그램 동작 SQL_ATTR_ODBC_VERSION 환경 특성 있지만 특성에서는 ODBC 2 응용 프로그램의 연결에 영향을 주지 상태입니다. *x* 또는 ODBC 3. *x* 드라이버입니다. ODBC 3입니다. *x* ODBC 2 응용 프로그램 하나에 연결할 수 있습니다. *x* 또는 3. *x* 환경 특성의 설정에 관계 없이 드라이버입니다.  
  
 ODBC 3입니다. *x* 응용 프로그램을 호출 하지 말아야 **SQLAllocEnv**합니다. 드라이버 관리자에 대 한 호출을 수신 하는 경우 결과적으로 **SQLAllocEnv**, 인식 응용 프로그램을 ODBC 2. *x* 응용 프로그램입니다.  
  
 SQL_ATTR_ODBC_VERSION 특성 ODBC 3의 세 가지 측면을 영향을 줍니다. *x* 드라이버의 동작:  
  
-   SQLSTATE  
  
-   날짜, 시간 및 타임 스탬프에 대 한 데이터 형식  
  
-   *CatalogName* 인수 **SQLTables** ODBC 3의 검색 패턴을 허용 합니다. *x*에 있지만 ODBC 2. *x*  
  
 SQL_ATTR_ODBC_VERSION 환경 특성의 설정에 영향을 주지 않는 **SQLSetParam** 또는 **SQLBindParam**합니다. **SQLColAttribute** 도 영향을 받지 않는이 비트입니다. 하지만 **SQLColAttribute** 영향 받는 특성을 반환 ODBC (date 형식, 전체 자릿수, 소수 자릿수 및 길이)의 버전, 의도 된 동작의 값에 의해 결정 되는 *FieldIdentifier*인수입니다. 때 *FieldIdentifier* SQL_DESC_TYPE, 같으면 **SQLColAttribute** ODBC 3을 반환 합니다. *x* date, time 및 timestamp;에 대 한 코드 때 *FieldIdentifier* SQL_COLUMN_TYPE, 같으면 **SQLColAttribute** ODBC 2를 반환 합니다. *x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSTATE 매핑](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
