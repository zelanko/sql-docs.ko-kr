---
title: 행동 변화 및 ODBC 3.x 드라이버 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8343573261d74a6a0c652cf425b12da91f7cb0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292367"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>동작 변경 및 ODBC 3.x 드라이버
SQL_ATTR_ODBC_VERSION 환경 특성은 ODBC *2.x* 동작 또는 ODBC *3.x* 동작을 표시해야 하는지 여부를 드라이버에 나타냅니다. SQL_ATTR_ODBC_VERSION 환경 특성이 설정되는 방법은 응용 프로그램에 따라 다릅니다. ODBC *3.x* 응용 프로그램은 **SQLSetEnvAttr을** 호출하여 **SQLAllocHandle을** 호출하여 환경 핸들을 할당하고 **SQLAllocHandle을** 호출하여 연결 핸들을 할당하기 전에 이 특성을 설정해야 합니다. 이 작업을 수행하지 못하면 드라이버 관리자는 후자 의 **SQLAllocHandle**에 대한 후자의 호출에서 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다.  
  
> [!NOTE]  
>  행동 변경 및 응용 프로그램의 작동 방식에 대한 자세한 내용은 [행동 변경](../../../odbc/reference/develop-app/behavioral-changes.md)을 참조하십시오.  
  
 ODBC *2.x* 응용 프로그램 및 ODBC *2.x* 응용 *3.x* 프로그램은 **SQLSetEnvAttr을**호출하지 않습니다. 그러나 **SQLAllocHandle 대신 SQLAllocEnv를** 호출하여 환경 핸들을 할당합니다. **SQLAllocHandle** 따라서 응용 프로그램이 드라이버 관리자에서 **SQLAllocEnv를** 호출할 때 드라이버 관리자는 **드라이버에서 SQLAllocHandle** 및 **SQLSetEnvAttr을** 호출합니다. 따라서 ODBC *3.x* 드라이버는 항상 설정 중인 이 특성을 믿을 수 있습니다.  
  
 ODBC_STD 컴파일 플래그로 컴파일된 표준을 준수하는 응용 프로그램이 **SQLAllOcEnv를** 호출하는 **경우(이는 SQLAllocEnv가** ISO에서 더 이상 사용되지 않기 때문에 발생할 수 있음) 컴파일 시 **SQLAllocHandleStd에** 매핑됩니다. 런타임에 응용 프로그램은 **SQLAllocHandleStd를**호출합니다. 드라이버 관리자는 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3 설정합니다. **SQLAllocHandleStd에** 대 한 호출은 *SQL_HANDLE_ENV 핸들 유형및* **SQLSetEnvAttr에** 대 한 호출을 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION 설정 하는 **SQLAllocHandle에** 대 한 호출에 해당 합니다.  
  
 특정 드라이버 아키텍처에서는 드라이버가 연결에 따라 ODBC *2.x* 드라이버 또는 ODBC *3.x* 드라이버로 표시해야 합니다. 이 경우 드라이버는 실제로 드라이버가 아니라 드라이버 관리자와 다른 드라이버 사이에 있는 레이어일 수 있습니다. 예를 들어 ODBC 스파이와 같은 드라이버를 모방할 수 있습니다. 또 다른 예에서는 EDA/SQL과 같은 게이트웨이 역할을 할 수 있습니다. ODBC *3.x* 드라이버로 표시하려면 이러한 드라이버는 **SQLAllocHandle을**내보낼 수 있어야 하며 ODBC *2.x* 드라이버로 표시하려면 **SQLAllocConnect,** **SQLAllocEnv**및 **SQLAllocStmt를**내보낼 수 있어야 합니다. 환경, 연결 또는 문을 할당할 때 드라이버 관리자는 이 드라이버가 **SQLAllocHandle**을 내보내는지 확인합니다. 드라이버가 수행하므로 드라이버 관리자는 드라이버에서 **SQLAllocHandle을** 호출합니다. 드라이버가 ODBC *2.x* 드라이버로 작업하는 경우 드라이버는 **SQLAllocHandle에** 대한 호출을 **SQLAllocConnect,** **SQLAllocEnv**또는 **SQLAllocStmt에**적절하게 매핑해야 합니다. 또한 ODBC *2.x* 드라이버로 작동 할 때 **SQLSetEnvAttr** 호출로 아무 것도하지 않아야합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Datetime 데이터 형식](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 데이터 형식의 이전 버전과의 호환성](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [고정 길이 책갈피](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 지원](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [SQL_NO_DATA 반환](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [SQLSetPos를 호출하여 데이터 삽입](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [서수로 로딩](../../../odbc/reference/appendixes/loading-by-ordinal.md)
