---
title: 동작 변경 내용 및 ODBC 3.x 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e386aa60489fe3edb2caac3cb49ebad263ffdfac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740051"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>동작 변경 및 ODBC 3.x 드라이버
환경 특성 SQL_ATTR_ODBC_VERSION 나타내며 드라이버 ODBC 2 발생 해야 하는지 여부를 *x* 동작 또는 ODBC 3 *.x* 동작 합니다. SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하는 방법을 응용 프로그램에 따라 달라 집니다. ODBC 3 *.x* 응용 프로그램을 호출 해야 **SQLSetEnvAttr** 호출 후에이 특성을 설정 하려면 **SQLAllocHandle** 환경 핸들을 할당 하려면 를호출하기전에및 **SQLAllocHandle** 연결 핸들을 할당 합니다. 드라이버 관리자 SQLSTATE HY010 반환이 실패 하는 경우 (함수 시퀀스 오류)의 두 번째 호출에서 **SQLAllocHandle**합니다.  
  
> [!NOTE]  
>  동작 변경 내용 및 응용 프로그램의 작업 방식에 대 한 자세한 내용은 참조 하세요. [동작 변경 내용](../../../odbc/reference/develop-app/behavioral-changes.md)합니다.  
  
 ODBC 2입니다. *x* 응용 프로그램 및 ODBC 2. *x* 응용 프로그램을 ODBC 3을 사용 하 여 다시 컴파일할 *.x* 헤더 파일을 호출 하지 마십시오 **SQLSetEnvAttr**합니다. 하지만 호출 **SQLAllocEnv** 대신 **SQLAllocHandle** 환경 핸들을 할당 합니다. 따라서 응용 프로그램 호출 하는 경우 **SQLAllocEnv** 드라이버 관리자에서 드라이버 관리자 호출 **SQLAllocHandle** 하 고 **SQLSetEnvAttr** 드라이버에서. ODBC 3 따라서 *.x* 드라이버 항상 수이 특성을 설정 합니다.  
  
 호출 ODBC_STD 컴파일 플래그를 사용 하 여 표준 호환 응용 프로그램을 컴파일한 **SQLAllocEnv** (때문에 발생할 수 있는 **SQLAllocEnv** iso에서 되지 됩니다), 호출에 매핑된  **SQLAllocHandleStd** 컴파일 타임에 있습니다. 런타임 시 응용 프로그램 호출 **SQLAllocHandleStd**합니다. 드라이버 관리자 SQL_OV_ODBC3를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정합니다. 에 대 한 호출 **SQLAllocHandleStd** 를 호출 하는 것과 같습니다 **SQLAllocHandle** 사용 하 여는 *HandleType* SQL_HANDLE_ENV 및에 대 한 호출의 **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3으로 설정 합니다.  
  
 특정 드라이버 아키텍처 중 하나는 ODBC 2로 표시 되도록 드라이버에 대 한 요구가 있습니다. *x* 드라이버나는 ODBC 3 *.x* 연결에 따라 드라이버입니다. 드라이버가 경우 실제로 아닐 드라이버 하지만 드라이버 관리자 및 다른 드라이버 사이 있는 계층입니다. 예를 들어 ODBC Spy와 같은 드라이버를 모방 수 것입니다. 또 다른 예로, EDA/s q L 같이 게이트웨이로 동작을 수행할 수 것입니다. ODBC 3으로 표시할 *.x* 드라이버와 같은 드라이버 내보내기 할 수 있어야 **SQLAllocHandle**, 및는 ODBC 2로 표시 되도록 합니다. *x* 드라이버를 내보낼 수 있어야 **SQLAllocConnect**합니다 **SQLAllocEnv**, 및 **SQLAllocStmt**합니다. 환경, 연결 또는 문이 할당 될 때 드라이버 관리자를 확인 하는 경우이 드라이버 내보냅니다 **SQLAllocHandle**합니다. 드라이버는 드라이버 관리자 호출 하므로 **SQLAllocHandle** 드라이버에서입니다. 드라이버는 ODBC 2 작동 하는 경우. *x* 드라이버를 드라이버에 대 한 호출을 매핑해야 합니다 **SQLAllocHandle** 하 **SQLAllocConnect**하십시오 **SQLAllocEnv**, 또는  **SQLAllocStmt**를 적절 하 게 합니다. 등록 하는 것도 수행 해야 합니다 **SQLSetEnvAttr** 는 ODBC 2로 작동 하는 경우 호출 합니다. *x* 드라이버입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Datetime 데이터 형식](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 데이터 형식의 이전 버전과의 호환성](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [고정 길이 책갈피](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 지원](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [SQL_NO_DATA 반환](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [SQLSetPos를 호출하여 데이터 삽입](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [서수로 로딩](../../../odbc/reference/appendixes/loading-by-ordinal.md)
