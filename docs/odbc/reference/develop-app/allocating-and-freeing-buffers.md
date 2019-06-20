---
title: 버퍼 할당 및 해제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388147de8935d36180ba9845c8353bbf3dd6edc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288080"
---
# <a name="allocating-and-freeing-buffers"></a>버퍼 할당 및 해제
모든 버퍼가 할당 되 고 응용 프로그램에서 해제 합니다. 버퍼 연기 되지 않고, 하는 경우 함수에 대 한 호출 중에 존재 해야 합니다. 예를 들어 **SQLGetInfo** 가리키는 버퍼의 특정 옵션을 사용 하 여 연결 된 값을 반환 합니다 *InfoValuePtr* 인수입니다. 이 버퍼를 호출한 후 즉시 해제할 수 있습니다 **SQLGetInfo**다음 코드 예제 에서처럼:  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 지연 된 버퍼는 하나의 함수에 지정 되 고 다른 사용, 이므로 드라이버 여전히 존재 하는 동안 지연 된 버퍼를 해제 하려면 응용 프로그램 프로그래밍 오류가 있습니다. 주소의 예는 \* *ValuePtr* 버퍼가 전달 될 **SQLBindCol** 에서 나중에 사용할 **SQLFetch**합니다. 이 버퍼 열에 대 한 호출을 사용 하 여 같은 바인딩된 없을 때까지 해제 될 수 없습니다 **SQLBindCol** 하거나 **SQLFreeStmt** 다음 코드 예제 에서처럼:  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 함수를 로컬로 버퍼를 선언 하 여 이러한 오류가 쉽게 발생 버퍼는 응용 프로그램 함수를 벗어날 때 해제 됩니다. 예를 들어, 다음 코드는 드라이버에서 정의 되지 않은 및 아마도 심각한 동작을 발생:  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
