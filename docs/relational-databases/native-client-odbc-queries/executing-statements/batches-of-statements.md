---
title: 성명서 일괄 처리 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6054ea09c297bc0d8521d0bc3e509585012e8ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297991"
---
# <a name="batches-of-statements"></a>문의 일괄 처리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  명령문 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 일괄 처리에는 세미콜론(;)으로 구분된 두 개 이상의 문이 포함되어 **있으며, SQLExecDirect** 또는 [SQLPrepare Function에](https://go.microsoft.com/fwlink/?LinkId=59360)전달된 단일 문자열에 내장되어 있습니다. 다음은 그 예입니다.  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 일괄 처리를 사용하면 대개 네트워크 트래픽이 줄어들므로 문을 개별적으로 전송하는 것보다 효율적일 수 있습니다. 현재 결과 집합으로 완료되면 [SQLMoreResults를](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 사용하여 다음 결과 집합에 배치합니다.  
  
 ODBC 커서 특성을 행 집합 크기가 1인 정방향 전용의 읽기 전용 커서(기본값)로 설정하면 항상 일괄 처리를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 서버 커서를 사용할 때 일괄 처리를 실행하면 서버 커서가 암시적으로 기본 결과 집합으로 변환됩니다. **SQLExecDirect** 또는 **SQLExecute** 는 SQL_SUCCESS_WITH_INFO 반환하고 **SQLGetDiagRec에** 대한 호출은 다음을 반환합니다.  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;문 실행](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
