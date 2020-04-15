---
title: 표준 준수 애플리케이션 및 드라이버 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4daf2e777b20b1b84c090757d0d84796a4cae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299720"
---
# <a name="standards-compliant-applications-and-drivers"></a>표준 준수 애플리케이션 및 드라이버
표준을 준수하는 응용 프로그램 또는 드라이버는 개방형 그룹 CAE 사양 "데이터 관리: SQL 통화 수준 인터페이스(CLI)"와 ISO/IEC 9075-3:1995(E) 통화 수준 인터페이스(SQL/CLI)를 준수하는 응용 프로그램 또는 드라이버입니다.  
  
 ODBC *3.x는* 다음과 같은 기능을 보장합니다.  
  
-   오픈 그룹 및 ISO CLI 사양에 기록된 응용 프로그램은 ODBC *3.x* 헤더 파일로 컴파일되고 ODBC *3.x* 라이브러리와 연결되고 ODBC 3.x 드라이버 관리자를 통해 드라이버에 액세스할 수 있는 경우 ODBC *3.x* 드라이버 또는 표준을 준수하는 드라이버와 함께 작동합니다. *3.x*  
  
-   오픈 그룹 및 ISO CLI 사양에 기록된 드라이버는 ODBC *3.x* 헤더 파일로 컴파일되고 ODBC *3.x* 라이브러리와 연결되고 응용 프로그램이 ODBC *3.x* 드라이버 관리자를 통해 드라이버에 액세스할 수 있는 경우 ODBC *3.x* 응용 프로그램 또는 표준을 준수하는 응용 프로그램과 함께 작동합니다.  
  
 표준을 준수하는 응용 프로그램과 드라이버는 ODBC_STD 컴파일 플래그로 컴파일됩니다.  
  
 표준을 준수하는 응용 프로그램은 다음과 같은 동작을 나타낸다.  
  
-   표준을 준수하는 응용 프로그램이 **SQLAllocEnv(SQLAllocEnv가** 오픈 그룹 및 ISO CLI에서 유효한 함수이기 때문에 발생할 수 있음)를 호출하는 경우 컴파일 시 **SQLAllocHandleStd에** 호출이 매핑됩니다. **SQLAllocEnv** 따라서 런타임에 응용 프로그램은 **SQLAllocHandleStd를**호출합니다. 이 호출을 처리하는 동안 드라이버 관리자는 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3 설정합니다. **SQLAllocHandleStd에** 대 한 호출은 *SQL_HANDLE_ENV 핸들 유형및* **SQLSetEnvAttr에** 대 한 호출을 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION 설정 하는 **SQLAllocHandle에** 대 한 호출에 해당 합니다.  
  
-   표준을 준수하는 응용 프로그램이 **SQLBindParam(SQLBindParam이** 오픈 그룹 및 ISO CLI에서 유효한 함수이기 때문에 발생할 수 있음)을 호출하는 경우 ODBC *3.x* 드라이버 관리자는 **SQLBindParameter**에서 해당 호출에 대한 호출을 매핑합니다. **SQLBindParam** (부록 G의 [SQLBindParam 매핑:](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) 이전 버전과의 호환성에 대한 드라이버 지침 참조)를 참조하십시오.  
  
-   ISO CLI에 맞추기 위해 ODBC *3.x* 헤더 파일에는 **SQLGetInfo**에 대한 호출에 사용되는 정보 유형에 대한 별칭이 포함되어 있습니다. 표준을 준수하는 응용 프로그램은 ODBC *3.x* 정보 유형 대신 이러한 별칭을 사용할 수 있습니다. 자세한 내용은 다음 항목인 [헤더 파일을](../../../odbc/reference/develop-app/header-files.md)참조하십시오.  
  
-   표준을 준수하는 응용 프로그램은 지원하는 모든 기능이 작동하는 드라이버에서 지원되는지 확인해야 합니다. SQL_ATTR_CURSOR_SCROLLABLE 문 특성을 SQL_SCROLLABLE 설정하고 SQL_ATTR_CURSOR_SENSITIVITY 명령문 특성을 SQL_INSENSITIVE 또는 SQL_SENSITIVE 설정하면 표준의 선택적 기능으로 사용할 수 있지만 ODBC *3.x* 코어 수준에 포함되지 않으므로 모든 ODBC *3.x* 드라이버에서 지원되지 않을 수 있습니다. 표준을 준수하는 응용 프로그램이 이러한 기능을 사용하는 경우 함께 작동할 드라이버가 해당 기능을 지원하는지 확인해야 합니다.
