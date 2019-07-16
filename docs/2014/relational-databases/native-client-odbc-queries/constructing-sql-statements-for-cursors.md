---
title: 커서에 대 한 SQL 문 생성 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dc86f27ab9e111c5d93c91de65c51da9008ba33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207084"
---
# <a name="constructing-sql-statements-for-cursors"></a>쿼리에 대한 SQL 문 생성
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 서버 커서를 사용 하 여 ODBC 사양에 정의 된 커서 기능을 구현 합니다. ODBC 응용 프로그램을 사용 하 여 커서 동작을 제어 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 다른 문 특성을 설정할 수 있습니다. 다음은 이러한 특성과 해당 기본값에 대한 설명입니다.  
  
|attribute|기본값|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 SQL 문을 실행할 때 이러한 옵션을 기본값으로 설정 된 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합을 구현 하는 서버 커서를 사용 하지 않습니다; 대신 기본 결과 집합을 사용 합니다. 이러한 옵션 중 하나는 SQL 문을 실행할 때 해당 기본값에서 변경 되는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합을 구현 하는 서버 커서를 사용 하려고 합니다.  
  
 기본 결과 집합을 사용할 때는 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지원됩니다. 기본 결과 집합을 사용할 경우 실행할 수 있는 SQL 문의 유형에는 제한이 없습니다.  
  
 서버 커서를 사용할 경우에는 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지원되지 않습니다. 서버 커서에서는 여러 결과 집합을 생성하는 SQL 문이 지원되지 않습니다.  
  
 서버 커서에서 지원되지 않는 문 유형은 다음과 같습니다.  
  
-   일괄 처리  
  
     다음 예와 같이 두 개 이상의 개별 SQL SELECT 문으로 작성된 SQL 문  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   여러 SELECT 문이 있는 저장 프로시저  
  
     둘 이상의 SELECT 문이 포함된 저장 프로시저를 실행하는 SQL 문. 여기에는 매개 변수나 변수를 채우는 SELECT 문도 포함됩니다.  
  
-   키워드  
  
     FOR BROWSE 또는 INTO 키워드를 포함하는 SQL 문  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이러한 조건과 일치하는 SQL 문을 서버 커서를 사용하여 실행하면 서버 커서가 암시적으로 기본 결과 집합으로 변환됩니다. 이후에 **SQLExecDirect** 하거나 **SQLExecute** 커서 특성이 기본 설정으로 다시 설정 됩니다, SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 위의 범주에 맞지 않는 SQL 문은 모든 문 특성 설정을 사용하여 실행할 수 있으며, 기본 결과 집합이나 서버 커서 중 무엇을 사용하든 동일하게 작동합니다.  
  
## <a name="errors"></a>오류  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이상에서 여러 결과 집합을 반환하는 문을 실행하려고 하면 SQL_SUCCESS_WITH INFO 및 다음 메시지가 생성됩니다.  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 이 메시지를 수신 하는 ODBC 응용 프로그램에서 호출할 수 있습니다 [SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md) 현재 커서 설정을 확인 합니다.  
  
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
  
 이 오류를 수신하는 ODBC 응용 프로그램은 문을 실행하기 전에 모든 커서 문 특성을 기본값으로 다시 설정해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 실행 &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
