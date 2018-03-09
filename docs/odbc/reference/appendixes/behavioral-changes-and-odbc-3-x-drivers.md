---
title: "변경 된 동작 및 ODBC 3.x 드라이버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc06520b8dcf2fe5686d041e1c48e50cf5555b79
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>변경 된 동작 및 ODBC 3.x 드라이버
환경 특성 SQL_ATTR_ODBC_VERSION 나타냅니다 드라이버에 ODBC 2를 따르기만 하는 데 필요한 여부. *x* 동작이 나 ODBC 3*.x* 동작 합니다. SQL_ATTR_ODBC_VERSION 환경 특성은 설정 하는 방법을 응용 프로그램에 따라 달라 집니다. ODBC 3*.x* 응용 프로그램 호출 해야 **SQLSetEnvAttr** 호출 후이 특성을 설정 하려면 **SQLAllocHandle** 환경 핸들을 할당 를호출하기전에 **SQLAllocHandle** 연결 핸들을 할당 합니다. 드라이버 관리자 SQLSTATE HY010 반환이 작업을 수행 하지 않은 경우 (함수 시퀀스 오류입니다.)의 두 번째 호출 **SQLAllocHandle**합니다.  
  
> [!NOTE]  
>  변경 된 동작 및 응용 프로그램의 작업 방식에 대 한 자세한 내용은 참조 하십시오. [변경 된 동작](../../../odbc/reference/develop-app/behavioral-changes.md)합니다.  
  
 ODBC 2입니다. *x* 응용 프로그램 및 ODBC 2. *x* ODBC 3과 함께 다시 컴파일된 응용 프로그램*.x* 헤더 파일을 호출 하지 않으면 **SQLSetEnvAttr**합니다. 하지만 호출 **SQLAllocEnv** 대신 **SQLAllocHandle** 환경 핸들을 할당 합니다. 따라서 응용 프로그램 호출 하는 경우 **SQLAllocEnv** 드라이버 관리자를 드라이버 관리자를 호출 **SQLAllocHandle** 및 **SQLSetEnvAttr** 드라이버에서입니다. 따라서 ODBC 3*.x* 드라이버가이 특성이 설정 되 고 항상 신뢰할 수 있는 합니다.  
  
 표준 호환 응용 프로그램 호출 ODBC_STD 컴파일 플래그를 사용 하 여 컴파일한 **SQLAllocEnv** (때문에 발생할 수 있는 **SQLAllocEnv** ISO에서 사용 되지 되지 않는), 호출에 매핑된  **SQLAllocHandleStd** 컴파일 타임에 있습니다. 런타임 시 응용 프로그램 호출 **SQLAllocHandleStd**합니다. 드라이버 관리자 SQL_OV_ODBC3를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정합니다. 에 대 한 호출 **SQLAllocHandleStd** 에 대 한 호출에 해당 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV 및에 대 한 호출의 **SQLSetEnvAttr** SQL_OV_ODBC3를 sql_attr_odbc_version으로 설정 합니다.  
  
 특정 드라이버 아키텍처에는 어느 ODBC 2로 표시 되도록 드라이버에 대 한 요구가 있습니다. *x* 드라이버 또는 ODBC 3*.x* 드라이버는 연결에 종속 됩니다. 드라이버가 경우 실제로 아닐 드라이버 하지만 다른 드라이버 및 드라이버 관리자 사이 있는 계층. 예를 들어 ODBC Spy와 같은 드라이버를 처럼 가장 될 수 있습니다. 또 다른 예로, EDA/SQL과 같은 게이트웨이로 역할 수 합니다. ODBC 3으로 표시할*.x* 드라이버와 같은 드라이버 내보내기 할 수 있어야 **SQLAllocHandle**, 및 ODBC 2로 표시 되도록 합니다. *x* 드라이버를 내보낼 수 있어야 **SQLAllocConnect**, **SQLAllocEnv**, 및 **SQLAllocStmt**합니다. 드라이버 관리자는 확인 하는 경우이 드라이버 내보냅니다는 환경, 연결 또는 문이 할당 되 면 **SQLAllocHandle**합니다. 드라이버는 드라이버 관리자를 호출 하 여 이후 **SQLAllocHandle** 드라이버에서입니다. 경우 드라이버는 ODBC 2와 작동 합니다. *x* 드라이버를 드라이버에 대 한 호출을 매핑해야 합니다. **SQLAllocHandle** 를 **SQLAllocConnect**, **SQLAllocEnv**, 또는  **SQLAllocStmt**를 적절 하 게 합니다. 등록 하는 것도 수행 해야는 **SQLSetEnvAttr** ODBC 2로 작동 때 호출 됩니다. *x* 드라이버입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Datetime 데이터 형식](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 데이터 형식의 이전 버전과의 호환성](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [고정 길이 책갈피](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 지원](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [SQL_NO_DATA 반환](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [SQLSetPos를 호출하여 데이터 삽입](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [서수로 로딩](../../../odbc/reference/appendixes/loading-by-ordinal.md)
