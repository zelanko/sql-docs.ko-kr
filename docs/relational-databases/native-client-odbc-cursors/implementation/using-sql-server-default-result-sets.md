---
title: SQL Server 기본 결과 집합을 사용 하 여 | Microsoft Docs
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
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 867a0aa7d51e64de9ec55ce5016fb791b3afd5cd
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073756"
---
# <a name="using-sql-server-default-result-sets"></a>SQL Server 기본 결과 집합 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  기본 ODBC 커서 특성은 다음과 같습니다.  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 때마다 이러한 특성을 기본값으로 설정 됩니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 사용을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 결과 집합입니다. 기본 결과 집합은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 지원하는 모든 SQL 문에서 사용할 수 있으며 클라이언트에 전체 결과 집합을 전송하는 가장 효율적인 방법입니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 다중 활성 결과 집합 (MARS);에 대 한 지원 도입된 응용 프로그램 둘 이상의 활성 기본 결과 집합 연결당 이제 있습니다. MARS 기능은 기본적으로 해제됩니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전에는 기본 결과 집합이 동일한 연결에서 다중 활성 문을 지원하지 않았습니다. 따라서 연결에서 SQL 문을 실행한 후 결과 집합의 모든 행이 처리될 때까지 서버가 클라이언트에서 나머지 결과 집합을 취소하는 요청을 제외한 다른 명령을 받지 않았습니다. 부분적으로 처리 된 결과 집합의 나머지 부분을 취소 하려면 호출 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) 하거나 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 사용 하 여는 *fOption* 매개 변수를 SQL_CLOSE로 설정 합니다. 부분적으로 처리 된 결과 집합을 다른 결과 집합의 현재 상태에 대 한 테스트를 완료 하려면 호출 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)합니다. 기본 결과 집합을 아직 완전히 처리 하기 전에 연결 핸들의 명령을 시도 하는 ODBC 응용 프로그램을 호출 하면 SQL_ERROR와 생성에 대 한 호출 **SQLGetDiagRec** 반환 합니다.  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>관련 항목  
 [커서 구현 방법](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
