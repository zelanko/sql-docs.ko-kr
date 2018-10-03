---
title: 사용자가 SQL 문을 입력 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 28256433802d686f4362b2b733fc2d2b13e65302
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612621"
---
# <a name="sql-statements-entered-by-the-user"></a>사용자가 입력한 SQL 문
일반적으로 임시 분석을 수행 하는 응용 프로그램 사용자가 SQL 문을 직접 입력할 수 있도록 허용 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
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
  
 이 방법은 응용 프로그램 코딩; 간소화 응용 프로그램에서 사용자가 SQL 문을 작성 하 고 설명의 유효성을 검사할 데이터 원본에 의존 합니다. SQL의 복잡성을 적절 하 게 노출 하는 그래픽 사용자 인터페이스를 작성 하는 것 이기 때문에 단순히 SQL 문 텍스트를 입력 하 라는 것이 좋습니다 대안을 수 있습니다. 그러나이 위해서는 사용자 SQL 뿐만 아니라 쿼리 중인 데이터 원본의 스키마를 알아야 합니다. 일부 응용 프로그램 사용 되는 사용자 수 기본 SQL 문을 만들고 수도 있는 사용자 수 있어서 텍스트 인터페이스를 제공 하는 그래픽 사용자 인터페이스를 제공 합니다.
