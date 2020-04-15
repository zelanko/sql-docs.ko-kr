---
title: 커서에 대한 SQL 문 생성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], statement construction
- ODBC applications, cursors
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
- statements [ODBC], cursors
ms.assetid: 134003fd-9c93-4f5c-a988-045990933b80
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0e422be747c2b47dacb1feb97ba6c00fa1131fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291458"
---
# <a name="constructing-sql-statements-for-cursors"></a>쿼리에 대한 SQL 문 생성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 서버 커서를 사용하여 ODBC 사양에 정의된 커서 기능을 구현합니다. ODBC 응용 프로그램은 [SQLSetStmtAttr을](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 사용하여 다른 문 특성을 설정하여 커서 동작을 제어합니다. 다음은 이러한 특성과 해당 기본값에 대한 설명입니다.  
  
|특성|기본값|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 SQL 문이 실행될 때 이러한 옵션이 기본값으로 설정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 서버 커서를 사용하여 결과 집합을 구현하지 않습니다. 대신 기본 결과 집합을 사용합니다. SQL 문이 실행될 때 이러한 옵션이 기본값에서 변경되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 서버 커서를 사용하여 결과 집합을 구현하려고 시도합니다.  
  
 기본 결과 집합을 사용할 때는 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지원됩니다. 기본 결과 집합을 사용할 경우 실행할 수 있는 SQL 문의 유형에는 제한이 없습니다.  
  
 서버 커서를 사용할 경우에는 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지원되지 않습니다. 서버 커서에서는 여러 결과 집합을 생성하는 SQL 문이 지원되지 않습니다.  
  
 서버 커서에서 지원되지 않는 문 유형은 다음과 같습니다.  
  
-   Batch  
  
     다음 예와 같이 두 개 이상의 개별 SQL SELECT 문으로 작성된 SQL 문  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   여러 SELECT 문이 있는 저장 프로시저  
  
     둘 이상의 SELECT 문이 포함된 저장 프로시저를 실행하는 SQL 문. 여기에는 매개 변수나 변수를 채우는 SELECT 문도 포함됩니다.  
  
-   키워드  
  
     FOR BROWSE 또는 INTO 키워드를 포함하는 SQL 문  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이러한 조건과 일치하는 SQL 문을 서버 커서를 사용하여 실행하면 서버 커서가 암시적으로 기본 결과 집합으로 변환됩니다. **SQLExecDirect** 또는 **SQLExecute가** SQL_SUCCESS_WITH_INFO 반환하면 커서 특성이 기본 설정으로 다시 설정됩니다.  
  
 위의 범주에 맞지 않는 SQL 문은 모든 문 특성 설정을 사용하여 실행할 수 있으며, 기본 결과 집합이나 서버 커서 중 무엇을 사용하든 동일하게 작동합니다.  
  
## <a name="errors"></a>오류  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이상에서 여러 결과 집합을 반환하는 문을 실행하려고 하면 SQL_SUCCESS_WITH INFO 및 다음 메시지가 생성됩니다.  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 이 메시지를 받는 ODBC 응용 프로그램은 [SQLGetStmtAttr을](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) 호출하여 현재 커서 설정을 확인할 수 있습니다.  
  
 서버 커서를 사용할 때 여러 SELECT 문이 포함된 프로시저를 실행하려고 하면 다음 오류가 생성됩니다.  
  
```  
SqlState: 42000  
pfNative: 16937  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               A server cursor is not allowed on a stored procedure  
               with more than one SELECT statement in it. Use a  
               default result set or client cursor.  
```  
  
 서버 커서를 사용할 때 여러 SELECT 문이 포함된 일괄 처리를 실행하려고 하면 다음 오류가 생성됩니다.  
  
```  
SqlState: 42000  
pfNative: 16938  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               sp_cursoropen. The statement parameter can only  
               be a single SELECT statement or a single stored   
               procedure.  
```  
  
 이 오류를 수신하는 ODBC 애플리케이션은 문을 실행하기 전에 모든 커서 문 특성을 기본값으로 다시 설정해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;쿼리 실행](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
