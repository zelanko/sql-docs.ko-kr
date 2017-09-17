---
title: "사용자가 SQL 문을 입력 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b234123c01d4bdf4590c000b996a4febe4ad485e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-statements-entered-by-the-user"></a>사용자가 입력 한 SQL 문
일반적으로 임시 분석을 수행 하는 응용 프로그램 SQL 문을 직접 입력할 수 있습니다. 예를 들어  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 이 간편 하 게 응용 프로그램을 코딩 합니다. 응용 프로그램에서 사용자가 SQL 문을 작성 하 고 설명의 유효성을 검사 하도록 데이터 원본에 의존 합니다. 적절 하 게 SQL의 고급 기능을 노출 하는 그래픽 사용자 인터페이스를 작성 하는 것 이기 때문에 단순히 SQL 문 텍스트를 입력 하 라는 것이 좋습니다 대신 사용할 수 있습니다. 그러나이 위해서는 사용자 SQL 뿐만 아니라 쿼리 중인 데이터 원본의 스키마에 알아야 합니다. 일부 응용 프로그램 기준이 사용자 기본 SQL 문을 만들고 수도 하는 사용자가 수정할 수 있는 텍스트 인터페이스를 제공 하는 그래픽 사용자 인터페이스를 제공 합니다.
