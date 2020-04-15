---
title: 비동기 모드 및 SQLCancel | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 014314eebdeabc137f9f1735e899f7d111105ed4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303759"
---
# <a name="creating-a-driver-application---asynchronous-mode-and-sqlcancel"></a>드라이버 애플리케이션 만들기 - 비동기 모드 및 SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  일부 ODBC 함수는 동기적 또는 비동기적으로 작동할 수 있습니다. 애플리케이션에서는 문 핸들이나 연결 핸들에 대해 비동기 작업을 설정할 수 있습니다. 연결 핸들에 대해 비동기 작업 옵션을 설정하면 연결 핸들의 모든 문 핸들에도 적용됩니다. 애플리케이션에서는 다음 문을 사용하여 비동기 작업을 설정하거나 해제합니다.  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 애플리케이션에서 ODBC 함수를 동기 모드로 호출하면 서버가 명령을 완료했다는 알림을 받을 때까지 드라이버가 애플리케이션에 제어를 반환하지 않습니다.  
  
 반면 비동기로 작업을 수행하는 경우 드라이버는 서버에 명령을 보내기 전이라도 즉시 애플리케이션에 제어를 반환합니다. 드라이버가 반환 코드를 SQL_STILL_EXECUTING으로 설정하여 애플리케이션이 다른 작업을 수행할 수 있게 됩니다.  
  
 명령 실행이 완료되었는지 테스트할 때 애플리케이션은 드라이버에 대해 동일한 매개 변수를 사용하여 동일한 함수를 호출합니다. 드라이버는 서버로부터 아직 응답을 받지 않은 경우 다시 SQL_STILL_EXECUTING을 반환합니다. 애플리케이션은 SQL_STILL_EXECUTING 이외의 코드가 반환될 때까지 명령을 주기적으로 테스트해야 합니다. 애플리케이션은 다른 반환 코드(SQL_ERROR 포함)가 수신되면 명령이 완료된 것으로 판단할 수 있습니다.  
  
 명령이 오랫동안 보류되는 경우도 있습니다. 응용 프로그램이 응답을 기다리지 않고 명령을 취소해야 하는 경우 **SQLCancel을 호출하여** 처리 되지 않은 명령과 동일한 문 핸들을 호출할 수 있습니다. **SQLCancel을** 사용해야 하는 유일한 시간입니다. 일부 프로그래머는 결과 집합을 통해 일부 방법을 처리하고 나머지 결과 집합을 취소하려는 경우 **SQLCancel을** 사용합니다. [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 또는 [SQLCloseCursor는](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) **SQLCancel이**아닌 미해결 결과 집합의 나머지 부분을 취소하는 데 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client ODBC 드라이버 애플리케이션 만들기](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
