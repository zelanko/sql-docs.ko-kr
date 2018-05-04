---
title: 메시지를 생성 하는 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9475afda740b4c2b2d6b279c0ea0a454fd397bf0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="processing-statements-that-generate-messages"></a>메시지를 생성하는 문 처리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] SET 문 옵션 STATISTICS TIME 및 STATISTICS IO를 사용하여 장기 실행 쿼리를 진단하는 데 유용한 정보를 얻을 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 쿼리 계획을 분석하는 SHOWPLAN 옵션을 지원합니다. ODBC 응용 프로그램은 다음 문을 실행하여 이러한 옵션을 설정할 수 있습니다.  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 ON 이면 SET STATISTICS TIME 또는 SET SHOWPLAN 경우 **SQLExecute** 및 **SQLExecDirect** 가 SQL_SUCCESS_WITH_INFO를 반환 하 고 해당 시점에 응용 프로그램 SHOWPLAN 또는 STATISTICS 타임 출력을 검색할 수 있습니다 호출 하 여 **SQLGetDiagRec** sql_no_data가 반환 될 때까지 합니다. 각 SHOWPLAN 데이터 행은 다음과 같은 형식으로 반환됩니다.  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0에서 SHOWPLAN 옵션은 출력을 메시지 집합이 아닌 결과 집합으로 반환하는 SHOWPLAN_ALL 및 SHOWPLAN_TEXT로 대체되었습니다.  
  
 각 STATISTICS TIME 행은 다음과 같은 형식으로 반환됩니다.  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 SET STATISTICS IO의 출력은 결과 집합의 끝에 도달할 때까지 표시되지 않습니다. STATISTICS IO 출력을 호출 하 여 응용 프로그램을 가져올 **SQLGetDiagRec** 당시 **SQLFetch** 또는 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) SQL_NO_DATA를 반환 합니다. STATISTICS IO 출력은 다음과 같은 형식으로 반환됩니다.  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>DBCC 문 사용  
 DBCC 문은 데이터를 결과 집합이 아닌 메시지로 반환합니다. **SQLExecDirect** 또는 **SQLExecute** SQL_SUCCESS_WITH_INFO를 및 응용 프로그램 출력을 호출 하 여 검색 반환 **SQLGetDiagRec** sql_no_data가 반환 될 때까지 합니다.  
  
 예를 들어 다음 문은 SQL_SUCCESS_WITH_INFO를 반환합니다.  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 에 대 한 호출이 **SQLGetDiagRec** 반환:  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>PRINT 및 RAISERROR 문 사용  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT 및 RAISERROR 문의 호출 하 여 데이터를 반환할 수도 **SQLGetDiagRec**합니다. 인쇄 문은 SQL_SUCCESS_WITH_INFO를 및 후속 호출을 반환 하는 SQL 문 실행 **SQLGetDiagRec** 반환는 *SQLState* 01000 합니다. 심각도가 10 이하인 RAISERROR는 PRINT와 동일하게 동작합니다. 실행이 SQL_ERROR를 및 후속 호출을 반환 하는 심각도 11 이상인 RAISERROR가 발생 하면 **SQLGetDiagRec** 반환 *SQLState* 42000 합니다. 예를 들어 다음 문은 SQL_SUCCESS_WITH_INFO를 반환합니다.  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 호출 **SQLGetDiagRec** 반환:  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 다음 문은 SQL_SUCCESS_WITH_INFO를 반환합니다.  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 호출 **SQLGetDiagRec** 반환:  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 다음 문은 SQL_ERROR를 반환합니다.  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 호출 **SQLGetDiagRec** 반환:  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 호출의 타이밍 **SQLGetDiagRec** PRINT 또는 RAISERROR 문의 출력 결과 집합에 포함 되 면이 중요 합니다. 에 대 한 호출 **SQLGetDiagRec** 검색할 PRINT 또는 RAISERROR 출력 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 수신 하는 문 바로 뒤 수행 합니다. 위의 예에서와 같이 단일 SQL 문만 실행하는 경우에는 간단합니다. 이러한 경우에 대 한 호출 **SQLExecDirect** 또는 **SQLExecute** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하 고 **SQLGetDiagRec** 호출할 수 있습니다. 하지만 SQL 문 일괄 처리의 출력을 처리하는 루프를 코딩할 때나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저를 실행할 때는 이보다 복잡합니다.  
  
 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 일괄 처리 또는 저장 프로시저에서 실행된 각 SELECT 문마다 결과 집합을 하나씩 반환합니다. 일괄 처리 또는 프로시저에 PRINT 또는 RAISERROR 문이 포함된 경우 SELECT 문 결과 집합에 이러한 문의 출력이 인터리브됩니다. 일괄 처리 또는 프로시저에서 첫 번째 문이 PRINT 또는 RAISERROR 인 경우는 **SQLExecute** 또는 **SQLExecDirect** 를 호출해야하는SQL_SUCCESS_WITH_INFO또는SQL_ERROR와응용프로그램반환**SQLGetDiagRec** PRINT 또는 RAISERROR 정보를 검색 하기 위해 sql_no_data가 반환 될 때까지 합니다.  
  
 PRINT 또는 RAISERROR 문 (예: SELECT 문), SQL 문 다음에 오는 경우 PRINT 또는 RAISERROR 정보 때 반환 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)결과에 위치 오류를 포함 하는 설정입니다. **SQLMoreResults** 메시지의 심각도 따라 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 반환 합니다. 메시지를 호출 하 여 검색 **SQLGetDiagRec** sql_no_data가 반환 될 때까지 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
