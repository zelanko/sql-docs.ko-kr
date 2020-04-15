---
title: SQL 서버 기본 결과 집합 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08926660face8061abdf8352d0c4a84ad7e67f8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305400"
---
# <a name="using-sql-server-default-result-sets"></a>SQL Server 기본 결과 집합 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  기본 ODBC 커서 특성은 다음과 같습니다.  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 이러한 특성이 기본값으로 설정될 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 때마다 네이티브 클라이언트 ODBC 드라이버는 기본 결과 집합을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용합니다. 기본 결과 집합은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 지원하는 모든 SQL 문에서 사용할 수 있으며 클라이언트에 전체 결과 집합을 전송하는 가장 효율적인 방법입니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]여러 활성 결과 세트 (화성)에 대한 지원 도입; 이제 응용 프로그램에는 연결당 두 개 이상의 활성 기본 결과가 설정될 수 있습니다. MARS 기능은 기본적으로 해제됩니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전에는 기본 결과 집합이 동일한 연결에서 다중 활성 문을 지원하지 않았습니다. 따라서 연결에서 SQL 문을 실행한 후 결과 집합의 모든 행이 처리될 때까지 서버가 클라이언트에서 나머지 결과 집합을 취소하는 요청을 제외한 다른 명령을 받지 않았습니다. 부분적으로 처리된 결과 집합의 나머지 부분을 취소하려면 *SQL_CLOSE fOption* 매개 변수를 사용하여 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) 또는 [SQLFreeStmt를](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 호출합니다. 부분적으로 처리된 결과 집합을 완료하고 다른 결과 집합이 있는지 테스트하려면 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 호출합니다. ODBC 응용 프로그램이 기본 결과 집합이 완전히 처리되기 전에 연결 핸들에서 명령을 시도하는 경우 호출은 SQL_ERROR 생성하고 **SQLGetDiagRec에** 대한 호출은 반환합니다.  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>참고 항목  
 [커서 구현 방법](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
