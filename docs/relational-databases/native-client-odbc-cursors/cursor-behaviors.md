---
title: 커서 동작 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2e3400e52cd0b7574c07a3cf813b4cbca317df2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305494"
---
# <a name="cursor-behaviors"></a>커서 동작
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC는 커서의 스크롤 가능 여부 및 민감도를 지정하여 커서의 동작을 지정하는 ISO 옵션을 지원합니다. 이러한 동작은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)에 대한 호출에서 SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY 옵션을 설정하여 지정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 다음과 같은 특징을 가진 서버 커서를 요청하여 이러한 옵션을 구현합니다.  
  
|커서 동작 설정|필요한 서버 커서 특징|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 및 SQL_SENSITIVE|키 집합 커서 및 버전 기반 낙관적 동시성|  
|SQL_SCROLLABLE 및 SQL_INSENSITIVE|정적 커서 및 읽기 전용 동시성|  
|SQL_SCROLLABLE 및 SQL_UNSPECIFIED|정적 커서 및 읽기 전용 동시성|  
|SQL_NONSCROLLABLE 및 SQL_SENSITIVE|정방향 전용 커서 및 버전 기반 낙관적 동시성|  
|SQL_NONSCROLLABLE 및 SQL_INSENSITIVE|기본 결과 집합(정방향 전용, 읽기 전용)|  
|SQL_NONSCROLLABLE 및 SQL_UNSPECIFIED|기본 결과 집합(정방향 전용, 읽기 전용)|  
  
 버전 기반 낙관적 동시성은 기본 테이블의 **타임스탬프** 열이 필요합니다. **타임스탬프** 열이 없는 테이블에서 버전 기반 낙관적 동시성 제어가 요청되면 서버는 값 기반 낙관적 동시성을 사용합니다.  
  
## <a name="scrollability"></a>스크롤 가능 여부  
 SQL_ATTR_CURSOR_SCROLLABLE SQL_SCROLLABLE 설정되면 커서는 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)의 *FetchOrientation* 매개 변수에 대한 모든 다른 값을 지원합니다. SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE 설정하면 커서는 *SQL_FETCH_NEXT FetchOrientation* 값만 지원합니다.  
  
## <a name="sensitivity"></a>민감도  
 SQL_ATTR_CURSOR_SENSITIVITY가 SQL_SENSITIVE로 설정되면 커서는 현재 사용자가 수행하거나 다른 사용자가 커밋한 데이터 수정 내용을 반영합니다. SQL_ATTR_CURSOR_SENSITIVITY가 SQL_INSENSITIVE로 설정되면 커서는 데이터 수정 내용을 반영하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서(ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [커서 속성](properties/cursor-properties.md) 사용 
  
  
