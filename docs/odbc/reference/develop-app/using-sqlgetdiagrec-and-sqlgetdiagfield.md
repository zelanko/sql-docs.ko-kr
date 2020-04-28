---
title: SQLGetDiagRec 및 SQLGetDiagField 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69a17086253b40469b0ed98cb6f870f319f03f52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306754"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 사용
응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField** 를 호출 하 여 진단 정보를 검색 합니다. 이러한 함수는 환경, 연결, 문 또는 설명자 핸들을 수락 하 고 해당 핸들을 마지막으로 사용한 함수에서 진단을 반환 합니다. 해당 핸들을 사용 하 여 새 함수를 호출 하면 특정 핸들에 기록 된 진단이 삭제 됩니다. 함수가 여러 진단 레코드를 반환 하는 경우 응용 프로그램은 이러한 함수를 여러 번 호출 합니다. 상태 레코드의 총 수는 SQL_DIAG_NUMBER 옵션을 사용 하 여 헤더 레코드 (레코드 0)에 대해 **SQLGetDiagField** 를 호출 하 여 검색 합니다.  
  
 응용 프로그램은 **SQLGetDiagField** 를 호출 하 고 검색할 필드를 지정 하 여 개별 진단 필드를 검색 합니다. 특정 진단 필드는 특정 유형의 핸들에 대해 의미가 없습니다. 진단 필드 목록과 해당 의미에 대 한 자세한 내용은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명을 참조 하세요.  
  
 응용 프로그램은 **SQLGetDiagRec**를 호출 하 여 단일 호출에서 SQLSTATE, 네이티브 오류 코드 및 진단 메시지를 검색 합니다. **SQLGetDiagRec** 는 헤더 레코드에서 정보를 검색 하는 데 사용할 수 없습니다.  
  
 예를 들어 다음 코드는 사용자에 게 SQL 문을 입력 하 라는 메시지를 표시 하 고 실행 합니다. 반환 된 진단 정보가 있는 경우 **SQLGetDiagField** 를 호출 하 여 상태 레코드 수를 가져오고 **SQLGetDiagRec** 를 호출 하 여 해당 레코드에서 SQLSTATE, 원시 오류 코드 및 진단 메시지를 가져옵니다.  
  
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
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
