---
title: "표준 호환 응용 프로그램 및 드라이버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1aba299d163aaf9ec14d86740e5d8aa91ddb7b3b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="standards-compliant-applications-and-drivers"></a>표준 호환 응용 프로그램 및 드라이버
표준 호환 응용 프로그램 또는 드라이버는 준수 하는 Open 그룹 CAE 사양 "데이터 관리:: SQL 호출 수준 인터페이스 (CLI)," 및 ISO/IEC 9075 하나-3:1995 (E) 호출 수준 인터페이스 (SQL/CLI).  
  
 ODBC 3*.x* 다음과 같은 기능을 보장 합니다.  
  
-   ODBC 3 Open Group 및 ISO CLI 사양을 작성 된 응용 프로그램 작동할지*.x* 드라이버 또는 ODBC 3로 컴파일할 때 표준 규격 드라이버*.x* 헤더 파일 및 연결 된 ODBC 3*.x* 라이브러리가 ODBC 3를 통해 드라이버에 액세스할 때 및*.x* 드라이버 관리자입니다.  
  
-   Open Group 및 ISO CLI 사양을 작성 된 드라이버는 ODBC 3 작동할지*.x* 응용 프로그램 또는 ODBC 3로 컴파일할 때 표준 호환 응용 프로그램*.x* 헤더 파일 및 연결 ODBC 3*.x* 라이브러리, 응용 프로그램에서 ODBC 3를 통해 드라이버에 대 한 액세스를 획득 하는 경우 및*.x* 드라이버 관리자입니다.  
  
 표준 호환 응용 프로그램 및 드라이버 ODBC_STD 컴파일 플래그를 사용 하 여 컴파일됩니다.  
  
 표준 호환 응용 프로그램 동작은 다음과 같습니다.  
  
-   표준 호환 응용 프로그램을 호출 하는 경우 **SQLAllocEnv** (때문에 발생할 수 있는 **SQLAllocEnv** 는 Open Group 및 ISO CLI에는 유효한 함수), 호출에 매핑된  **SQLAllocHandleStd** 컴파일 타임에 있습니다. 결과적으로, 실행 시 응용 프로그램 호출 **SQLAllocHandleStd**합니다. 이 호출을 처리 하는 동안 드라이버 관리자 SQL_OV_ODBC3를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다. 에 대 한 호출 **SQLAllocHandleStd** 에 대 한 호출에 해당 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV 및에 대 한 호출의 **SQLSetEnvAttr** SQL_OV_ODBC3를 sql_attr_odbc_version으로 설정 합니다.  
  
-   표준 호환 응용 프로그램을 호출 하는 경우 **SQLBindParam** (때문에 발생할 수 있는 **SQLBindParam** 는 Open Group 및 ISO CLI에는 유효한 함수), ODBC 3*.x* 드라이버 관리자에서 해당 호출에 대 한 호출을 매핑합니다 **SQLBindParameter**합니다. (참조 [SQLBindParam 매핑](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에서.)  
  
-   ODBC 3 ISO CLI에 맞춰*.x* 헤더 파일에 대 한 호출에서 사용 되는 정보 종류에 대 한 별칭을 포함 **SQLGetInfo**합니다. 표준 호환 응용 프로그램을 ODBC 3 대신 이러한 별칭을 사용할 수*.x* 정보 유형입니다. 자세한 내용은 다음 항목을 참조 하십시오. [헤더 파일](../../../odbc/reference/develop-app/header-files.md)합니다.  
  
-   표준 호환 응용 프로그램 작동할지 드라이버에서 지 원하는 지 원하는 모든 기능을 확인 해야 합니다. SQL_ATTR_CURSOR_SCROLLABLE 문 특성을 SQL_SCROLLABLE 설정 설정 SQL_INSENSITIVE 또는 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY 문 특성은 표준에 선택적 기능으로 사용할 수 있는 기능 ODBC 3에 포함 되지 않은*.x* 코어 스레드와 수준이 지원 되지 않는 모든 ODBC 3으로*.x* 드라이버입니다. 이러한 기능을 사용 하는 표준 호환 응용 프로그램에서는 작동 하는 드라이버 지원에 확인 해야 것입니다.

