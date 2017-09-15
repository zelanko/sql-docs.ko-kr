---
title: "SQLGetDiagRec 및 SQLGetDiagField를 사용 하 여 | Microsoft Docs"
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
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: abd9c6e0b7d4a56f55e854dda6c61fe216a84ad5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField를 사용 하 여
응용 프로그램 호출 **SQLGetDiagRec** 또는 **SQLGetDiagField** 진단 정보를 검색 합니다. 이러한 함수는 환경, 연결, 문 또는 설명자 핸들에 동의 하 고 진단 마지막 해당 핸들을 사용 하는 함수 반환 합니다. 특정 핸들에 기록 하는 진단 해당 핸들을 사용 하는 새 함수를 호출할 때 삭제 됩니다. 함수가 여러 진단 레코드를 반환 하는 경우 응용 프로그램에서는 이러한 함수를 여러 번; 상태 레코드의 총 수를 호출 하 여 검색 **SQLGetDiagField** SQL_DIAG_NUMBER 옵션 헤더 레코드 (레코드 0)에 대 한 합니다.  
  
 호출 하 여 개별 진단 필드를 검색 하는 응용 프로그램 **SQLGetDiagField** 검색할 필드를 지정 하 고 있습니다. 특정 진단 필드 핸들의 특정 유형에 의미가 없습니다. 진단 필드와 해당 의미가 나와의 목록에 대 한 참조는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다.  
  
 호출 하 여 SQLSTATE, 원시 오류 코드 및 단일 호출에서 진단 메시지를 검색 하는 응용 프로그램 **SQLGetDiagRec**; **SQLGetDiagRec** 헤더 레코드에서 정보를 검색 하는 데 사용 될 수 없습니다.  
  
 예를 들어 다음 코드는 SQL 문에 대 한 사용자 요청 하 고이 실행 합니다. 진단 정보는 반환 된 경우 호출 **SQLGetDiagField** 상태 레코드의 수를 얻을 수 및 **SQLGetDiagRec** 된 SQLSTATE, 원시 오류 코드 및 진단 메시지를 가져오려는 레코드가 있습니다.  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {  
   // Get the status records.  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
