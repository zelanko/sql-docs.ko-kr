---
title: ODBC 커서 라이브러리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1ff52345cf4afa65ebb4e183a9a012dd9d197419
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425612"
---
# <a name="odbc-cursor-library"></a>ODBC 커서 라이브러리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  일부 ODBC 드라이버는 기본 커서 설정만; 지원 이러한 드라이버도 지원 하지 않습니다 위치 지정된 커서 작업의 경우와 같은 **SQLSetPos**합니다. ODBC 커서 라이브러리는 일반적으로 블록 또는 정적 커서를 지원하지 않는 드라이버에서 블록 또는 정적 커서를 구현하는 데 사용되는 MDAC(Microsoft Data Access Components) 구성 요소입니다. 커서 라이브러리 위치 지정된 UPDATE 및 DELETE 문을 구현 하 고 **SQLSetPos** 만드는 커서에 대 한 합니다.  
  
 ODBC 커서 라이브러리는 ODBC 드라이버 관리자와 ODBC 드라이버 사이의 계층으로 구현됩니다. ODBC 커서 라이브러리가 로드되면 ODBC 드라이버 관리자에서 모든 커서 관련 명령을 드라이버 대신 커서 라이브러리로 라우팅합니다. 커서 라이브러리는 기본 드라이버에서 전체 결과 집합을 인출하고 결과 집합을 클라이언트에 캐시하여 커서를 구현합니다. ODBC 커서 라이브러리를 사용하는 경우 응용 프로그램은 커서 라이브러리의 커서 기능으로 제한됩니다. 기본 드라이버의 추가 커서 기능에 대한 지원은 응용 프로그램에서 사용할 수 없습니다.  
  
 드라이버 자체에서 ODBC 커서 라이브러리보다 많은 커서 기능을 지원하므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 ODBC 커서 라이브러리를 사용할 필요는 없습니다. ODBC 커서 라이브러리를 사용 하는 유일한 이유는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 드라이버가 서버 커서를 통해 커서 지원을 구현 이므로 서버 커서는 모든 SQL 문을 지원 하지 않습니다. 저장 프로시저, 일괄 처리 또는 COMPUTE, COMPUTE BY, FOR BROWSE 또는 INTO가 포함된 SQL 문에 정적 커서가 필요한 경우 ODBC 커서 라이브러리를 사용합니다. 하지만 커서 라이브러리는 전체 결과 집합을 클라이언트에 캐시하여 많은 메모리가 사용되고 성능이 저하될 수 있으므로 주의해야 합니다.  
  
 사용 하 여 연결 하 여 연결 단위로 커서 라이브러리를 호출 하는 응용 프로그램 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 데이터 원본에 연결 하기 전에 SQL_ATTR_ODBC_CURSORS 연결 특성을 설정 합니다. SQL_ATTR_ODBC_CURSORS는 다음 세 값 중 하나로 설정됩니다.  
  
 SQL_CUR_USE_ODBC  
 사용 하 여이 옵션을 설정 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 ODBC 커서 라이브러리 재정의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 기본 커서 지원을 합니다. 커서 라이브러리에서 지원되는 커서 유형만 연결에 사용할 수 있으며 서버 커서는 사용할 수 없습니다.  
  
 SQL_CUR_USE_DRIVER  
 이 옵션을 설정 하면 모든 커서 지원을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결에 사용할 수 있습니다. ODBC 커서 라이브러리는 사용할 수 없습니다. 모든 커서가 서버 커서로 구현됩니다.  
  
 SQL_CUR_USE_IF_NEEDED  
 이 옵션을 설정 하는 경우 효과와 함께 사용할 경우 SQL_CUR_USE_DRIVER와 동일 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버. 연결 시 ODBC 드라이버 관리자 연결 되는 ODBC 드라이버의 SQL_FETCH_PRIOR 옵션을 지원 하는지 확인 하려면 테스트 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)합니다. 드라이버가 이 옵션을 지원하지 않으면 ODBC 드라이버 관리자에서 ODBC 커서 라이브러리를 로드합니다. 드라이버가 이 옵션을 지원하면 ODBC 드라이버 관리자에서 ODBC 커서 라이브러리를 로드하지 않으며 응용 프로그램이 드라이버의 기본 지원을 사용합니다. 때문에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 SQL_FETCH_PRIOR를 ODBC 드라이버 관리자에서 ODBC 커서 라이브러리를 로드 하지 않습니다.  
  
 커서 라이브러리를 사용하면 응용 프로그램이 스크롤 및 업데이트 가능한 커서는 물론 한 연결에서 활성 문을 여러 개 사용할 수 있습니다. 이 기능을 지원하려면 커서 라이브러리를 로드해야 합니다. 사용 하 여 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 커서 라이브러리를 사용 하는 방법을 지정 하 고 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 커서 유형, 동시성 및 행 집합 크기를 지정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [커서 구현 방법](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
