---
description: 커서 사용(ODBC)
title: 커서 사용 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], how to topics
ms.assetid: c502736f-bca0-45c3-ae25-d2ad52d296bf
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ebea27cac6309c6946d664c6a0a80d5b3787f81
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467804"
---
# <a name="use-cursors-odbc"></a>커서 사용(ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-use-cursors"></a>커서를 사용하려면  
  
1.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 호출하여 원하는 커서 특성을 설정합니다.  
  
     SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 특성을 설정합니다(기본 옵션).  
  
     또는  
  
     SQL_CURSOR_SCROLLABLE 및 SQL_CURSOR_SENSITIVITY 특성을 설정합니다.  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 호출하여 SQL_ATTR_ROW_ARRAY_SIZE 특성으로 행 집합 크기를 설정합니다.  
  
3.  필요한 경우 WHERE CURRENT OF 절을 사용하여 위치 지정 업데이트를 수행하려면 [SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)을 호출하여 커서 이름을 설정합니다.  
  
4.  SQL 문을 실행합니다.  
  
5.  필요한 경우 WHERE CURRENT OF 절을 사용하여 위치 지정 업데이트를 수행하려면 [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)을 호출하여 커서 이름을 가져옵니다(3단계에서 [SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)을 사용하여 커서 이름을 지정하지 않은 경우).  
  
6.  [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)를 호출하여 행 집합의 열 수(C)를 가져옵니다.  
  
     열 단위 바인딩을 사용합니다.  
  
     \- 또는 -  
  
     행 단위 바인딩을 사용합니다.  
  
7.  커서에서 원하는 대로 행 집합을 인출합니다.  
  
8.  [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 호출하여 다른 결과 집합이 있는지 확인합니다.  
  
    -   다른 결과 집합이 있으면 SQL_SUCCESS가 반환됩니다.  
  
    -   다른 결과 집합이 없으면 SQL_NO_DATA가 반환됩니다.  
  
    -   SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR가 반환되면 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)를 호출하여 사용할 수 있는 PRINT 또는 RAISERROR 문 출력이 있는지 확인합니다.  
  
     바인딩된 문 매개 변수가 출력 매개 변수 또는 저장 프로시저의 반환 값으로 사용될 경우 바인딩된 매개 변수 버퍼에서 현재 사용할 수 있는 데이터를 사용합니다.  
  
     바인딩된 매개 변수를 사용하면 [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md) 또는 [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)를 호출할 때마다 SQL 문이 S번 실행됩니다. 여기서 S는 바인딩된 매개 변수 배열에 포함된 요소 수입니다. 이는 S개의 결과 집합을 처리해야 함을 의미하며, 각 결과 집합은 SQL 문을 한 번 실행했을 때 일반적으로 반환되는 모든 결과 집합, 출력 매개 변수 및 반환 코드 전체로 구성됩니다.  
  
     결과 집합에 컴퓨팅 행이 포함된 경우 각 컴퓨팅 행은 별도의 결과 집합으로 사용할 수 있습니다. 이러한 컴퓨팅 결과 집합은 일반 행 내에 섞여 일반 행을 여러 개의 결과 집합으로 나눕니다.  
  
9. 필요에 따라 SQL_UNBIND와 함께 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)를 호출하여 바인딩된 열 버퍼를 해제합니다.  
  
10. 다른 결과 집합이 있으면 6단계부터 반복합니다.  
  
     9단계에서 부분적으로 처리된 결과 집합에 대해 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 호출하면 나머지 결과 집합이 지워집니다. [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)를 호출하여 부분적으로 처리된 결과 집합을 지울 수도 있습니다.  
  
     SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY를 설정하거나 SQL_ATTR_CURSOR_SENSITIVITY 및 SQL_ATTR_CURSOR_SCROLLABLE을 설정하여 사용되는 커서 유형을 제어할 수 있습니다. 커서 동작을 지정할 때 이 두 방법을 함께 사용하면 안 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 사용 방법 항목 ODBC&#41;&#40;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
