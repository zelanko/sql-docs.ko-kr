---
title: SQLGetDiagRec 및 SQLGetDiag필드 사용 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306754"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 사용
응용 프로그램은 진단 정보를 검색하기 위해 **SQLGetDiagRec** 또는 **SQLGetDiagField를** 호출합니다. 이러한 함수는 환경, 연결, 명령문 또는 설명자 핸들을 허용하고 해당 핸들을 마지막으로 사용한 함수에서 진단을 반환합니다. 특정 핸들에 기록된 진단 은 해당 핸들을 사용하여 새 함수를 호출할 때 삭제됩니다. 함수가 여러 진단 레코드를 반환하는 경우 응용 프로그램은 이러한 함수를 여러 번 호출합니다. 상태 레코드의 총 수는 SQL_DIAG_NUMBER 옵션을 사용 하 여 헤더 레코드 (레코드 0)에 대 한 **SQLGetDiagField** 호출 하 여 검색 됩니다.  
  
 응용 프로그램은 **SQLGetDiagField를** 호출하고 검색할 필드를 지정하여 개별 진단 필드를 검색합니다. 특정 진단 필드에는 특정 유형의 핸들에 대한 의미가 없습니다. 진단 필드 및 그 의미 목록은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명을 참조하십시오.  
  
 응용 프로그램은 **SQLGetDiagRec를**호출하여 단일 호출에서 SQLSTATE, 기본 오류 코드 및 진단 메시지를 검색합니다. **SQLGetDiagRec는** 헤더 레코드에서 정보를 검색하는 데 사용할 수 없습니다.  
  
 예를 들어 다음 코드는 사용자에게 SQL 문을 묻고 실행합니다. 진단 정보가 반환된 경우 **SQLGetDiagField를** 호출하여 상태 레코드 수와 **SQLGetDiagRec을** 사용하여 SQLSTATE, 기본 오류 코드 및 해당 레코드의 진단 메시지를 가져옵니다.  
  
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
