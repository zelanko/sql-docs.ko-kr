---
title: 사용자가 입력한 SQL 문 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf2f8cf36be392cb42a970fa2fb0b19c35daeb39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301964"
---
# <a name="sql-statements-entered-by-the-user"></a>사용자가 입력한 SQL 문
임시 분석을 수행하는 응용 프로그램은 일반적으로 사용자가 SQL 문을 직접 입력할 수 있도록 합니다. 다음은 그 예입니다.  
  
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
  
 이 방법은 응용 프로그램 코딩을 단순화합니다. 응용 프로그램은 SQL 문을 작성하고 데이터 원본에 문의하여 명령문의 유효성을 확인합니다. SQL의 복잡성을 적절하게 노출하는 그래픽 사용자 인터페이스를 작성하는 것은 어렵기 때문에 사용자에게 SQL 문 텍스트를 입력하도록 요청하는 것이 좋습니다. 그러나 이렇게 하려면 SQL뿐만 아니라 쿼리되는 데이터 원본의 스키마도 알아야 합니다. 일부 응용 프로그램은 사용자가 기본 SQL 문을 만들고 사용자가 수정할 수 있는 텍스트 인터페이스를 제공할 수 있는 그래픽 사용자 인터페이스를 제공합니다.
