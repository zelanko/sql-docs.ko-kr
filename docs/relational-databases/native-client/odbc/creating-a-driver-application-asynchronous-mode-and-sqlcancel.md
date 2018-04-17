---
title: 비동기 모드와 SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8984ec584c25ae3029f38d5bd3054479ced88b3a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="creating-a-driver-application---asynchronous-mode-and-sqlcancel"></a>드라이버 응용 프로그램-비동기 모드와 SQLCancel 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  일부 ODBC 함수는 동기적 또는 비동기적으로 작동할 수 있습니다. 응용 프로그램에서는 문 핸들이나 연결 핸들에 대해 비동기 작업을 설정할 수 있습니다. 연결 핸들에 대해 비동기 작업 옵션을 설정하면 연결 핸들의 모든 문 핸들에도 적용됩니다. 응용 프로그램에서는 다음 문을 사용하여 비동기 작업을 설정하거나 해제합니다.  
  
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
  
 응용 프로그램에서 ODBC 함수를 동기 모드로 호출하면 서버가 명령을 완료했다는 알림을 받을 때까지 드라이버가 응용 프로그램에 제어를 반환하지 않습니다.  
  
 반면 비동기로 작업을 수행하는 경우 드라이버는 서버에 명령을 보내기 전이라도 즉시 응용 프로그램에 제어를 반환합니다. 드라이버가 반환 코드를 SQL_STILL_EXECUTING으로 설정하여 응용 프로그램이 다른 작업을 수행할 수 있게 됩니다.  
  
 명령 실행이 완료되었는지 테스트할 때 응용 프로그램은 드라이버에 대해 동일한 매개 변수를 사용하여 동일한 함수를 호출합니다. 드라이버는 서버로부터 아직 응답을 받지 않은 경우 다시 SQL_STILL_EXECUTING을 반환합니다. 응용 프로그램은 SQL_STILL_EXECUTING 이외의 코드가 반환될 때까지 명령을 주기적으로 테스트해야 합니다. 응용 프로그램은 다른 반환 코드(SQL_ERROR 포함)가 수신되면 명령이 완료된 것으로 판단할 수 있습니다.  
  
 명령이 오랫동안 보류되는 경우도 있습니다. 응용 프로그램을 회신을 기다리지 않고 명령을 취소 하는 경우 가능한 것 호출 하 여 **SQLCancel** 동일한 문을 사용 하 여 처리 중인 명령으로 처리 합니다. 이 유일한 경우 **SQLCancel** 사용 해야 합니다. 사용 **SQLCancel** 결과 통해 일부 처리 있을 때 설정 하 고 결과 집합의 나머지 부분을 취소 하려고 합니다. [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 또는 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) 취소는 보류 중인 결과 집합의 나머지 부분을 사용해 **SQLCancel**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client ODBC 드라이버 응용 프로그램 만들기](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
