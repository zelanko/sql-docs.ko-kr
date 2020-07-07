---
title: 커서 동작 | Microsoft Docs
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
ms.openlocfilehash: 65ee29f4bab4994f3d96bd4cacdbab65c46ab305
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000640"
---
# <a name="cursor-behaviors"></a>커서 동작
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC는 커서의 스크롤 가능 여부 및 민감도를 지정하여 커서의 동작을 지정하는 ISO 옵션을 지원합니다. 이러한 동작은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)에 대 한 호출에서 SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY 옵션을 설정 하 여 지정 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 다음과 같은 특징을 가진 서버 커서를 요청하여 이러한 옵션을 구현합니다.  
  
|커서 동작 설정|필요한 서버 커서 특징|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 및 SQL_SENSITIVE|키 집합 커서 및 버전 기반 낙관적 동시성|  
|SQL_SCROLLABLE 및 SQL_INSENSITIVE|정적 커서 및 읽기 전용 동시성|  
|SQL_SCROLLABLE 및 SQL_UNSPECIFIED|정적 커서 및 읽기 전용 동시성|  
|SQL_NONSCROLLABLE 및 SQL_SENSITIVE|정방향 전용 커서 및 버전 기반 낙관적 동시성|  
|SQL_NONSCROLLABLE 및 SQL_INSENSITIVE|기본 결과 집합(정방향 전용, 읽기 전용)|  
|SQL_NONSCROLLABLE 및 SQL_UNSPECIFIED|기본 결과 집합(정방향 전용, 읽기 전용)|  
  
 버전 기반 낙관적 동시성을 사용 하려면 기본 테이블에 **timestamp** 열이 있어야 합니다. **Timestamp** 열이 없는 테이블에 대해 버전 기반 낙관적 동시성 제어를 요청 하는 경우 서버는 값 기반 낙관적 동시성을 사용 합니다.  
  
## <a name="scrollability"></a>스크롤 가능 여부  
 SQL_ATTR_CURSOR_SCROLLABLE을 SQL_SCROLLABLE로 설정 하면 커서가 [Sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)의 *fetchorientation* 매개 변수에 대해 다른 모든 값을 지원 합니다. SQL_ATTR_CURSOR_SCROLLABLE을 SQL_NONSCROLLABLE로 설정 하면 커서는 SQL_FETCH_NEXT의 *Fetchorientation* 값만 지원 합니다.  
  
## <a name="sensitivity"></a>민감도  
 SQL_ATTR_CURSOR_SENSITIVITY가 SQL_SENSITIVE로 설정되면 커서는 현재 사용자가 수행하거나 다른 사용자가 커밋한 데이터 수정 내용을 반영합니다. SQL_ATTR_CURSOR_SENSITIVITY가 SQL_INSENSITIVE로 설정되면 커서는 데이터 수정 내용을 반영하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 커서 [(ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [커서 속성](properties/cursor-properties.md) 사용 
  
  
