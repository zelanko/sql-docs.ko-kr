---
description: 버퍼 할당 및 해제
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 629c613e8c0aba4675b2b95c9c9ccd82fb7cdfb6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429475"
---
# <a name="allocating-and-freeing-buffers"></a>버퍼 할당 및 해제
응용 프로그램에서 모든 버퍼를 할당 하 고 해제 합니다. 버퍼가 지연 되지 않은 경우에는 함수를 호출 하는 동안에만 존재 해야 합니다. 예를 들어 **SQLGetInfo** 는 *Infovalueptr* 인수가 가리키는 버퍼의 특정 옵션과 연결 된 값을 반환 합니다. 다음 코드 예제와 같이 **SQLGetInfo**를 호출한 후 즉시이 버퍼를 해제할 수 있습니다.  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 지연 된 버퍼는 한 함수에서 지정 되 고 다른 함수에서 사용 되므로 드라이버가 여전히 존재 하는 동안 지연 된 버퍼를 해제 하는 것은 응용 프로그램 프로그래밍 오류입니다. 예를 들어, \* *ValuePtr* 나중에 **sqlfetch**에서 사용 하기 위해 **SQLBindCol** 에 전달 됩니다. 다음 코드 예제에 표시 된 것 처럼 **SQLBindCol** 또는 **SQLFreeStmt** 에 대 한 호출을 사용 하는 경우와 같이 열을 바인딩 해제 해야이 버퍼를 해제할 수 있습니다.  
  
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
  
 이러한 오류는 버퍼를 함수에서 로컬로 선언 하 여 쉽게 만들 수 있습니다. 응용 프로그램에서 함수를 벗어나면 버퍼가 해제 됩니다. 예를 들어 다음 코드는 드라이버에서 정의 되지 않은 동작을 발생 시킬 수 있습니다.  
  
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
