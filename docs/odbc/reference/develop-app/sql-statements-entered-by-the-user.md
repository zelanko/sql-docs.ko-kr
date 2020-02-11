---
title: 사용자가 입력 한 SQL 문 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78a1653df60b21cde772cbe32a688b3fdef80a42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086071"
---
# <a name="sql-statements-entered-by-the-user"></a>사용자가 입력한 SQL 문
임시 분석을 수행 하는 응용 프로그램은 일반적으로 사용자가 SQL 문을 직접 입력할 수 있습니다. 다음은 그 예입니다.  
  
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
  
 이 방법은 응용 프로그램 코딩을 간소화 합니다. 응용 프로그램은 사용자에 게 문의 유효성을 검사 하기 위해 SQL 문과 데이터 원본에 의존 합니다. 복잡 한 SQL을 적절 하 게 노출 하는 그래픽 사용자 인터페이스를 작성 하기 어렵기 때문에 사용자에 게 SQL 문 텍스트를 입력 하 라고 요청 하는 것이 좋습니다. 그러나이를 위해서는 사용자가 SQL 뿐만 아니라 쿼리 중인 데이터 원본의 스키마를 알고 있어야 합니다. 일부 응용 프로그램은 사용자가 기본 SQL 문을 만들 수 있는 그래픽 사용자 인터페이스를 제공 하며 사용자가 수정할 수 있는 텍스트 인터페이스도 제공 합니다.
