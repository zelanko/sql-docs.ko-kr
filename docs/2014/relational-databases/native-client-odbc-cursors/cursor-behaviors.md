---
title: 커서 동작 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c5ded9f42da267cfd137f0adfd4465d965d9a06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188569"
---
# <a name="cursor-behaviors"></a>커서 동작
  ODBC는 커서의 스크롤 가능 여부 및 민감도를 지정하여 커서의 동작을 지정하는 ISO 옵션을 지원합니다. 이러한 동작은 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)에 대 한 호출에서 SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY 옵션을 설정 하 여 지정 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 다음과 같은 특징을 가진 서버 커서를 요청하여 이러한 옵션을 구현합니다.  
  
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
 SQL_ATTR_CURSOR_SCROLLABLE을 SQL_SCROLLABLE로 설정 하면 커서가 [Sqlfetchscroll](../native-client-odbc-api/sqlfetchscroll.md)의 *fetchorientation* 매개 변수에 대해 다른 모든 값을 지원 합니다. SQL_ATTR_CURSOR_SCROLLABLE을 SQL_NONSCROLLABLE로 설정 하면 커서는 SQL_FETCH_NEXT의 *Fetchorientation* 값만 지원 합니다.  
  
## <a name="sensitivity"></a>민감도  
 SQL_ATTR_CURSOR_SENSITIVITY가 SQL_SENSITIVE로 설정되면 커서는 현재 사용자가 수행하거나 다른 사용자가 커밋한 데이터 수정 내용을 반영합니다. SQL_ATTR_CURSOR_SENSITIVITY가 SQL_INSENSITIVE로 설정되면 커서는 데이터 수정 내용을 반영하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 사용](using-cursors-odbc.md)  
  
  
