---
title: 표준 호환 응용 프로그램 및 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1283cd0b41eff971a1014b213bda5e44f1912039
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792779"
---
# <a name="standards-compliant-applications-and-drivers"></a>표준 준수 애플리케이션 및 드라이버
표준 호환 응용 프로그램 또는 드라이버 하나인 Open 그룹 CAE 사양을 준수 하는 "데이터 관리: SQL 호출 수준 인터페이스 (CLI)"및 9075 ISO/IEC-3:1995 (E) 호출 수준 인터페이스 (SQL/CLI).  
  
 ODBC *3.x* 다음과 같은 기능을 보장 합니다.  
  
-   ODBC를 사용 하 여 Open Group 및 ISO CLI 사양에 작성 된 응용 프로그램 작동 *3.x* 드라이버나 ODBC를 사용 하 여 컴파일할 때 표준 규격 드라이버 *3.x* 헤더 파일 및 연결 ODBC *3.x* 라이브러리를 통해 ODBC 드라이버에 대 한 액세스를 얻을 때와 *3.x* 드라이버 관리자입니다.  
  
-   Open Group 및 ISO CLI 사양에 작성 된 드라이버는 ODBC를 사용 하 여 작동 *3.x* 응용 프로그램 또는 ODBC를 사용 하 여 컴파일할 때 표준 호환 응용 프로그램 *3.x* 헤더 파일 및 연결 ODBC를 사용 하 여 *3.x* 라이브러리 및 응용 프로그램에서 ODBC 통해 드라이버에 대 한 액세스를 향상 하는 경우 *3.x* 드라이버 관리자입니다.  
  
 표준 호환 응용 프로그램 및 드라이버 ODBC_STD 컴파일 플래그를 사용 하 여 컴파일됩니다.  
  
 표준 호환 응용 프로그램 동작은 다음과 같습니다.  
  
-   표준 호환 응용 프로그램을 호출 하는 경우 **SQLAllocEnv** (때문에 발생할 수 있는 **SQLAllocEnv** 는 Open Group 및 ISO CLI에서 올바른 함수), 호출에 매핑된  **SQLAllocHandleStd** 컴파일 타임에 있습니다. 결과적으로, 런타임 시 응용 프로그램 호출 **SQLAllocHandleStd**합니다. 이 호출을 처리 하는 동안 드라이버 관리자 SQL_OV_ODBC3를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다. 에 대 한 호출 **SQLAllocHandleStd** 를 호출 하는 것과 같습니다 **SQLAllocHandle** 사용 하 여는 *HandleType* SQL_HANDLE_ENV 및에 대 한 호출의 **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3으로 설정 합니다.  
  
-   표준 호환 응용 프로그램을 호출 하는 경우 **SQLBindParam** (때문에 발생할 수 있는 **SQLBindParam** 는 Open Group 및 ISO CLI에서 올바른 함수), ODBC *3.x* 드라이버 관리자에서 해당 호출에 대 한 호출을 매핑합니다 **SQLBindParameter**합니다. (참조 [SQLBindParam 매핑](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) 부록 g: 드라이버 지침 이전 버전과 호환성에 대 한 합니다.)  
  
-   ODBC ISO CLI를 사용 하 여 맞게 *3.x* 헤더 파일에 대 한 호출에 사용 되는 정보 유형에 대 한 별칭을 포함 **SQLGetInfo**합니다. 표준 호환 응용 프로그램을 ODBC 대신 이러한 별칭을 사용할 수 *3.x* 정보 유형입니다. 자세한 내용은 다음 항목을 참조 하세요 [헤더 파일](../../../odbc/reference/develop-app/header-files.md)합니다.  
  
-   표준 호환 응용 프로그램을 지 원하는 모든 기능 작동할지 드라이버에서 지원 되는지 확인 해야 합니다. SQL_SCROLLABLE 및 설정을 SQL_ATTR_CURSOR_SCROLLABLE 문 특성 설정을 SQL_INSENSITIVE 하거나 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY 문 특성은 표준에 대 한 선택적 기능으로 사용할 수 있는 기능 ODBC에 포함 되지 않지만 *3.x* Core 있어 수준이 지원 되지 않는 모든 ODBC에서 *3.x* 드라이버입니다. 이러한 기능을 사용 하는 표준 호환 응용 프로그램, 드라이버를 사용할 수 있는 고 지 확인 해야 합니다.
