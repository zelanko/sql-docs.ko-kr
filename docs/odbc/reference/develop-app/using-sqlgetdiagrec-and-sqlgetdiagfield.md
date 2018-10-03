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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37fb095579fd173fd24a5df933e3e1a65edbeada
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626041"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 사용
응용 프로그램 호출 **SQLGetDiagRec** 하거나 **SQLGetDiagField** 진단 정보를 검색 합니다. 이러한 함수는 환경, 연결, 문 또는 설명자 핸들을 수락 하 고 마지막으로 해당 핸들을 사용 하는 함수에서 진단을 반환 합니다. 특정 핸들을 로그온 진단 해당 핸들을 사용 하 여 새 함수를 호출할 때 삭제 됩니다. 함수가 여러 진단 레코드를 반환 하는 경우 응용 프로그램에서는 이러한 함수를 여러 번; 상태 레코드의 총 수를 호출 하 여 검색 됩니다 **SQLGetDiagField** SQL_DIAG_NUMBER 옵션을 사용 하 여 헤더 레코드 (레코드 0)에 대 한 합니다.  
  
 응용 프로그램 호출 하 여 개별 진단 필드를 검색할 **SQLGetDiagField** 검색할 필드를 지정 합니다. 특정 진단 필드 핸들의 특정 형식에 대 한 의미를 갖지 않습니다. 진단 필드 및 해당 의미의 목록을 참조 하세요. 합니다 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다.  
  
 호출 하 여 SQLSTATE, 원시 오류 코드 및 단일 호출에서 진단 메시지를 검색 하는 응용 프로그램 **SQLGetDiagRec**; **SQLGetDiagRec** 헤더 레코드에서 정보를 검색에 사용할 수 없습니다.  
  
 예를 들어, 다음 코드는 SQL 문에 대 한 라는 메시지 하 고 실행 합니다. 모든 진단 정보를 반환 하는 경우 호출 **SQLGetDiagField** 상태 레코드의 번호를 가져오려면 및 **SQLGetDiagRec** 에서 SQLSTATE, 원시 오류 코드 및 진단 메시지를 가져오려면 기록 합니다.  
  
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
