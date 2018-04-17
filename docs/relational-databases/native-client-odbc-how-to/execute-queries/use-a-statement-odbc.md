---
title: (ODBC) 문을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 338d2b2d4aebd252d5922d53f1cab854f6125216
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="use-a-statement-odbc"></a>문 사용(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-a-statement"></a>문을 사용하려면  
  
1.  SQL_HANDLE_STMT의 *HandleType*으로 [SQLAllocHandle](http://go.microsoft.com/fwlink/?LinkId=58396)을 호출하여 문 핸들을 할당합니다.  
  
2.  필요에 따라 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 호출하여 문 옵션을 설정하거나 [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)을 호출하여 문 특성을 가져옵니다.  
  
     서버 커서를 사용하려면 커서 특성을 기본값 이외의 값으로 설정해야 합니다.  
  
3.  문이 여러 번 실행되는 경우 필요에 따라 [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360)(SQLPrepare 함수)을 사용하여 문 실행을 준비합니다.  
  
4.  문에 바인딩된 매개 변수 표식이 있으면 필요에 따라 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)를 사용하여 프로그램 변수에 매개 변수 표식을 바인딩합니다. 문이 준비되어 있으면 [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) 및 [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)을 호출하여 매개 변수의 수와 특징을 확인할 수 있습니다.  
  
5.  SQLExecDirect를 사용하여 문을 직접 실행합니다.  
  
     \- 또는 -  
  
     문이 준비되어 있는 경우 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400)를 사용하여 여러 번 실행합니다.  
  
     \- 또는 -  
  
     카탈로그 함수를 호출하여 결과가 반환되도록 합니다.  
  
6.  결과 집합 열을 프로그램 변수에 바인딩하거나 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)를 사용하여 결과 집합 열에서 프로그램 변수로 데이터를 이동하거나 이 두 방법을 함께 사용하여 결과를 처리합니다.  
  
     문의 결과 집합을 한 번에 한 행씩 인출합니다.  
  
     \- 또는 -  
  
     블록 커서를 사용하여 결과 집합을 한 번에 여러 행씩 인출합니다.  
  
     \- 또는 -  
  
     [SQLRowCount](../../../relational-databases/native-client-odbc-api/sqlrowcount.md)를 호출하여 INSERT, UPDATE 또는 DELETE 문의 영향을 받는 행 수를 확인합니다.  
  
     SQL 문의 결과 집합이 여러 개이면 각 결과 집합의 끝에서 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 호출하여 추가로 처리할 결과 집합이 있는지 확인합니다.  
  
7.  결과 집합이 처리된 후에는 새 문을 실행하는 데 문 핸들을 사용할 수 있도록 하기 위해 다음 동작을 수행해야 할 수도 있습니다.  
  
    -   SQL_NO_DATA가 반환될 때까지 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 호출하지 않은 경우 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)를 호출하여 커서를 닫습니다.  
  
    -   매개 변수 표식을 프로그램 변수에 바인딩한 경우 *Option*을 SQL_RESET_PARAMS로 설정한 상태로 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)를 호출하여 바인딩된 매개 변수를 해제합니다.  
  
    -   결과 집합 열을 프로그램 변수에 바인딩한 경우 *Option*을 SQL_UNBIND로 설정한 상태로 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)를 호출하여 바인딩된 열을 해제합니다.  
  
    -   문 핸들을 다시 사용하려면 2단계로 이동합니다.  
  
8.  SQL_HANDLE_STMT의 *HandleType*으로 [SQLFreeHandle](../../../relational-databases/native-client-odbc-api/sqlfreehandle.md)을 호출하여 문 핸들을 해제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [실행 중인 쿼리 방법 도움말 항목 & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
